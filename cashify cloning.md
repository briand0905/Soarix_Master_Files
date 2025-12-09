```markdown
# 🧠 Soarix AI Orchestrator — E-Commerce Build Chat (Cashify-Style Marketplace)

---

## 🧾 Role & Context

**You (the assistant)** act as a cross-functional expert team:
- Senior **Next.js + TypeScript full-stack developer**
- **DevOps/security engineer**
- **SEO specialist**
- **Accessibility & compliance advisor** (SOC2 + regional frameworks)
- **Product/UX strategist**
- **E-commerce architect**

**Goal:**  
Clone and improve a **Cashify-style refurbished electronics e-commerce** platform starting from:  
`https://github.com/firecrawl/open-lovable`  

Transform it into a **branded, secure, high-performance, owner-controlled product marketplace** with **live pricing & valuation features**.

---

## 🧩 Principles

- **Owner-first:** Business owner controls products, pricing, and approvals — not the developer.  
- **Human-in-the-loop:** Automation only *proposes* changes; owner approves production actions.  
- **Safety-first:** Every risky action must be reversible with rollback + kill-switch.  
- **Layman-friendly:** Each step explained simply first, with developer notes after.  
- **Stepwise gating:** One step at a time; assistant waits for `APPROVE`, `MODIFY`, or `STOP`.

---

## 🪜 Step 0 — Discovery & Goals

### 1) Layman summary
We’ll define the basics — who this site serves, what you want at launch, and what’s essential to get live.  
This shapes every future technical choice (stack, backend type, automation, etc.).

---

### 2) Developer notes
- Validate repo stack: **Next.js + TypeScript** (likely).  
- Decide between **headless commerce** vs **custom backend**.  
- Define infrastructure (hosting, DB, CDN, secrets).  
- Confirm supplier API access, payment methods, and data feeds.  
- Compliance: IMEI, serials, PII → privacy laws (SOC2, regional).  
- Use tokens like 👉 **(Google AI Pro: fetch/update needed here)** to mark where live data is needed later.

---

### 3) Deliverables
- One-page **Discovery Summary** (owner answers + setup plan).  
- MVP feature priorities (owner-first control highlighted).  
- Acceptance checklist for Step 1.  
- Risk register + mitigations.  
- Decision matrix (headless vs custom, Stripe vs PayPal, SKU tier).  
- Step 1 readiness checklist.

---

### 4) Missing full-stack considerations
- Legal/regional compliance (returns, IMEI, taxes).  
- IMEI & anti-fraud mechanisms.  
- Supplier SLAs & caching for APIs.  
- Payment settlement timing & chargeback policies.  
- Inventory model (consignment / owned / marketplace).  
- Warranty & repair process tracking.  
- Image/CDN strategy.  
- PII storage & retention rules.  
- Secrets rotation policy.  
- Audit trails for human approvals.  
- Monitoring & anomaly detection.  
- Automated SEO data refresh 👉 (Google AI Pro: fetch/update needed here).

---

### 5) 💡 Better-than-Cashify Idea
**“Image + IMEI Hybrid Instant Valuator”**  
User uploads device photos + IMEI → system returns instant valuation with confidence score and rationale.  
- **Feasibility:** *Medium* — start rule-based; upgrade with ML once enough labeled data collected.

---

### 6) KPIs & Acceptance Criteria
Owner must confirm:
- ✅ REGION, DOMAIN, SITE_NAME, CONTACT_EMAIL, BRANCH_PREFIX, REPO are correct.  
- ✅ MVP features + human approval flow accepted.  
- ✅ Top 3 risks acknowledged.  
- ✅ Discovery doc ready.

---

### 7) Top 3 Risks & Mitigations
| Risk | Description | Mitigation |
|------|--------------|-------------|
| Valuation errors | Bad pricing may cause loss | Require manual approval, nightly reconciliation, payout delays |
| Supplier downtime | APIs unavailable | Cache results, add fallback supplier, alert on failure |
| Compliance breaches | Mishandling IMEI/PII | Limit region, strong retention rules, legal signoff |

---

### 8) Owner Questions
| Key | Example Value |
|-----|----------------|
| REGION | US |
| DOMAIN | https://example.com |
| SITE_NAME | My Business |
| CONTACT_EMAIL | hi@example.com |
| BRANCH_PREFIX | feature/ |
| REPO | https://github.com/firecrawl/open-lovable |
| TARGET | Cashify-style refurbished marketplace |
| SKU Volume | hundreds / thousands / tens of thousands |
| Suppliers | (list + API access: yes/no) |
| Payment | Stripe / PayPal / Other |
| Backend | Headless / Custom |
| Priority | Speed / Control / Cost / Valuation Engine |
| Novel UX | None / Low / Medium / High |

---

### 9) Owner Action Required
Reply with one of:
- `APPROVE` — confirm and proceed to Step 1.  
- `MODIFY: <changes>` — adjust details and re-present Step 0.  
- `STOP` — cancel setup.

---

## 🧱 Supporting References

### 📘 Soarix Dev Environment Setup (from uploaded PDF)
Referenced environment stack includes:
- **Ubuntu LTS / Pop!_OS** base.  
- **NVM + Node.js LTS** for frontend.  
- **Pyenv + Python** for backend tools.  
- **Docker + Docker Compose** for isolation and deployment.  
- **Supabase / Render / Railway / Firebase** as cloud options.  
- **Cloudflare / BunnyCDN / Backblaze B2** for hosting and media delivery.  
- **Security stack:** UFW, Fail2Ban, Falco, Wazuh, Trivy, Bandit.  
- **Monitoring:** Prometheus, Grafana, Sentry.  
- **Backups:** Timeshift, rclone, rsync.  
- **CI/CD Quality Gates:** SPDX tooling, security linters.  
- **AI Tools:** Ollama, LM Studio, Whisper, Stable Diffusion, Coqui TTS.  
*(source: dev environment setup.pdf):contentReference[oaicite:0]{index=0}*

---

### 📗 Soarix System Prompt V3 Summary
Soarix Solutions — a 5-branch creative + AI-driven ecosystem:  
1. **Soarix Media** — AI marketing agency.  
2. **Soarix Studios** — 3D rendering & visualization.  
3. **Soarix Publishing** — AI-assisted writing & publishing.  
4. **Soarix AI** — Full-stack AI software development.  
5. **Soarix Nexus** — R&D for AI agents & innovation systems.  

Guiding principles:
- Explain simply, like to a smart 10-year-old.  
- Operate as virtual **CEO/CTO/Corporate Lawyer**.  
- Builds must be **production-ready**, covering frontend → backend → infra → monitoring.  
- Always link actions to **business impact, compliance, scalability, and revenue generation.**  
*(source: Soarix System Prompt V3.docx):contentReference[oaicite:1]{index=1}*

---

### 🧭 Integration Context
This Cashify-style marketplace aligns with:
- **Soarix AI** (build & automation).
- **Soarix Media** (marketing & SEO).
- **Soarix Nexus** (AI valuation R&D).
- **Soarix Publishing** (product storytelling, brand content).

---

### 🧮 Executive Insight
Strategically, this build is a *scalable foundation* for Soarix AI’s **commerce intelligence engine** — a model that merges resale economics, pricing analytics, and consumer trust.  
The ROI will depend on:
- Time-to-market (infra ready vs custom backend).  
- Data accuracy (IMEI pricing).  
- Conversion funnel UX (simplicity & credibility).

---

**Next action:**  
Wait for your exact token response.

> ✅ Reply exactly with:  
> - `APPROVE` — move to Step 1 (Repo clone & local sanity)  
> - `MODIFY: <changes>` — edit discovery details  
> - `STOP` — end process  

---

**End of Chat Log — Ready for Export (.md)**  
*(All sections preserved for markdown copy-paste into Notion, GitHub, or Docs.)*
```
