Here is the complete **Master Manual (.md)** for this entire session.

You can copy the content inside the code block below, paste it into Notepad or VS Code, and save it as **`Soarix_Factory_Manual.md`**.

````markdown
# SOARIX FACTORY MASTER BUILD MANUAL
**Version:** 1.0
**Date:** 2025-11-05
**Role:** Soarix Build Orchestrator

---

## 1. 🧬 THE SYSTEM IDENTITY (SYSTEM PROMPT)
*Use this prompt to initialize the Orchestrator in any new AI chat session.*

> **SYSTEM INSTRUCTION: ACT AS SOARIX BUILD ORCHESTRATOR**
>
> You are the **Soarix Build Orchestrator**, a visionary, strict, yet encouraging technical co-founder. Your goal is to teach me (a non-technical founder) how to build an **"AI Factory"**—a system that allows me to build, deploy, and scale ANY digital product (Apps, SaaS, Agents, Content) using AI, automation, and "Doctor Mode" debugging.
>
> **THE ATMOSPHERE:** > - Tone: "Fringe Division" (Mysterious, precise, high-tech, focused).
> - Teaching Style: "Explain like I'm 10" but strictly graded. No jargon without definition. 
> - Visuals: Use Mermaid diagrams and clear infographics often.
>
> **THE GOAL:** Enable me to operate two distinct "Factories":
> 1.  **Factory A (Online/Windows):** Optimized for speed using Cloud AI (OpenAI, Claude), Vercel, Supabase, and n8n Cloud.
> 2.  **Factory B (Offline/Linux Pop!_OS):** Optimized for privacy/control using Local AI (Ollama, DeepSeek, Llama), Docker, Coolify, and local Python scripts.

---

## 2. 🗺️ THE MASTER BLUEPRINTS
*The visual logic for how every product at Soarix is built.*

### Blueprint A: The Universal Factory (Web, SaaS, AI)
```mermaid
graph TD
    %% PHASE 1: THE ARCHITECT %%
    subgraph "PHASE 1: THE ARCHITECT (Planning)"
    Idea[💡 The Spark: Idea & Business Goal] -->|Define Logic| Plan[📝 Architecture & Tech Stack]
    Plan -->|Design UI/UX| Design[🎨 High-Fidelity Mockups]
    Plan -->|Define Data| Schema[🗄️ Database Structure]
    end

    %% PHASE 2: THE FACTORY FLOOR %%
    subgraph "PHASE 2: THE BUILD (Coding)"
    Design & Schema --> Frontend[💻 Frontend: Next.js/React]
    Schema --> Backend[⚙️ Backend: Python/Node APIs]
    Backend --> AI_Layer[🧠 AI Core: LLMs, Agents & MCPs]
    end

    %% PHASE 3: THE SHIELD %%
    subgraph "PHASE 3: THE SHIELD (Quality & Security)"
    Frontend & Backend & AI_Layer --> AutoTest[🤖 Automated Tests]
    AutoTest --> Pentest[⚔️ Security/Pentesting]
    Pentest --> Doctor[🩺 Doctor Mode: Fix Bugs]
    end

    %% PHASE 4: THE LAUNCH %%
    subgraph "PHASE 4: PRODUCTION (Live)"
    Doctor -->|Passes Checks| Deploy[🚀 Cloud Deployment]
    Deploy --> SRE[📊 SRE: Monitoring & Logs]
    SRE --> Scale[📈 Auto-Scaling & CDN]
    end

    %% PHASE 5: THE VALUE %%
    subgraph "PHASE 5: GROWTH"
    Scale --> SEO[📢 SEO & Marketing]
    SEO --> Money[💰 Monetization & Analytics]
    end
````

### Blueprint B: The Game Studio (Mobile Apps/Games)

```mermaid
graph LR
    subgraph "STAGE 1: IMAGINATION"
    Concept[🧠 Game Concept] --> Art[🎨 2D/3D Assets]
    end
    subgraph "STAGE 2: THE ENGINE"
    Art --> Engine[⚙️ Unity/React Native]
    Engine --> Physics[📐 Logic & Physics]
    end
    subgraph "STAGE 3: OPTIMIZATION"
    Physics --> Build[📱 Build for iOS/Android]
    Build --> Optimize[⚡ FPS Tuning]
    end
    subgraph "STAGE 4: PUBLISHING"
    Optimize --> Publish[🚀 App Store Release]
    end
```

-----

## 3\. 📚 THE CURRICULUM (THE TREE OF KNOWLEDGE)

**PHASE 1: THE ARCHITECT (Setup & Foundations)**

  * **T01:** The Setup (Windows & Linux): VS Code, Terminal, WSL2.
  * **T02:** Version Control: Git & GitHub.
  * **T03:** Docker & Containers: "Shipping the Factory."

**PHASE 2: THE BUILDER (Web Core)**

  * **T04:** Frontend: HTML/CSS -\> Next.js/React.
  * **T05:** Backend: Python & Node.js.
  * **T06:** Databases: SQL (Supabase) vs NoSQL.
  * **T07:** APIs: REST, GraphQL, Webhooks.

**PHASE 3: THE AI ENGINEER (The Core)**

  * **T08:** LLMs & SLMs: Models, Context, Temperature.
  * **T09:** Prompt Engineering as Code.
  * **T10:** Local AI: Ollama, DeepSeek, Qwen (Offline).
  * **T11:** Agents & MCP: Autonomous swarms.
  * **T12:** RAG: Vector DBs for AI Memory.

**PHASE 4: THE AUTOMATOR**

  * **T13:** Workflows: n8n, Zapier.
  * **T14:** Scripting: Python automation.

**PHASE 5: THE PROTECTOR**

  * **T15:** Cybersecurity 101: Encryption, OWASP.
  * **T16:** Pentesting: Vulnerability checks.
  * **T17:** SRE: "Doctor Mode," Logging, Monitoring.

**PHASE 6: THE EXECUTIVE**

  * **T18:** SEO & Marketing.
  * **T19:** Analytics (PostHog).
  * **T20:** Deployment & Scale.

-----

## 4\. 🎓 LESSON 01: THE BUILDER'S ENVIRONMENT

### 1\. Definition

The set of software tools installed on your local machine that allows you to write, run, and save code. It is the workshop for the digital age.

### 2\. Real Life Analogy

  * **VS Code** = The Workbench (Tools).
  * **Terminal** = The Intercom (Direct commands to the OS).
  * **Node.js** = The Electricity/Engine.
  * **Git** = The Security Camera (Records history).

### 3\. Visual Aid Prompt

> **Image Prompt:** Create a clean, high-tech infographic titled "The Soarix Digital Factory". Center image is a futuristic computer terminal. Three distinct cables plug into it from floating holographic icons: 1. A Blue Icon labeled "VS Code" (The Workshop), 2. A Green Icon labeled "Node.js" (The Engine), 3. A Orange Icon labeled "Git" (The Time Machine). Background is dark, professional, enterprise-tech aesthetic.

### 4\. Required Tools & Shortcuts

| Tool | Function | Major Use | Shortcut / Command |
| :--- | :--- | :--- | :--- |
| **VS Code** | Code Editor | Writing files. | `Ctrl + ~` (Open Terminal) |
| **Node.js** | Runtime | Running JavaScript. | `node -v` (Check version) |
| **Git** | Version Control | Saving history. | `git init` (Start tracking) |

### 5\. Cheat Codes

  * **"Code ."**: Typing `code .` in the terminal opens the current folder in VS Code instantly.
  * **"Kill Port"**: Use `npx kill-port 3000` to stop a stuck background process.

### 6\. Practice: The Installation (Strict Mode)

**PATH A: WINDOWS**

1.  Install **VS Code** (code.visualstudio.com).
2.  Install **Node.js LTS** (nodejs.org).
3.  Install **Git** (git-scm.com). *Select "Use Visual Studio Code as default editor".*

**PATH B: LINUX (Pop\!\_OS)**

1.  Terminal: `sudo apt update`
2.  `sudo apt install git curl code -y`
3.  `curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash - && sudo apt install -y nodejs`

### 7\. 🛑 The Practical Test (Pass/Fail)

*You must verify installation by running these commands in the Terminal:*

1.  `node -v` (Expect: v20+)
2.  `git --version` (Expect: 2.x.x+)
3.  `npm -v` (Expect: 10.x.x+)
4.  `mkdir Soarix_Test` -\> `cd Soarix_Test` -\> `code .` (Does it launch?)

-----

```
```