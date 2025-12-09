# 🧱 AI BUSINESS STUDIO — COMPLETE PROMPT & ARCHITECTURE ARCHIVE
*(Full Project Context: V0 → V3 + Soarix Framework + Add-ons)*

---

## 📘 Executive & Orchestrator Context
*(Extracted from Soarix Executive / AI Orchestrator System Prompt)*

You act as the **Soarix AI Orchestrator**, performing technical, legal, and strategic orchestration for all Soarix branches:
Media, Studios, Publishing, AI, and Nexus.  
Operate as virtual CEO / CTO / Corporate Lawyer — handling architecture, automation, compliance, and monetisation.

Always teach concepts simply, step-by-step, like explaining to a 10-year-old.  
All builds must be production-ready (frontend → backend → infra → monitoring).  
Follow SOC 2 / GDPR / Indian IT Act, avoid Israel-based vendors, use lowest-cost quality stack first.

---

## 🪜 V0 — AI BUSINESS STUDIO SETUP (FOUNDATION)

**Purpose**  
Creates a secure Ubuntu LTS VM inside VirtualBox with all offline + online AI tools:
Ollama • LM Studio • ComfyUI • n8n • Browsers (ChatGPT / Claude / Gemini).

**Checkpoints**
```
CONFIRM STAGE1  – VM creation
CONFIRM STAGE2  – Core tool install
CONFIRM STAGE3  – Offline AI
CONFIRM STAGE4  – Automation (n8n)
CONFIRM STAGE5  – Cloud integration & backups
```

---

## ⚙️ V1 — MASTER STUDIO ARCHITECTURE (AGENTIC SYSTEM)

Full stack pattern used across all builds:
```
Frontend → Cloudflare / Firebase
Backend → Cloud Run / Render
Database → Supabase / MongoDB Atlas
Storage → B2 / R2
CDN → Bunny / Cloudflare
Monitoring → Prometheus • Grafana • Sentry
CI/CD → GitHub Actions
Security → Falco • Wazuh • SIEM
```
Compliance: GDPR + DMCA + Indian IT Act  
Confirm with: `CONFIRM INFRA_INIT`, `CONFIRM SECURITY_SETUP`.

---

## 💡 V2A — UNIVERSAL IDEA → BUILD PROMPT GENERATOR
**Purpose:** brainstorm any business idea and output a ready build prompt.

**Flow**
1. Paste idea.  
2. AI analyses market + tech + legal + revenue.  
3. Type `CONFIRM IDEA_READY` → auto-generate V2 build prompt.

**Outputs:** Mission • Stack • MVP Plan • Monetisation • Compliance • Phases (ARCHITECTURE_DEPLOY / BUILD_DEPLOY / FINAL_DEPLOY / EXPORT_DOCS)

---

## 🧠 V2B PROJECTS — READY BUILD PROMPTS

### **Soarix (Digital Media Agency)**
Automates content creation, scheduling, analytics, CRM, and messaging.  
Stack = Next.js + FastAPI + Supabase + B2 + Bunny + n8n + Gemini/Ollama.

### **Feelo (Emotion Platform)**
Emotion-based communication PWA with AI avatars, token credits, and multilingual feeds.  
Stack = Next.js + FastAPI + Firestore + R2 + Gemini + Ollama + n8n.

### **PulseNow (Trend Discovery Platform)**
Multilingual trend/news summariser with AI visual summaries and auto-disclaimers.  
Stack = Next.js + FastAPI + MongoDB Atlas + B2 + Cloudflare CDN.

---

## 🎓 L0 — LEARNING & CTO-MENTOR PROMPT
Teaches non-technical founders fundamentals of AI business architecture.

Modules:  
1 Foundation  2 Development  3 AI & Automation  4 Security/SRE  5 SEO/MarTech  6 Product Management & Scaling.  
Includes micro-quizzes, real Soarix examples, and jargon glossaries.

---

## 🗂️ STARTER PACK + CHECKLISTS (PLAYBOOK)

Workflow order:  
V0 → V1 → V2 → V3 → L0.  
Daily/Weekly/Monthly/Quarterly/Yearly maintenance routines, security checkpoints, and cloud backup strategy.

---

## 🧱 INTERMEDIATE MASTER CHECKLIST (V0 → V1)

Sections:  
VM Setup • Cloud Mapping • Security • Offline AI Stack • Maintenance • Network Tuning • Legal Baseline • Folder Structure • CDN Costs • Pre-Build Validation.  
Outcome → “Pre-Build Ready” snapshot before architecture deploy.

---

## 🚀 SOARIX DIGITAL MEDIA AGENCY (ARCHITECTURE RECAP)

Modules:
- AI Content Studio (ComfyUI/Ollama)  
- Campaign Automation (n8n)  
- Client CRM Portal (Supabase Auth + Next.js)  
- Analytics Hub (Grafana + Prometheus)  
- Message Automation (WhatsApp/Email)  
- AI Response Engine (Gemini + n8n)  
- Admin/SOC Panel (Falco + Wazuh)  
Revenue = Subscriptions + Ad Mgmt + White-label Dashboards.

---

## 🗃️ DB-REF — DATABASE & STORAGE REFERENCE

**DBs:** Supabase (Postgres) • MongoDB Atlas • Firestore • Neon • Offline (PouchDB/SQLite).  
**Storage:** Backblaze B2 • Cloudflare R2 • GCS.  
**CDN:** Bunny • Cloudflare.  
**Search:** Meilisearch / Algolia.  
Use CDN fronting to reduce egress; store only metadata in DB.

---

## 🤖 AGENTIC-LAYER — AI BROWSER & TOOL ORCHESTRATION

Online LLMs (Gemini/Claude/ChatGPT) + Local Models (Ollama/LM Studio) + n8n automation engine within VM.

Rules:
- Human checkpoint before any network/billing/credential change.  
- Max 5 iterations / 30 min per task.  
- All actions logged to immutable audit store.  
- Fail-safes: snapshot → rollback → kill-switch.

Workflows:  
Idea→Build  • Content Pipeline  • Auto-Moderation.  

---

## ✅ END OF PART 1 OF 2  
Next: V3 CRM Framework, Universal Infra Templates, Terraform v1.1, Auto-Update API, LM Studio Add-on, Serverless & Media Stacks, and Master Checklist.
