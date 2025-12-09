---

````markdown
# SOARIX WORKSPACE – MASTER DESIGN DOCUMENT (FULL CHAT CONSOLIDATION)

A single consolidated Markdown file summarizing the full conversation and containing all artifacts created so far (requirements, architecture, UI wireframe, model stack).  
This represents the **MVP blueprint** and the first steps of the build process.

---

# 0. PROJECT PURPOSE

Soarix Workspace is a **local-first AI Operating System** designed to act as a **factory** where the user can build *anything*:

- Full-stack apps, SaaS, websites, mobile apps, games  
- AI agents, plugins, MCP tools, automations  
- Books, blogs, scripts, courses, marketing, social content  
- Images, infographics, prompts, videos, thumbnails  
- Workflows through n8n, Zapier, custom tools  
- UI/UX design generation  
- Everything from a *ChatGPT-like simple interface*, but **private and offline-first**.

Workspace must support:

- Local models (AMD GPU optimized)
- Online models (Gemini 3 Pro, ChatGPT 5.1)
- Agents + tools + automations
- File/folder-based project structure
- Clean, elegant, emotional UI/UX

---

# 1. LOCAL & ONLINE MODEL STACK (FINALIZED)

## 1.1 Offline Models (local-first)

| Model | Purpose |
|-------|---------|
| **Kimi K2** | Long-form writing, polished prose, structured documents |
| **Kimi K1.5** | Fast drafting, rough outlines |
| **DR-Tulu** | Deep reasoning, research, planning, system design |
| **OLMo 3 Base** | Very fast general use |
| **OLMo 3 Reasoning** | Lightweight reasoning |
| **Qwen 3 7B** | Fast coding + general chat |
| **Qwen 3 14B** | Strong reasoning + creativity |
| **Qwen 3 32B** | “Offline GPT-4-Lite”, highest reasoning locally |
| **Minimax M2 / GLM 4.6** | Excellent coding/debug assistant |
| **Qwen 3 VL** | Vision model for reading images & PDFs |

## 1.2 Online Models

| Provider | Use |
|----------|-----|
| **Gemini 3 Pro** | Reasoning, planning, coding |
| **ChatGPT 5.1** | Expert-level reasoning, coding |
| **Claude-like offline models (equivalents)** | For creative reasoning, content |
| (Future optional: Qwen/QwRn/Claude integrations) |

Local execution frameworks (Windows + AMD 7800XT supported):

- **LM Studio (DirectML)**
- **Ollama for Windows (DirectML)**
- **VLLM DirectML**
- **KoboldCPP HIP/Vulkan**

---

# 2. MVP REQUIREMENTS  
*(File: `/requirements/workspace-mvp-requirements-v1.md`)*

```markdown
# Soarix Workspace – MVP Requirements (v1)

## 1. Purpose
Create a local-first AI OS that builds anything via prompts:
- Content (blogs, videos, books)
- Apps (websites, SaaS, AI apps)
- Agents (Architect, Content, Code)
- Automations (n8n, Zapier, MCP tools)
- Everything saved as artifacts in a project file tree.

## 2. MVP Must-Haves
1. Project system  
2. Chat-centered interface  
3. Artifact file system  
4. Model selector (local + online)  
5. Basic agents (Architect, Content, Code)  
6. Simple orchestration  
7. Local storage  
8. Sidebar navigation  
9. System prompts & personas  
10. Files/Tasks/Chat tabs

## 3. Model Integration
(Local models + online models — as listed above)

## 4. Agents
- Architect Agent  
- Content Agent  
- Coding Agent  

Each has:
- System prompt  
- Default model  
- Triggered via UI or planner

## 5. Storage
Local filesystem + SQLite DB.

## 6. Non-Goals for MVP
- Full automations builder  
- Multi-user  
- Cloud deployment  
- Advanced autonomous agents  

## 7. Future Extensions
- Auto-model routing  
- Visual workflow editor  
- Real-time UI preview  
- Deployment assistant  
````

---

# 3. SYSTEM ARCHITECTURE BLUEPRINT

*(File: `/architecture/system-architecture-v1.md`)*

```markdown
# Soarix Workspace – System Architecture Blueprint (v1)

## 1. Concept
A local-first AI Workspace with:
- ChatGPT-like UI  
- Project-based artifact system  
- Multi-model routing  
- Agents + Tools via Orchestrator  

## 2. Architecture Layers

UI (Tauri + React)
↓
Orchestrator Engine
↓
Model Router (local/online)
↓
Model Execution Layer:
  - LM Studio, Ollama-DML, VLLM-DML
  - Gemini 3 Pro, ChatGPT 5.1
↓
Tools/MCP/Automations
↓
Storage (Filesystem + SQLite)

## 3. Project Structure

/project-name
  /requirements
  /architecture
  /backend
  /frontend
  /agents-and-tools
  /ui-ux
  /automation
  /deployment
  /content
  workspace.json

## 4. Prompt → Artifact Flow

User Prompt  
→ Orchestrator  
→ Agent Plan  
→ Model Router  
→ Model Execution  
→ Artifact Generator  
→ Save to project  
→ UI displays file  

## 5. AMD 7800XT Integration
Local models run via:
- DirectML  
- LM Studio  
- Ollama (DirectML)  
- VLLM DirectML  

Memory:
- 7B = instant  
- 14B = smooth  
- 32B = quantized (4–6bit)  

## 6. Online Providers
- Gemini 3 Pro  
- ChatGPT 5.1  
- Claude-equivalent offline options  

## 7. Expandability
- Multi-agent graph  
- Visual workflow builder  
- Deployment pipelines  
```

---

# 4. UI / UX WIREFRAME

*(File: `/ui-ux/workspace-ui-wireframe-v1.md`)*

```markdown
# Soarix Workspace – UI Wireframe (v1)

## Layout

---------------------------------------------------------
| Sidebar |               Center Area                   |
|         |---------------------------------------------|
|         | Tabs: Chat | Tasks | Files | Build | ...    |
|         |---------------------------------------------|
|         | Chat / Files / Tasks Surface                |
---------------------------------------------------------
| Right Panel: Project Brief | Goals | Model | Agents   |
---------------------------------------------------------

## Sidebar Sections
- Projects
- Agents
- Plugins / MCP tools
- Automations
- Templates
- System Prompts
- + New Project
- + New Agent

## Center Tabs
- Chat (main)
- Tasks
- Files (artifact explorer)
- Build (pipeline)
- Content
- Agents
- Whiteboard

## Right Panel
- Project Brief  
- Goals  
- Active Model  
- Active Agent  
- System Prompt  
- Status updates  

## Emotional Design
- Calm, elegant, minimal  
- Feels like a futuristic studio  
- Microcopy examples:
  - “Describe what you want to create.”
  - “Your factory is listening.”  
```

---

# 5. SYSTEM SETUP – FIRST USER STEPS

These steps are tailored to your machine:

* **Windows OS**
* **AMD 7800XT GPU**
* **AMD 7800X3D CPU**
* **32GB RAM**

## Step 1 — Install Node.js (LTS)

*(You completed this.)*

## Step 2 — Will follow after next instruction

(Each will be one tiny actionable step.)

---

# 6. CURRENT STATUS (END OF CHAT SUMMARY)

You now have:

* MVP requirements
* System architecture
* UI wireframe skeleton
* Hardware-aware model plan
* Clear next steps for installation
* The foundation for building the actual Soarix Workspace app

Next action (after this doc):
We proceed to **System Step 2**:
Install Tauri prerequisites (Rust) in one tiny step.





