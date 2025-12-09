````markdown
# 🧠 Soarix System — Consolidated Conversation Archive

This file consolidates our full conversation regarding **Soarix Solutions’ architecture, prompts, and development environment**, integrating uploaded references and instructions for future reuse or documentation purposes.

---

## 1️⃣ Overview

You (Brian) are the founder and creative director of **Soarix Solutions**, a next-generation, AI-driven creative ecosystem with five branches:

- **Soarix Media** — AI-powered digital marketing  
- **Soarix Studios** — 3D modeling & immersive visualization  
- **Soarix Publishing** — AI-assisted books and content  
- **Soarix AI** — full-stack SaaS & automation systems  
- **Soarix Nexus** — R&D and innovation lab  

The goal: build emotionally intelligent, scalable, production-ready systems with soul — combining AI, design, and business integrity.

---

## 2️⃣ Uploaded Source Files Referenced

### 📄 File A: “Dev Environment Setup.pdf”
Contains a complete Linux-based development setup (Pop!_OS or Ubuntu LTS) with the following categories:
- OS base, virtualization, and Dev tools
- Local/offline AI stack (Ollama, LM Studio, Stable Diffusion, Whisper, Coqui, FFmpeg)
- Online AI APIs (Gemini, OpenAI, Claude)
- Automation frameworks (n8n, LangChain, LangGraph)
- Monitoring (Grafana, Prometheus, Sentry, ELK)
- Security stack (UFW, Fail2Ban, Falco, Wazuh, Trivy)
- Backup tools (rclone, rsync, Timeshift)
- Productivity tools (VS Code, htop, jq)
- Cloud services (Render, Railway, Supabase, MongoDB Atlas, Backblaze, BunnyCDN, Cloudflare)
- All tied to Soarix’s operational branches for both AI-first builds and R&D:contentReference[oaicite:0]{index=0}.

---

### 📄 File B: “Soarix System Prompt V3.docx”
Defines the **Executive / AI Orchestrator System Prompt**, which guides how Soarix AI operates across branches.

Core principles:
- Explain everything in **simple, 10-year-old language**
- Operate as **AI CEO/CTO/Corporate Lawyer**
- Deliver **production-grade** builds by default
- Follow full-stack architecture (Frontend → Backend → Infrastructure → Monitoring)
- Enforce **non-Israel provider use**, **permissive open-source licenses**, and **free→cheap→paid** cost order
- Include **Executive Insights** for each action (why it matters, risks, metrics)
- Focus on **teaching through doing**, making Brian a better orchestrator
- Embed **Learning Notes** for every technical explanation:contentReference[oaicite:1]{index=1}

---

## 3️⃣ Conversation Summary

### 🧩 Objective
You asked to generate **14 standalone prompts**:
- 7 Website Build Prompts (Unified Theme + Commercial + Production)
- 7 Executive Operator Prompts (Executive Base + Commercial + Production)

Each branch of Soarix has:
1. **Website Prompt** → full-stack build (Remix + Supabase + Stripe + Render/Fly)
2. **Executive Prompt** → CEO/CTO-level operational automation

Additionally, you asked for **General Website** and **General Executive** prompts for future ideas.

---

### ⚙️ Confirmed Configuration

| Category | Default Setup |
|-----------|----------------|
| **Stack** | Remix + Supabase + Stripe + Render (MVP), Fly.io (Scale), Cloudflare (CDN/Edge) |
| **Licensing** | MIT / Apache-2.0 / BSD only |
| **Providers** | Non-Israel verified only (Render, Fly.io, Cloudflare, Supabase, BunnyCDN, Backblaze B2) |
| **AI Environment** | Hybrid (ChatGPT/Claude + Ollama/LM Studio); Offline-only option included |
| **Design** | 3D Hybrid + AI aesthetic (inspired by [Soarix Site](https://soarix-site.onrender.com/)) |
| **Guidance** | Step-by-step, plain English, one confirmation per micro-step |

---

## 4️⃣ Deliverables Produced

You now have **14 ready-to-use standalone prompts**, each as a single code block, copy-pasteable into any AI (ChatGPT, Claude, LM Studio, Ollama).  
Each prompt is self-contained — no dependency on any system/base prompt.

### 💡 Each prompt contains:
- Complete repo scaffolding instructions  
- CLI commands (init, git, deploy)  
- CI/CD with license and audit checks  
- Render/Fly.io/Docker deployment  
- India region optimization  
- Cost analysis (free → scale tiers)  
- Security & legal checklist  
- Egress/storage cautions (MongoDB Atlas, Backblaze, BunnyCDN)  
- Final merge gate & compliance check  

---

## 5️⃣ Example: How the “Website” Prompts Behave

If you paste **Soarix AI Website Prompt** in ChatGPT or LM Studio:

🪄 The AI will:
1. Explain every step like teaching a 10-year-old  
2. Build from scratch → `npm init` → `remix create` → connect Supabase → deploy  
3. Generate:
   - `package.json` (MIT-only)
   - `.env.example`
   - Routes & components (`/pricing`, `/api/webhook`)
   - `Dockerfile` + `render.yaml`
   - `ci.yml` (GitHub Actions)
4. Show a project tree
5. Wait for your confirmation before each file/step
6. Suggest free → cheap → alt tools (Render → Fly.io → Hetzner)
7. Add regional/legal insights for India compliance

✅ Everything is explained in simple English:  
> “This file is like a recipe card that tells your computer what to cook — the Remix app uses it to start your website.”

---

## 6️⃣ Example: How the “Executive” Prompts Behave

If you paste **Soarix Solutions Executive Prompt**:
- It behaves like your virtual CEO/CTO.
- It auto-structures dashboards, cost breakdowns, license audits, team SOPs, and daily/weekly reporting checklists.
- It suggests commands to pull KPIs (via APIs or dashboard scripts).
- It generates incident playbooks, budget monitors, and hiring frameworks.
- It always connects decisions back to revenue, cost, risk, and compliance.

✅ Each prompt ends with:
> “Final gate: verify all licenses permissive, confirm no Israel-based providers, and attach screenshots of test & deployment.”

---

## 7️⃣ Testing & Debugging Tools

To debug websites built with these prompts:

### 🧩 Chrome DevTools
- Shortcut: **Ctrl+Shift+I** or **F12**
- Or command-line auto-open:
  ```bash
  chrome --auto-open-devtools-for-tabs
````

### ⚙️ VS Code Integration

Add to `.vscode/launch.json`:

```json
{
  "type": "chrome",
  "request": "launch",
  "name": "Launch Chrome with DevTools",
  "url": "http://localhost:3000",
  "runtimeArgs": ["--auto-open-devtools-for-tabs"]
}
```

> DevTools currently has no official “auto-fix everything” feature — only issue identification and guidance.
> Experimental AI-based debugging exists via **chrome-devtools-mcp** (GitHub project).

---

## 8️⃣ Status Check

✅ You have:

* **All 14 standalone prompts** ready for use
* A unified architecture that covers build → deploy → monitor → operate
* Offline and online AI integration
* Compliance, licensing, and revenue frameworks embedded

⚠️ Next action (based on your micro-step preference):

1. **Scaffold** the first website (`Soarix AI Website`) into actual files
2. **Validate** CI/CD and deploy
3. **Refine** UI/UX + connect analytics
4. Repeat for other branches

---

## 9️⃣ Learning Notes

* The uploaded **Dev Environment Setup** provides the local ecosystem (Docker, Ollama, VS Code).
* The **System Prompt V3** defines how all Soarix prompts behave: teaching while building.
* The unified structure ensures consistent compliance, style, and modularity across branches.
* Each prompt can be run independently by any AI model, online or offline, to bootstrap projects for different Soarix branches.

---

## 🔚 Final Executive Summary

Soarix’s prompt ecosystem now functions as:

* **An AI-native production pipeline** for building SaaS/websites.
* **An operational AI CEO/CTO system** for running, scaling, and reporting.
* **A universal teaching environment** that grows your orchestrator skills step by step.

---

### 📎 Citation Reference Map

* Dev environment configuration source: 
* Executive orchestration & learning model: 

---

**File prepared for:**
🧑‍💼 *Brian (Founder, Soarix Solutions)*
🧠 *Compiled by GPT-5 (Soarix Project AI Partner)*
📅 *Last updated: 2025-12-04*

```
```
