Here’s your complete chat preserved in a single `.md` file format — you can copy everything inside the code block and save it as `Soarix_OpenCode_Tutor_Session.md` on your system:

````markdown
# Soarix Interactive Tutor — OpenCode, Roo Code & GitHub Desktop Setup  
**Date:** 2025-12-04  
**Session Type:** Interactive Hands-on Tutoring  
**User:** Brian (Founder, Soarix Solutions)  
**AI Role:** Virtual CTO / Tutor  

---

## 🧭 Conversation Summary

This session sets up **OpenCode**, **Roo Code (VS Code extension)**, and **GitHub Desktop** on **Windows OS**.  
Goal: Learn both GUI and terminal (PowerShell/TUI) workflows.

---

## Step 0 — Initial Setup

**ChatGPT:**  
Which OS are you using (Windows / macOS / Linux) and do you prefer GUI or terminal-first?

**User:**  
Windows OS

**ChatGPT:**  
Got it 👍 — Windows OS.  
Now, do you prefer **GUI-first** instructions (clicks, installers) or **terminal-first** (PowerShell / Chocolatey commands)?

**User:**  
Ok I would prefer GUI but I still need to know how TUI works

**ChatGPT:**  
Perfect ✅ — we’ll do **GUI-first** steps, but I’ll also show you the matching **PowerShell/Chocolatey (TUI/terminal)** commands so you can practice both.  
We’ll start with **OpenCode** first (then Roo Code, then GitHub Desktop).  

---

## Step 1 — OpenCode Overview

**What it does:**  
OpenCode is an open-source desktop app for running and testing AI coding agents locally — like an offline Copilot for building and testing AI workflows.  
Use it when you want to **experiment with AI code generation locally** instead of cloud IDEs.

---

## Step 2 — Install OpenCode (Windows)

### GUI method (recommended):
1. Go to 👉 [https://opencode.so](https://opencode.so)  
2. → Click **Download** → choose **Windows (.exe installer)**  
3. → Run the installer → click **Next → Install → Finish**

### Terminal (PowerShell / Chocolatey alternative):
```powershell
choco install opencode -y
````

---

**ChatGPT:**
Reply **"DONE"** when you’ve completed installation (or **"SKIP"** if you want to move on).
Would you like me to include the **config step** next, or do you want to test the install first?

---

## Uploaded References

### 1. dev environment setup.pdf

Contains detailed baseline for development tools, including Docker, Node, Python, LangChain, Supabase, etc. — foundational to Soarix AI architecture.

### 2. Soarix System Prompt V3.docx

Defines Soarix’s executive AI orchestrator role, communication style, compliance, and architecture-first principles for all builds.

---

## Files Mentioned

* **`dev environment setup.pdf`** — environment preparation & categorized software for AI development.
* **`Soarix System Prompt V3.docx`** — defines AI orchestration workflow and build standards.

---

## Notes

**Learning Tip:**
Always test GUI installs first to get comfortable, then practice the terminal version.
Never paste API keys or tokens into chats. Store them in environment variables:

```powershell
setx OPENAI_API_KEY "YOUR_API_KEY_HERE"
```

Then restart PowerShell to apply changes.

---

## Next Steps

Once you reply **DONE**, the next sections will cover:

1. Post-install configuration
2. Running first test in OpenCode
3. 5 short practice tasks
4. One combined exercise using Git
5. Final checklist export for Windows

---

*End of current session log.*

```

Would you like me to **append Roo Code and GitHub Desktop sections** to the same `.md` file once we finish their walkthroughs — or keep each tool’s setup in a **separate markdown file** for easier tracking?
```
