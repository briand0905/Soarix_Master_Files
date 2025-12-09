# Soarix Automation Factory — Conversation Archive (Option A)

**Date Exported:** 2025-12-04  
**Format:** Markdown (.md)  
**Scope:** This conversation thread only  

---

## USER →  
MASTER TASK: Build a complete Soarix Automation Factory (n8n + AI)

I want you to act as my step-by-step builder and teacher. I will not build the factory manually — you will produce everything I need to paste into Synta so Synta builds the full automation factory, which I will export as JSON and run in my own n8n + AI stack (online or offline). 

Do this in five phases. After each phase, STOP and ask me to confirm before moving to the next phase.

PHASE 1 — Tools & Inventory (finalize with me)
• Produce a final, simple list of all tools, APIs, webhooks, and AI options we need for Soarix’s five branches: Media, Studios, Publishing, AI, Nexus.
• For each item list: name, purpose (one sentence), auth type (OAuth/API key/local endpoint), webhook needed? (yes/no).
• Provide a short recommendation: “must-have” or “optional” for Soarix scale.
• Wait for my confirmation to lock the list.

PHASE 2 — Factory plan & steps
• Give me a clear step-by-step plan (simple English) to build the factory (n8n + AI): staging vs production, hosting, webhooks, secrets, offline AI hosting, monitoring, approval flows, and templates storage.
• For each step include estimated one-line result (what I will have after doing the step).
• Provide a minimal one-time checklist of things I must provision (servers, domains, storage, GPUs if offline AI, etc).
• Wait for my confirmation to proceed.

PHASE 3 — Synta master prompt for the full factory
• Produce one exact English prompt (one block, paste-ready) I will paste into Synta that asks Synta to build the ENTIRE Soarix Automation Factory (master orchestration workflow + per-branch workflows + placeholders for credentials + exportable n8n JSON templates + acceptance tests + a one-page runbook).
• The prompt must instruct Synta to:
  - create a master “English→Automation” n8n workflow that accepts plain text requests and selects templates,
  - create canonical per-branch workflows (Media, Studios, Publishing, AI, Nexus) with error handling, retries, approvals, and DLQ,
  - include credential placeholder names (no secrets),
  - include export instructions and file naming conventions (so I can export JSON),
  - produce acceptance test payloads for each workflow.
• Keep the prompt simple and story-like but precise about deliverables.
• Wait for my confirmation to proceed.

PHASE 4 — Connect AI (online + offline) to n8n
• Give clear instructions (step-by-step, simple) on how to connect:
  - ChatGPT / OpenAI or Gemini (cloud) to n8n nodes,
  - offline models (Ollama, Llama-studio, private LLM endpoint) to n8n (healthcheck URLs, expected request/response shapes, auth).
• Include example minimal payloads, headers, and a common placeholder base-URL for local AI (e.g., https://ai-local.soa.example/v1).
• Include how to handle quotas, retries, and model fallbacks (cloud → local).
• Wait for my confirmation to proceed.

PHASE 5 — Test builds for each branch
• Give one short test scenario per branch (input, expected outputs, acceptance checks).
• For each test, show exactly what to paste into Synta (if needed) and exactly what to run in n8n after importing JSON.
• Provide one click-style approval flow example (how admin approves a deploy/publish in n8n).
• If tests pass, provide short instructions to export the JSON templates and save them to our repo with naming rules.
• Wait for my confirmation to finish.

ADDITIONAL RULES
• Write everything in very simple English (explain any technical words once).  
• Use placeholders for credentials (e.g., {{CRED_GH_OAUTH}}). Never include secrets.  
• Provide exact file naming examples (soarix_media_post_publish_v1.json).  
• Keep replies short and actionable — step at a time.  
• Ask only one clarifying question if you must. Otherwise, follow the five phases above and wait for my OK after each.

Start by asking: “Do you want to start with Phase 1: Tools & Inventory?”

---

## ASSISTANT →  
Do you want to start with Phase 1: Tools & Inventory?

---

## USER →  
create a .md file in a single code block to copy and paste for the entire chat?

---

## ASSISTANT →  
Before I generate the full .md file, I need one tiny confirmation because your chats span multiple threads.

**Option A:** Full archive of THIS conversation only.  
**Option B:** Merge ALL your conversations into one giant archive.

Which do you choose?

---

## USER →  
option A

---

## ASSISTANT →  
Perfect. I’ll generate Option A — one .md file of this conversation only.

(You are reading that file now.)

---

# END OF THREAD
