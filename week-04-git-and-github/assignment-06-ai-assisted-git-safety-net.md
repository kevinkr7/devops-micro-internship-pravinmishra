# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

![Screenshot 1 — Output of git remote -v and git branch](./screenshots/a6-ss1-branch-setup.png)

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

Working on a dedicated feature branch (`feature/ai-pr-ready`) isolates experimental, in-progress code and safety experiments from the stable production trunk (`main`). In DevOps and continuous delivery environments, the `main` branch represents deployable, verified infrastructure and application code. 

By isolating changes on a feature branch, we ensure that:
1. Production code is never polluted with untested features or intermediate exploratory commits.
2. Other team members can continue shipping fixes and features without merge conflicts or unverified code interfering with their workflows.
3. Automated CI/CD gates, secret scanners, and peer reviews can be executed specifically against the isolated pull request branch before merging.
4. Rollbacks or abandoning experimental work becomes trivial (deleting a branch) without altering git commit history on `main`.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of `git status` showing the staged file on feature/ai-pr-ready

![Screenshot 2 — Output of git status showing staged risky file](./screenshots/a6-ss2-status-risky.png)

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

Using an RFC-compliant, standard documentation dummy key (such as AWS's official sample format `AKIAIOSFODNN7EXAMPLE`) allows us to rigorously test regex pattern matchers and deterministic validation logic without exposing sensitive cloud credentials. 

Real access keys, if committed to version control—even for a split second or on a private repository—are immediately scraped by automated botnets, credential stuffers, and GitHub's automated secret scanning partner program. Exposing a live key triggers immediate revocation, security alarms, potential unauthorized resource provisioning, and significant financial liability. A fake key provides 100% realistic syntax for deterministic testing while maintaining zero security exposure.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![Screenshot 3 — hooks/pre-commit open in VS Code](./screenshots/a6-ss3-hook-vscode.png)

---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![Screenshot 4 — Output of git config core.hooksPath](./screenshots/a6-ss4-hooks-path-config.png)

---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Files inside `.git/` are strictly local to a single cloned repository instance; Git never tracks, commits, or pushes the `.git/hooks/` directory to remote remotes. If hooks are placed only in `.git/hooks/`, every developer, CI/CD runner, or collaborator would have to manually recreate or copy the script onto their machine, leading to inevitable security omissions and inconsistent enforcement.

By placing the hook in a version-controlled directory (`hooks/pre-commit`) and configuring `git config core.hooksPath hooks`, the security rules and automated verification gates become part of the repository's codebase. Team members automatically receive the hook upon cloning or pulling, guaranteeing uniform security governance across the entire team and automated build agents.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

`PreToolUse` and Git `pre-commit` hooks are both deterministic interceptors that operate as guardrails before an irreversible mutation occurs:
- **What `PreToolUse` intercepts:** In Claude Code's agentic loop, `PreToolUse` intercepts an LLM's proposed tool invocation (e.g., executing a bash command or writing a file) before the system executes it in the workspace.
- **What `pre-commit` intercepts:** In Git's lifecycle, the `pre-commit` hook intercepts the `git commit` command immediately after staging, inspecting the staged snapshot before a permanent SHA-1 commit object is created in the Git history database.
- **What they have in common:** Both mechanisms operate deterministically without AI guessing, evaluate incoming payloads against explicit policy rules (regex patterns, banned prefixes, size constraints), and exit with a non-zero status code to instantly abort unauthorized or high-risk actions. Both prioritize fail-safe prevention over post-incident recovery.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

![Screenshot 5 — Terminal showing git commit rejected with BLOCKED message](./screenshots/a6-ss5-commit-blocked.png)

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line matching the key was:
```bash
if git diff --cached --name-only | xargs -r grep -E -n "AKIA[0-9A-Z]{16}" /dev/null 2>/dev/null; then
```
This regex matched because AWS IAM Access Key IDs follow a strict deterministic format: the static 4-character prefix `AKIA` followed by exactly 16 uppercase alphanumeric characters. When `git diff --cached` evaluated `services/api_service.py`, line 12 contained `aws_access_key_id="AKIAIOSFODNN7EXAMPLE"`. The pattern detected the `AKIA` prefix followed by the 16 characters `IOSFODNN7EXAMPLE`, causing the grep check to succeed, print the offending file and line number, output the `[BLOCKED]` alert, and terminate the commit process with exit status 1.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No, this hook would completely miss a secret stored in an arbitrary variable like `token = "x98f219084bd"` or `client_secret = "mypassword123"` because standard static regex patterns rely exclusively on predefined syntactic signatures (like the `AKIA` prefix).

This highlights the fundamental limitation of fixed, deterministic rules: they are rigid and only catch what they have been explicitly programmed to match. If a secret does not adhere to known regex patterns, or if an engineer obfuscates credentials, fixed rules produce false negatives (missed threats). Conversely, overly broad regex rules produce frequent false positives (flagging random hashes or UUIDs). This is precisely why fixed rules must be augmented with contextual, semantic AI reviewers that analyze code intent and context.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

![Screenshot 6 — SKILL.md frontmatter open in VS Code](./screenshots/a6-ss6-skill-frontmatter.png)

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

![Screenshot 7 — /pr-ready output flagging staged issues](./screenshots/a6-ss7-pr-ready-flagged.png)

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

The `/pr-ready` skill is designed as an advisory, read-only analysis tool that supports the engineer rather than acting on its own. Granting `Bash`, `Read`, and `Grep` provides the agent sufficient capability to execute read-only git commands (such as `git diff --cached` and `git status`), read file contents, and search for patterns across the codebase.

Excluding `Write` guarantees by architectural design that the AI model cannot inadvertently modify files, add unverified lines of code, create commits, push to remote repositories, or trigger pull requests without human permission. This enforces strict privilege separation: the AI evaluates and advises, but the human engineer maintains absolute control over modifications to the repository state.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both mechanisms correctly caught the hardcoded AWS Access Key ID (`AKIAIOSFODNN7EXAMPLE`). However, their scope and contextual depth differed substantially:
- **What `/pr-ready` caught that the hook didn't:** `/pr-ready` detected the contextual code hygiene issue of the active `print(f"DEBUG: ...")` statement, recognizing it as inappropriate for production pull requests, and suggested replacing it with structured logging (`logger.debug()`). It also analyzed the semantic intent of the diff to assess PR readiness and drafted conventional commit descriptions.
- **What the pre-commit hook did that `/pr-ready` didn't:** The pre-commit hook provided an absolute, non-negotiable blocker directly in the Git terminal stream, completely aborting execution with exit code 1. The hook guarantees zero tolerance for policy violations, whereas `/pr-ready` provides intelligent diagnostic analysis and constructive remediation advice.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

![Screenshot 8 — git commit succeeding after fix](./screenshots/a6-ss8-commit-success.png)

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

![Screenshot 9 — Second /pr-ready run showing clean report and PR draft](./screenshots/a6-ss9-pr-ready-clean.png)

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

To satisfy the pre-commit hook and code hygiene standards, two distinct modifications were made to `services/api_service.py`:
1. **Replaced Hardcoded Secret with Environment Variable:** The hardcoded string `aws_access_key_id="AKIAIOSFODNN7EXAMPLE"` was replaced with a dynamic credential lookup: `aws_access_key_id=os.environ.get("AWS_ACCESS_KEY_ID")`. This completely eliminated the `AKIA` string literal from the staged diff, satisfying the regex rule in `hooks/pre-commit`.
2. **Purged Leftover Debug Statement:** The raw `print(f"DEBUG: connecting to endpoint {endpoint}")` call was deleted and replaced with standard production logging via `logging.getLogger(__name__).debug(...)`.

After staging the clean file with `git add`, the pre-commit hook scanned the staged diff, verified zero matches, and exited with status 0, allowing the commit to proceed cleanly.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

![Screenshot 10 — Pull Request showing base repo as own fork and AI drafted content](./screenshots/a6-ss10-pr-opened.png)

---

#### PR Link

`https://github.com/kevinkr7/devops-micro-internship-pravinmishra/pull/14`

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

While the AI draft provided an excellent summary structure and accurate bullet points, I made two specific refinements before submitting the Pull Request:
1. **Added Explicit Verification Evidence:** I included the exact terminal outputs showing that `hooks/pre-commit` executed and exited with code 0, as well as the confirmed clean `/pr-ready` report. AI drafts typically include placeholder verification notes, so adding concrete command results proves that empirical testing occurred.
2. **Clarified Architecture Scope:** I updated the summary to explicitly state that the PR introduced both the deterministic bash hook and the Claude Code skill for future engineering consistency, providing vital architectural context for reviewers.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

Blindly copy-pasting an AI draft introduces significant risks into the engineering workflow:
- **Hallucinated Changes:** The AI might summarize functions or files that were not actually altered or misunderstand subtle configuration nuances.
- **False Verification Claims:** AI models often hallucinate verification statements such as "All unit tests passed with 100% coverage" even if tests were never run or do not exist in the repository.
- **Security & Privacy Leaks:** An AI might accidentally echo internal environment details, endpoints, or project names that should remain unexposed.
- **Reviewer Misalignment:** A generic or inaccurate description wastes peer reviewers' time, masks potential bugs, and diminishes engineering trust.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This assignment involves creating local learning exercises, dummy mock files (`services/api_service.py`), and customized practice skills. These additions are designed specifically for student skill development and portfolio demonstration in our personal forks.

If this PR were opened against the shared upstream repository (`pravinmishraaws/devops-micro-internship-pravinmishra`), it would spam the upstream project maintainers with personal practice branches, introduce unrelated files into the class curriculum templates, and create merge conflicts for hundreds of other students syncing from upstream. Targeting our own fork keeps open-source upstream clean and follows sound Git governance.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

The **Gather** phase occurs when the tooling collects empirical data about the system's current state:
- When the pre-commit hook runs `git diff --cached --name-only` and `git diff --cached` to gather all staged code lines.
- When the Claude Code `/pr-ready` skill runs `git diff --cached` and inspects repository status and file structures using `Bash`, `Read`, and `Grep`.
- In both cases, the tools gather raw, objective facts about the staged changes without making assumptions or modifying state.

---

**2. Which step(s) represent Analyze?**

The **Analyze** phase represents evaluating the gathered facts against defined standards:
- The pre-commit hook analyzes the diff against deterministic regex expressions (`AKIA[0-9A-Z]{16}`) and checks file size limits (`MAX_SIZE=1048576`).
- The `/pr-ready` Claude Code skill analyzes the semantic context of the changes, evaluating whether variable naming indicates hidden credentials, whether debug statements were left behind, whether commits mix unrelated concerns, and formulating a coherent summary.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

The **Human Act** phase occurs when the engineer makes the conscious decision to fix the code, stage the clean files, execute `git commit`, push the branch to GitHub (`git push`), and formally open the Pull Request.

A human must execute these actions because accountability in engineering belongs exclusively to people, not language models. An AI cannot accept legal, security, or financial responsibility for shipping bugs, leaking customer data, or introducing infrastructure regressions. By keeping the human in the loop as the sole authorized actor, we ensure that automated tools advise while the engineer verifies and takes ownership of every production change.

---

**4. Which step is Verify?**

The **Verify** phase occurs after the remediation has been applied:
- Re-running `git commit` to verify that the pre-commit hook passes cleanly with zero violations (exit code 0).
- Re-running the `/pr-ready` skill to confirm that the risk report is completely clean and that the generated PR title and description accurately reflect the final tested increment.
- Reviewing the open Pull Request on GitHub to confirm that the branch comparison is conflict-free and ready for review.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

Fixed-rule pre-commit hooks provide fast, deterministic, non-negotiable guarantees against known critical patterns (like AWS keys and oversized files), but cannot understand code context or intent. The AI skill fills this gap by evaluating semantic hygiene, detecting subtle risks, and synthesizing meaningful documentation, but lacks the guaranteed enforcement power of a hard gate; together, they form a robust defense-in-depth safety net.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

Add your LinkedIn post URL here...

`https://www.linkedin.com/posts/kevinkr77_dmibypravinmishra-devops-claudecode-activity-7509928192408371200-Pq9w?utm_source=share&utm_medium=member_desktop`

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

- **Defense-in-Depth Git Governance:** Combining deterministic pre-commit hooks with contextual AI skills creates a balanced safety net where strict security rules are enforced without human error while code quality is elevated through intelligent semantic review.
- **Repository-Tracked Hook Configuration:** Configuring `core.hooksPath` to point to a committed `hooks/` directory ensures uniform security policies across all developers and CI/CD pipelines, overcoming the limitation of untracked `.git/hooks/`.
- **Restricted Agentic Capabilities:** Enforcing read-only permissions (`allowed-tools` without `Write`) in AI skills prevents autonomous agents from modifying code or executing unverified commits, preserving human agency and auditability.
- **Strict Adherence to the Agentic Loop:** Structuring developer workflows around Gather → Analyze → Human Act → Verify guarantees that AI augments decision-making while human engineers retain ultimate operational responsibility.

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`https://github.com/kevinkr7/devops-micro-internship-pravinmishra`

---

# Completion Checklist

- [x] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [x] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [x] `core.hooksPath` configured to point at `hooks/`
- [x] Pre-commit hook shown blocking the risky commit
- [x] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [x] `/pr-ready` run against the risky diff and shown flagging issues
- [x] Risky file fixed; `git commit` succeeds cleanly
- [x] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [x] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [x] Agentic Loop mapping (Task 7) completed in your own words
- [x] LinkedIn post published and URL submitted
- [x] All required screenshots added
- [x] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
