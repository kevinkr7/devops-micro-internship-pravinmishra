# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/agents/` with all 3 files

![VS Code sidebar showing .claude/agents/ with all 3 files](screenshots/a4-ss1-agents-folder.png)

---

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

The cost optimizer performs lightweight, rule-based infrastructure checks such as inspecting resource configurations, evaluating tagging, and identifying obvious cost savings (e.g. storage tiering, unneeded redundancy). Because this task does not require multi-step deep reasoning or complex code synthesis, Claude Haiku is the ideal choice — it executes much faster, consumes significantly fewer tokens/costs, and keeps routine operational audits quick and economical.

---

#### 2. Why does the security auditor NOT have Write in its tools list?

The security auditor follows the core security principle of least privilege and strict separation of duties. Its sole responsibility is inspection, risk identification, and reporting vulnerabilities — never modifying code or infrastructure directly. Withholding the `Write` permission prevents accidental, unauthorized, or unintended alterations to production Terraform configurations during an audit.

---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

The Terraform writer needs adaptability depending on the complexity of the task and the user's active session configuration. By setting `inherit`, the agent dynamically adopts whatever model the user has currently configured in their primary Claude Code session (e.g., Sonnet or Opus for complex multi-module architecture generation, or a faster model for minor tweaks) rather than hardcoding a single fixed model.

---

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

![security-auditor.md frontmatter configuration](screenshots/a4-ss2-security-auditor-frontmatter.png)

---

#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

![cost-optimizer.md frontmatter configuration](screenshots/a4-ss3-cost-optimizer-frontmatter.png)

---

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor

![Claude launching security-auditor delegation](screenshots/a4-ss4-security-auditor-launch.png)

---

#### Screenshot 5 — Security audit report output

![Security audit report output](screenshots/a4-ss5-security-report.png)

---

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report

![Cost optimization delegation and report](screenshots/a4-ss6-cost-optimizer-launch.png)

---

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/kevinkr7/devops-micro-internship-pravinmishra

*Starter Repository Fork:* https://github.com/kevinkr7/Ultimate-Agentic-DevOps-with-Claude-Code

---

# Completion Checklist

- [x] `.claude/agents/` folder contains all 3 agent files
- [x] Screenshot 2 shows correct `security-auditor.md` configuration
- [x] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [x] All 3 written answers completed 
- [x] Security auditor executed successfully
- [x] Cost optimizer executed successfully
- [x] Security report is visible with findings
- [x] Cost report is visible with recommendations
- [x] All required screenshots added
- [x] GitHub repo updated with agents

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