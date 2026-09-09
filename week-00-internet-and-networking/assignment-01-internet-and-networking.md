# Week 00 - Internet and Networking

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

# 🧑‍💻 Task 1: Using ChatGPT as Your Learning Assistant

## Scenario

You're new to DevOps and will frequently encounter technical questions. ChatGPT can be your learning companion.

## Your Task

Write a clear ChatGPT prompt to help you understand:

> "What is a protocol in networking? Explain with a simple real-life example."

Take a screenshot of your interaction showing:

* Your detailed prompt (with clear expectations)
* ChatGPT's simplified response with an example

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![Task 1 Screenshot](screenshots/week-00-ChatGPT-prompt.png)
![Task 1 Screenshot](screenshots/week-00-ChatGPT-response-simplified.png)


Replace `task-1-chatgpt.png` with your actual screenshot file name.

---

## What I Learned (2–3 lines)

By providing chatGPT with a clear context, role, audience, depth, examples, and formatting requirements, I transformed a topic into a structured and relatable learning experience.
I have also discovered by working with and refining the prompts over time, that I can extract and assimilate information much more effectively by asking for an iteration of the prompt to make it simpler, analogue, provide examples from real life or provide a summary that is screen friendly. 

---

# 🌐 Task 2: Internet and Networking

## Scenario

Your friend is launching an online bookstore named **EpicReads**.

He asked you to explain how users globally can access his website hosted in Finland.

## Your Task

Write a short explanation (**100–150 words**) that includes:

* Packet Switching
* IP Address
* TCP/IP
* HTTP/HTTPS

💡 **Tip:** You may use ChatGPT (as demonstrated in Task 1) to refine your explanation.

## Answer

## 🌍 How Users Globally Access EpicReads

Imagine **EpicReads** is a bookstore website hosted on a server in Finland 🇫🇮, while customers are located around the world 🌎.

When a user opens EpicReads, the website data is divided into small **packets 📦**. Using **Packet Switching**, these packets travel across different networks and routers, possibly taking different paths, before reaching the user's device.

Every device involved has an **IP Address 📍**, which acts like a digital address and helps identify where packets should be sent.

**TCP/IP 🚚** provides the basic communication rules: **IP** handles addressing and routing, while **TCP** ensures data is delivered reliably and in the correct order.

Finally, **HTTP/HTTPS 🌐** allows the browser and EpicReads' server to communicate. **HTTPS 🔐** encrypts the communication, keeping sensitive information such as passwords and payment details safer.

Thus, users worldwide can access EpicReads even though its server is located in Finland.

---

# 🏗️ Task 3: Application Architecture & Stack

## Scenario

EpicReads bookstore has two application versions:

### Two-Tier Application

* Frontend
* Database

### Three-Tier Application

* Frontend
* Backend
* Database

## Your Task

* Draw simple diagrams (hand-drawn or tool-based such as draw.io)
* Label each layer clearly
* List at least two common technologies or tools used for each layer
* Submit a screenshot or photo clearly showing your own drawing

## Diagram Screenshot / Photo

Save your diagram image in the `screenshots` folder and update the file name below.

<p align="center">
  <img src="screenshots/Two-tier.drawio.png" alt="Two-Tier Architecture Diagram">
  <br>
  <strong>Two-Tier Architecture</strong>
</p>

<br>

<p align="center">
  <img src="screenshots/Three-tier.drawio.png" alt="Three-Tier Architecture Diagram">
  <br>
  <strong>Three-Tier Architecture</strong>
</p>

Replace `task-3-diagram.png` with your actual diagram file name.

---

## Technologies Used

### Frontend

- React
- Angular
- Vue.js
- HTML/CSS
- JavaScript
- TypeScript
- Next.js

### Backend

- Node.js
- Express.js
- FastAPI
- Django
- Flask
- Spring Boot
- ASP.NET Core
- Laravel

### Database

- PostgreSQL
- MySQL
- MongoDB
- Oracle Database
- Microsoft SQL Server
- SQLite
- Redis
- MariaDB

---

# 🌍 Task 4: Domain Name & DNS (Basic Concepts)

## Scenario

Your friend's bookstore **EpicReads** is currently accessible through:

```text
52.172.142.222:3000
```

He purchased the domain:

```text
epicreads.com
```

## Your Task

In **50–100 words**, explain in your own words:

1. What is DNS (Domain Name System)?
2. Which DNS record type should be used to connect the domain to the given IP, and why?

## Answer

1. DNS (Domain Name System) is a feature in web technology which is used to convert an IP address of a website into a human readable link (vice-versa). Example, Google link is technically in octect form (considering IPv4) like 142.xx.xx.xx (Public IP address) which is hard to memorize of even use it (Dynamic IP), so DNS is responsible to have this IP address as a human readable link as : "www.google.com"
2. Since epicreads.com is an IPv4 address, 'A' record is used for DNS. 

 ---

# 💻 Task 5: Visual Studio Code Setup (Hands-on)

## Your Task

Install Visual Studio Code (if not already installed).

Take a screenshot of your VS Code environment showing:

* Terminal open inside VS Code
* Running a basic command:

### Windows

```powershell
dir
```

### Linux / macOS

```bash
pwd
ls
```

* Your selected VS Code theme clearly visible

⚠️ **Important:** The screenshot must show your username or another identifiable detail to confirm it is your environment.

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![VS Code Setup Screenshot](screenshots/vs-code.png)


Replace `task-5-vscode.png` with your actual screenshot file name.

---

# 🔗 Task 6: Publish Your Assignment as a LinkedIn Post

## Objective

Publishing on LinkedIn helps you:

* Build your professional online presence
* Reinforce your learning
* Document your DevOps journey publicly

## Your Task

Summarize your answers from Tasks 1–5 into a LinkedIn post.

Clearly structure your post into the following sections:

* ChatGPT
* Internet & Networking
* App Architecture
* DNS
* VS Code Setup

Use the credit note that matches your track:

Add the following credit note at the end of your post **(If you are DMI Cohort 3 student)**:

> **P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=cohort3**


Add the following credit note at the end of your post **(If you are DMI Self-paced track student)**:

> **P.S. This post is part of the DevOps Micro Internship (DMI) — Self-Paced Engineer Track — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=self-paced**

Add the following credit note at the end of your post **(If you are DMI Campus student)**:

> **P.S. This post is part of the DevOps Micro Internship (DMI) — Campus — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=campus**

Replace `YOUR-GITHUB-USERNAME` with your GitHub username — that link is your public DMI progress page (your graded badge page).
---

## LinkedIn Post URL

Paste your LinkedIn post URL here:

```text
https://lnkd.in/p/gtWQ2JQv
```

---

## LinkedIn Post Backup Copy

Paste the full text of your LinkedIn post here:

Add your post content here...

```text
✅Completed Tasks of Week 00 - Internet and Networking, of the DevOps Micro Internship.

This week was mainly about understanding the basics that are needed before getting into the actual DevOps tools and workflows.

𝗖𝗵𝗮𝘁𝗚𝗣𝗧
Learned how to use ChatGPT effectively for understanding technical concepts, breaking down problems, and improving my learning process.

𝗜𝗻𝘁𝗲𝗿𝗻𝗲𝘁 & 𝗡𝗲𝘁𝘄𝗼𝗿𝗸𝗶𝗻𝗴
Worked through the basics of how devices communicate over the Internet, including IP addresses, ports, NAT, routers, and how a request reaches a server.

𝗔𝗽𝗽𝗹𝗶𝗰𝗮𝘁𝗶𝗼𝗻 𝗔𝗿𝗰𝗵𝗶𝘁𝗲𝗰𝘁𝘂𝗿𝗲
Learned the basic structure of an application and how the frontend, backend, APIs, and database communicate with each other.

𝗗𝗡𝗦
Learned how DNS works and how a domain name gets resolved to an IP address when accessing a website.

𝗩𝗦 𝗖𝗼𝗱𝗲 𝗦𝗲𝘁𝘂𝗽
Set up my development environment in VS Code and got the basic project structure and tools ready for the upcoming tasks.

I've also attached some of the diagrams and screenshots from my Week 00 work as evidence of what I completed.
Looking forward to continuing with the next set of tasks and getting more hands-on with DevOps!.

P.S. This post is part of the DevOps Micro Internship (DMI) — Self-Paced Engineer Track — by Pravin Mishra. My graded progress is public: https://lnkd.in/gKVaVndW · Start your DevOps journey: https://lnkd.in/gSRqreJg

hashtag#DMIByPravinMishra
```

---

# Reflection – Week 0

### What did you find easy?

I found setting up vs-code and using the terminal easy as I already possess some knowledge about it.

---

### What was difficult?

Using draw.io for drawing diagrams was new and a little bit time-consuming.

---

### What will you improve next week?

I will improve the prompt writing skills for obtaining efficient and effective results aligning to the requirements.

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.


## 📌 Resources

- 🌐 **DMI Official Website:** https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 **University:** https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 **Discord Community:** https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 **Blog:** https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ **YouTube Playlist (DMI Cohort 3):** https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 **Pravin Mishra (LinkedIn):** https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 **CloudAdvisory (LinkedIn):** https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track*
