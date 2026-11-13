# Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

![Jira Create Project Screen](screenshots/a4-ss1-jira-create-project.png)

---

### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

- **Product Owner (PO):** Prioritized candidate conversion and employer credibility features (salary range badges, verified company tags, and an accessible 'Apply Now' CTA button).
- **Scrum Master (SM):** Enforced the strict 90-minute time-box, guided Planning Poker estimation, ensured Definition of Done (DoD) compliance, and facilitated the retrospective.
- **Dev Lead:** Implemented UI stylesheet enhancements for Story GJ-3 (`.btn-apply-cta` with color `#0284c7`, hover transition `#0369a1`, and responsive flexbox alignment).
- **DevOps Lead:** Managed Git feature branching (`feature/gotto-cta-polish`), synchronized static assets to AWS EC2 Nginx web root at `http://54.210.88.142/gotto-job`, and verified live response codes.

---

# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

![Project Created Settings Sidebar](screenshots/a4-ss2-project-created-sidebar.png)

---

# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

![Backlog Epic Panel Created](screenshots/a4-ss3-epic-panel-created.png)

---

# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

![Backlog Six Stories Ranked](screenshots/a4-ss4-backlog-six-stories.png)

---

#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

![Story Points and Acceptance Criteria](screenshots/a4-ss5-story-points-acceptance-criteria.png)

---

# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

![Planning Poker Points in Backlog](screenshots/a4-ss6-planning-poker-points.png)

---

### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

- **GJ-1: Highlight salary range badge on job search cards (2 pts):** Requires badge formatting and conditional CSS chips across list views; moderate risk.
- **GJ-2: Add company verified trust badge next to employer name (1 pt):** Simple inline SVG verification checkmark with tooltip next to employer headings; straightforward and low risk.
- **GJ-3: Polish primary job application CTA button styling and hover state (1 pt):** Single UI component styling with hover elevation and focus states; debated 1 vs 2 pts, settled on 1 pt due to pure presentation scope.
- **GJ-4: Sticky filter bar for remote / location job preferences (3 pts):** Highest complexity story involving CSS sticky positioning, z-index stacking, and mobile viewport scroll clipping.
- **GJ-5: Quick-apply modal microcopy and validation clarity (2 pts):** Form input validation messages and microcopy adjustments across standard modal fields.
- **GJ-6: Footer copyright, version v1.0, and trust disclaimer (1 pt):** Static HTML container in page footer with version metadata; very low risk and easily verifiable.

---

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

![Sprint 1 Selected Stories](screenshots/a4-ss7-sprint-1-stories.png)

---

#### Screenshot 8 — One Story showing the Sub-tasks created

![Story Subtasks Breakdown](screenshots/a4-ss8-story-subtasks.png)

---

# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

![Burndown Chart Opened](screenshots/a4-ss9-burndown-chart-opened.png)

---

# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

![Jira Board Story Moved to Done](screenshots/a4-ss10-board-story-done.png)

---

#### Screenshot 11 — Git commit output

![Git Commit Output](screenshots/a4-ss11-git-commit-output.png)

---

#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

![Live UI Change in Browser](screenshots/a4-ss12-live-ui-change.png)

---

# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

![Jira Retro Comment](screenshots/a4-ss13-jira-retro-comment.png)

---

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/kevinkr77_devops-scrum-agile-activity-7262119284729104893-gotto`

---

#### Screenshot 14 — Published LinkedIn post

![Published LinkedIn Post](screenshots/a4-ss14-linkedin-post.png)

---

# Submission Instructions

- Add all 14 required screenshots
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [x] Task 1: Team Mode or Solo Mode selected and all four roles documented (Screenshot 1 & Notes)
- [x] Task 2: Team-managed Scrum project created with the required name (Screenshot 2)
- [x] Task 3: UI improvement Epic created (Screenshot 3)
- [x] Task 4: 6–8 Stories added under the Epic and ranked by value (Screenshots 4 & 5)
- [x] Task 5: Story Points set (1, 2, or 3) with reasoning recorded (Screenshot 6 & Notes)
- [x] Task 6: Sprint 1 created with Sprint Goal, 3–4 Stories, and Sub-tasks (Screenshots 7 & 8)
- [x] Task 7: Burndown Chart opened (Screenshot 9)
- [x] Task 8: One UI-only increment implemented, committed, deployed, and verified (Screenshots 10–12)
- [x] Task 9: Retro comment with one Scrum pillar and one Scrum value (Screenshot 13)
- [x] Task 10: Mandatory LinkedIn post published with the live URL, backlog refinement, Sprint planning, one shipped increment, proof, and Screenshot 14
- [x] Full Name visible in required screenshots
- [x] No sensitive data exposed

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
