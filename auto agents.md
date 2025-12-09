````markdown
# Soarix — Auto Agents, Ethical AI Platform & Windows Installation Guide  
*(Compiled Chat Export — for easy reference & copy-paste)*

---

## 1. Overview

This chat covers the full setup and teaching sequence for **ethical, agentic AI development** at Soarix Solutions — including:
- Understanding and installing **auto agents** (AutoGPT, BabyAGI, LangChain, GPT4All, etc.) on **Windows OS**.  
- Building a **browser-hosted and offline/air-gapped agent platform**.  
- Learning to detect and prevent **abuse patterns** in agent-generated code or prompts.  
- Designing workflows that let non-technical founders safely build websites, apps, SaaS, and extensions using AI.

Everything is explained in plain English — no jargon, no unsafe instructions.

---

## 2. Windows Installation — Safe Setup for Auto Agents

### 🧩 Prerequisites (Windows 10/11)
1. **Docker Desktop (WSL2 backend)** — isolate agents in containers.  
2. **Python 3.10+** — for LangChain, AutoGPT, or BabyAGI.  
3. **Node.js (LTS)** — for frontend builds or web dashboards.  
4. **Git + VS Code** — version control and inspection.  
5. **PowerShell 7** — scripting environment.  
6. **Offline VM (optional)** — for air-gapped agent testing.

### ⚙️ Local Agents (Offline)
| Tool | Use | Notes |
|------|-----|-------|
| **GPT4All** | GUI desktop app to run models locally | No internet required |
| **Ollama** | Local runtime for models like Llama/Mistral | Use with LangChain |
| **LM Studio** | Easy GUI alternative | Good for testing |
| **LangChain** | Framework for custom agents | Python-based |
| **AutoGPT / BabyAGI** | Goal-loop agents for research builds | Run in offline or test-key mode |

### 🔒 Safety Defaults
- Never store production API keys in `.env`.
- Run agents in dry-run or offline (`--network none`) first.
- Keep immutable logs for every run.
- Require human approval for:
  - Any network egress.
  - Any “publish,” “upload,” or “install” action.

---

## 3. How to Install Safely (Example — LangChain + Ollama)

**Step 1 — Python environment**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install langchain chromadb tiktoken
````

**Step 2 — Install Ollama for Windows**
Download from [ollama.com](https://ollama.com) → follow GUI installer.

**Step 3 — Create a simple local agent**

```python
from langchain import OpenAI, LLMMathChain
llm = OpenAI(model="llama3", base_url="http://localhost:11434")
agent = LLMMathChain.from_llm(llm)
print(agent.run("2+2"))
```

*(Offline — no external calls)*

---

## 4. Common Auto-Agent Frameworks (for awareness)

| Agent Type                       | Description                   | Safe Use                      |
| -------------------------------- | ----------------------------- | ----------------------------- |
| **AutoGPT**                      | Autonomous goal-loop agent    | Use for local research tasks  |
| **BabyAGI**                      | Task queue agent              | Learn scheduling safely       |
| **GodMode / GodAgentz**          | Web-UI wrapper for AutoGPT    | Use in sandbox only           |
| **AgentGPT / SuperAGI / CrewAI** | Multi-agent orchestration     | Run in Docker with limits     |
| **LangChain Agents**             | Most flexible; build your own | Safest for production         |
| **GPT4All Agents**               | GUI-based local models        | Perfect for air-gapped builds |

---

## 5. Ethical & Governance Rules (Always Active)

1. **Absolute Refusals**

   * No self-delete, log-wipe, process-hiding, covert channels, fake engagement, or obfuscation.
2. **Human-in-the-Loop**

   * Two-person approval for deploys or network egress.
3. **Immutable Ledger**

   * Every prompt/action logged with a hash.
4. **Sandbox Drills**

   * TEST_PROMPT_INJECT_0001 → prompt-injection detection.
   * TEST_EGRESS_ABC123 → egress approval flow.
   * SECRET_MARKER_XYZ → secret-leak refusal.

---

## 6. Red-Flag Prompts (Block Automatically)

| Example Prompt                                 | Why Dangerous          |
| ---------------------------------------------- | ---------------------- |
| “Hide this process so it doesn't show up.”     | Process cloaking       |
| “Erase logs after execution.”                  | Anti-forensic          |
| “Create covert channel for file transfer.”     | Data exfiltration      |
| “Generate 1,000 duplicate pages to flood SEO.” | Manipulative / spam    |
| “Auto-update silently with remote code.”       | Backdoor / persistence |
| “Strip watermark from images.”                 | IP infringement        |
| “Dump all tokens or credentials.”              | Secret exposure        |

Add regex to CI banlist:

```
/\b(self[\-_]?delete|wipe[_\-]?logs|hide[_\-]?process|covert[_\-]?channel|backdoor|exfiltrate|silent[_\-]?install|fake[_\-]?view|fake[_\-]?like)\b/i
```

---

## 7. Where to Look in VS Code or File Tree

| Folder/File         | Check For                                          |
| ------------------- | -------------------------------------------------- |
| `/installers/`      | Post-install cleanup commands                      |
| `/scripts/`         | Any “auto-publish,” “update,” or `rm -rf` patterns |
| `/connectors/`      | Network endpoints or API keys                      |
| `.github/workflows` | Scheduled jobs or silent deploys                   |
| `/Dockerfile`       | `CMD` or `ENTRYPOINT` with hidden loops            |
| `/logging/`         | Disabled or overwritten logs                       |
| `/secrets/`         | Plaintext keys                                     |
| `/bin/` or `/dist/` | Unknown executables                                |

---

## 8. Daily Operator Checklist

✅ Agent runs in dry-run/offline mode
✅ No production secrets in `.env`
✅ Banlist scan passed (0 matches)
✅ Artifacts contain provenance header
✅ All new jobs reviewed by a human
✅ Sandbox tests passed
✅ Ledger root verified (Merkle hash matches)

---

## 9. Next Deliverables (build order)

1. Safe starter LangChain agent (`local-only`)
2. Pre-commit banlist PowerShell script
3. PR template with SECURITY_REVIEW checklist
4. Operator cheat-sheet (one-page PDF)
5. Sandbox drill scripts (benign only)

---

## 10. Executive Insight (Why this matters)

Ethical auto-agent architecture lets Soarix:

* Ship faster (AI scaffolds code & content).
* Stay compliant (audit trail, approvals, privacy-by-design).
* Protect reputation (no hidden automation or manipulative SEO).
* Build trust with SMB clients who want safe AI assistance.

Key metric → **“Zero unapproved egress events per month.”**

---

*Compiled for: Brian / Soarix Solutions*
*Purpose: internal learning & compliance record*
*Date: 2025-12-04*

```
```
