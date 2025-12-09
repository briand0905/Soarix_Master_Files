# Project Blueprint: LedgerZero (CA/CPA Automation SaaS)
**Date:** 2025-12-04
**Role:** AI Business Orchestrator Mentor
**Vertical:** Accounting & Finance Automation

---

## 1. Product Vision
**"LedgerZero"** is an AI-powered data preparation and collaboration platform designed to bridge the gap between messy, real-world financial documents and clean, structured accounting data. 

It is **not** a replacement for Tally, Zoho, or QuickBooks; it is the intelligent "pre-accounting" layer.

**How it works:**
1.  **Ingest:** It takes unstructured data (invoices, receipts, bank statements) from multiple sources.
2.  **Process:** AI normalizes it into clean ledgers.
3.  **Present:** It shows a simplified dashboard for business owners.
4.  **Hand-off:** It provides a secure, review-only portal for CAs/CPAs to audit, export, and file, drastically reducing manual data entry.

---

## 2. Core Features

### Input Flows (The "Digital Shoebox")
* **India-First:** WhatsApp integration (snap a photo, forward a PDF).
* **Email:** Dedicated address (e.g., `bills@client.ledgerzero.com`) to forward e-receipts.
* **Direct Upload:** Web/mobile app for PDFs/images.
* **Bulk Data:** Plain text/CSV copy-paste for bank transaction scrubbing.

### AI Automation Engine
* **OCR & Extraction:** Extracts Vendor, Date, Amount, GSTIN/VAT ID, and Line Items.
* **Auto-Categorization:** AI maps "Uber" → "Travel", "AWS" → "Software". Learns from corrections.
* **Reconciliation:** Flags duplicates and matches invoices to bank lines.

### Dashboards
* **SMB/Freelancer View:** Visual cash flow, draft P&L, estimated GST/VAT. 
    * *Note: All metrics watermarked "Draft: For Professional Review Only".*
* **CA/CPA Audit Portal:** Professional view to filter, annotate, approve/reject transactions, and export to compliance software.

### Integrations & Exports
* **Export:** One-click to Tally `.XML` and generic `.CSV`.
* **Future:** Read-only API for Account Aggregators (India) or Plaid (West).

---

## 3. Target Segments

### India
* **SMBs:** Manufacturers, traders, *kirana* owners (GST registered).
* **Professionals:** Doctors, lawyers, architects (ITR filing).
* **Chartered Accountants:** Small/Mid-sized firms needing to eliminate data entry drudgery.

### Global West (US/UK/EU)
* **Solopreneurs:** Devs, designers, consultants.
* **Creators:** YouTubers, podcasters (sponsorship tracking).
* **Bookkeeping Firms:** Modern firms offering tech-forward services.

---

## 4. Monetization (Recurring SaaS)

### India (₹ INR)
| Tier | Price | Features |
| :--- | :--- | :--- |
| **Freelancer** | ₹499/mo | 100 docs, 1 User |
| **SMB** | ₹999/mo | 500 docs, 1 CA Access |
| **CA Practice** | ₹29,999/yr | 50 Clients, White-label, Practice Dashboard |

### West ($ USD)
| Tier | Price | Features |
| :--- | :--- | :--- |
| **Solopreneur** | $29/mo | 150 docs |
| **Business** | $79/mo | 750 docs, 1 CPA Access, QB Export |
| **CPA Firm** | $499/yr | Per seat, Unlimited clients, Co-branding |

*Note: Payments via Razorpay/Stripe only. No card data stored.*

---

## 5. Compliance & Legal Framework

* **Entity:** Indian Private Limited Company.
* **Master Service Agreement (MSA):** Explicitly defines LedgerZero as a "Data Organization Tool," not a financial advisor.
* **Disclaimer:** "LedgerZero does not provide financial or tax advice. All data must be verified by a qualified professional. User bears full responsibility for filings."
* **Liability Shield:** No "File to Govt" button. The Human Professional is the firewall.
* **Insurance:** Professional Indemnity (PI) + Cyber Liability.

---

## 6. Marketing & GTM Strategy

### India Strategy
* **Keywords:** "Automate tally entry", "WhatsApp accounting", "GST software for SMB".
* **Lead Gen:** Free tools (GST Calculator, HRA Calculator, TDS Guide).
* **Channels:** WhatsApp Marketing, LinkedIn (targeting CAs), ICAI Chapter partnerships.

### West Strategy
* **Keywords:** "AI bookkeeper", "Freelance tax tracker", "QuickBooks alternative".
* **Launch:** Product Hunt, Indie Hackers, BetaList.
* **Integrations:** App marketplaces for Stripe, PayPal, Mercury Bank.

---

## 7. Packaging & Services
* **Core:** SaaS Subscription.
* **Add-on:** "Compliance Calendar" (SMS/Email alerts for due dates).
* **Marketplace (Phase 2):** "Find a Pro" directory. Connect SMBs to vetted CAs for fixed-fee filing services.

---

## 8. Risk Mitigation
* **Zero Liability:** We provide the tool, not the signature.
* **Client-Owned Infra:** Option for clients to connect their own Google Drive/S3 for document storage. We process in-flight.
* **Security:** SOC2-Advisory dashboards (logs/uptime) to build trust without immediate certification costs.

---

## 9. Scalability Roadmap
1.  **MVP:** Web upload → AI Extract → Tally/CSV Export.
2.  **SaaS:** Self-serve tiers + WhatsApp integration.
3.  **Ecosystem:** Professional Marketplace + API for other Fintechs.

---

## 10. Exit Potential
* **Target:** Automation of the "messy" top-of-funnel data.
* **Potential Acquirers (India):** Razorpay, Zoho, Tally, Clear.
* **Potential Acquirers (Global):** Intuit, Xero, Freshworks, Stripe.