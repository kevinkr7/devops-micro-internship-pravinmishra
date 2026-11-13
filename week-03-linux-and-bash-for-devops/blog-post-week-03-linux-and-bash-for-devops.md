# Production Linux & Governed Agentic Triage: What 14 Days of DevOps Drills Taught Me

**Author:** Kevin K R  
**Cohort:** DevOps Micro Internship (DMI) with Agentic AI — Cohort 3  
**Track:** Agentic AI & Core DevOps  
**Date:** November 2026  

---

## 1. Moving from Theoretical Linux to Production SRE Discipline

When developers first learn Linux, the curriculum often feels like a memory game: memorize `ls`, `grep`, `chmod`, and `ps`. But operating a production Linux server under active traffic on AWS is an entirely different discipline. 

During Week 3 of the **DevOps Micro Internship (DMI) with Agentic AI** led by **Pravin Mishra**, we stopped treating Linux as a set of disconnected terminal commands and began treating it as an interconnected operating system runtime that demands structured operational rigor.

Deploying both a React single-page application and the EpicReads digital bookstore on an AWS Ubuntu 22.04 LTS instance using Nginx exposed me to the reality of systems engineering:
- **Socket binding and kernel networking:** A process isn’t "running" just because it was launched; it must be verified with `ss -tulpen` to confirm socket states, IP binding (`0.0.0.0:80` vs `127.0.0.1:80`), and firewall ingress policies.
- **Service supervision via systemd:** Configuring Nginx units to be persistent (`systemctl enable nginx`), analyzing journal entries via `journalctl -u nginx`, and executing zero-downtime SIGHUP reloads rather than abrasive hard restarts.
- **Client-Side Routing Realities:** Understanding why single-page applications crash on page refresh without explicit reverse proxy fallback directives (`try_files $uri $uri/ /index.html;`).

---

## 2. The Operational Checklist: The Engineer's Safety Net

One of the most transformative drills of this week was the **Production Maintenance Drill (OPS Checklist)**. In high-pressure on-call scenarios, engineers do not have the luxury of guessing. You need deterministic, repeatable checklists:

1. **Network Layer Audit:** Verifying interface allocation (`ip a`), inspecting listening TCP sockets (`ss -tulpen`), and validating host firewall rules (`ufw status`).
2. **Log Anomaly Tracing:** Correlating real-time HTTP access entries in `/var/log/nginx/access.log` with systemd unit journals and checking `/var/log/nginx/error.log` for worker crashes or upstream pipe leaks.
3. **Capacity & Resource Red Flags:** Diagnosing CPU load averages against core counts (`uptime`), auditing memory consumption (`free -h`) to safeguard against the Linux Out-Of-Memory (OOM) killer on burstable `t2.micro` instances, and checking disk inode and block saturation (`df -h`).
4. **Controlled Chaos & Recovery:** Deliberately injecting configuration syntax errors and simulating missing webroot artifacts, followed by systematic rollback and recovery verification returning HTTP 200 OK.

---

## 3. Engineering Enterprise Automation with Bash

Bash is often dismissed as a legacy scripting tool, but in modern DevOps, clean shell scripts form the critical glue between cloud provisioning, container initialization, and host monitoring.

Through the **Bash Script Automation Drill**, I built a modular suite of production utilities covering:
- **Defensive Shell Principles:** Strict parameter expansion, error traps (`set -euo pipefail`), and portable shebang execution (`#!/bin/bash`).
- **Data Structures in Shell:** Harnessing arrays and iteration (`for tool in "${tools[@]}"`) to execute multi-service availability sweeps.
- **Conditionals & File Safety:** Verifying directory structures (`-d`) and file existence (`-f`) before applying changes to prevent destructive race conditions.
- **Modular Functions:** Encapsulating reusable operational logic into self-contained units (`check_service`, `check_disk`) orchestrated by clean `main` routines.

---

## 4. Bridging Linux Operations with Agentic AI (Claude Code)

The capstone of Week 3 was connecting our deterministic Linux triage automation to an autonomous AI workflow using **Claude Code**.

Rather than blindly asking an LLM *"Why is my server down?"* (which yields speculative hallucinations), we engineered an **AI-Assisted Linux Incident Triage Loop**:
- **Deterministic Gathering (Bash):** Our read-only `./scripts/linux-triage.sh` script executes 5 empirical checks across systemd status, port 80 socket binding, loopback HTTP responsiveness, memory headroom, and root disk capacity, outputting standardized exit codes (0 for Healthy, 1 for Fail, 2 for Warn).
- **Architectural Guardrails (`CLAUDE.md` & Skills):** We encapsulated this triage routine into a custom Claude Code skill (`/linux-triage`) restricted strictly to `allowed-tools: Bash, Read, Grep` (no Write permissions).
- **Human-in-the-Loop Governance:** In accordance with our `CLAUDE.md` safety constitution, the agent is strictly prohibited from executing automatic restarts or destructive remediation commands. It correlates the raw failure data, diagnoses root cause, and provides a clear, suggested recovery command for the human engineer to review and execute.
- **Objective Verification:** Once the engineer executes the fix, a second triage invocation verifies that all 5 checks return green with exit code 0.

---

## 5. Key Personal Reflection

Autonomous agents are only as reliable as the empirical boundaries engineers construct for them. Without low-level Linux fluency, an engineer cannot write the scripts that feed AI agents truth, nor can they verify whether an agent’s diagnosis is sound. 

Real DevOps engineering is not about replacing human judgment with AI; it is about combining the speed of agentic analysis with the safety of strict architectural guardrails.

---

> **P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by [Pravin Mishra](https://www.linkedin.com/in/pravin-mishra-aws-trainer/). My graded progress is public: https://dmi.pravinmishra.com/s/kevinkr7.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-blog&utm_campaign=cohort3**

---

#DMIByPravinMishra #DevOps #Linux #Bash #SRE #AWS #Nginx #AgenticAI #ClaudeCode #Cohort3
