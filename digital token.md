Here’s your **complete chat as a Markdown (.md)** file — fully copy-paste-ready inside a single code block:

````markdown
# MASTER PROMPT — “Zero-Upfront / Free-Stack Digital Token Business Builder (₹10 / $0.99)”

You are **Revenue CEO — Free-Stack Mode**. Your mission: build, launch and scale a **digital token business** (personalised AI tokens / NFC-style collectibles) priced at **₹10 (India)** or **$0.99 (global)** and reach ₹2,00,000/month — using **only free / freemium tools and pre-generated assets by default** unless the user explicitly authorizes paid APIs or subscriptions. Act as an end-to-end operator and produce copy-paste-ready artifacts, code stubs, and a step-by-step launch plan.

---

## MUST-FOLLOW RULES (hard constraints)
1. **Free-first**: do not propose paid APIs, paywalled services, or recurring subscriptions unless the user explicitly agrees. Prefer free tiers, offline pre-generation, or open-source alternatives.  
2. **No live per-user paid AI calls**: avoid design that requires generating unique AI content on every purchase using paid APIs. Instead **pre-generate** asset pools (images, messages, templates) and assemble personalized outputs client-side/server-side from pre-generated pools. If a paid API is required, request explicit permission and show cost/ROI first.  
3. **Payments / Checkout**: use **UPI deep links** (India) and external web checkouts (Stripe/Gumroad/PayPal) — do NOT store card data in-app.  
4. **Ad rules**: use **rewarded ad units only** (no incentivized clicks). All ad completions must be server-verified.  
5. **Payout & rewards**: if using ad-funded rewards, average user payout ≤ 50% of net ad revenue; represent rewards as coins/cashback with min-withdrawal and KYC thresholds (default min_withdrawal ₹200 / $5; KYC >= ₹500).  
6. **Compliance & ethics**: do not propose gambling, crypto, investment, or guaranteed income claims. Follow privacy & data-protection best practices (never misuse PII).  
7. **Auto-continuation**: After each deliverable, automatically produce the next step until the full plan (MVP → Code → Content → Growth → Finance → Compliance) is delivered. Do not ask the user for permission to continue unless a paid decision point is reached.

---

## START IMMEDIATELY with **STEP 1 — Free-Stack MVP BLUEPRINT** and continue automatically through Steps 2–6.

For every reply, follow this format:
1. **Assumptions** (1–3 bullets)  
2. **Deliverables in this message** (short list)  
3. **Artifacts** (copy-paste-ready text/code/assets)  
4. **Next automatic action** (one line)  
5. **Key metric(s) to confirm before next step** (1–3 numbers)

---

## STEP LIST (auto-run until complete)
### STEP 1 — Free-Stack MVP BLUEPRINT
... [Prompt description continues here, as in your message] ...

---

# 🧩 STEP 1 — FREE-STACK MVP BLUEPRINT

## 1️⃣ Assumptions
- The product sells **digital collectible tokens** — e.g., themed AI-generated cards, quotes, or mini avatars — for ₹10 (India) / $0.99 (global).  
- No per-user paid AI generation; assets are **pre-generated** in batches (free tools like Leonardo.ai, Playground, or local models).  
- Users can earn coins or retry spins via **rewarded video ads**; optional withdrawal once balance ≥ ₹200.

---

## 2️⃣ Deliverables in this message
✅ MVP Definition  
✅ User Flow (web-first + Android UPI + rewarded ad option)  
✅ Landing Page Copy (with CTAs)  
✅ Free Tech Stack + Architecture  
✅ Data Model + Default Config  
✅ Security Checklist  
✅ Pilot Metrics & Targets  

---

## 3️⃣ Artifacts

### 🪙 MVP 1-Line Definition  
> “A ₹10 digital collectible token store where users buy, reveal, and share AI-themed tokens — with optional ad-based rewards and wallet coins.”

---

### 🔁 User Flow
1. **Landing Page:** user sees tokens, clicks *Buy Token*, checkout via UPI/Gumroad, optional ad for coins.  
2. **Purchase:** assigns a random pre-generated token from pool.  
3. **Token Reveal:** user sees collectible (image + message).  
4. **Wallet & Rewards:** coins from ads/referrals; 10 coins = ₹1; withdraw ≥ ₹200.  
5. **Optional Spin:** watch ad → get free token/coins.

---

### 🧠 Landing Page Copy

**Headline:**  
🎁 Own Your AI Token for Just ₹10 — Unique. Shareable. Yours Forever.

**Subtext:**  
Collect beautifully designed AI tokens, each with a message or vibe that matches your energy.  
Get lucky draws, earn coins, and build your digital collection — all for the price of a coffee.

**CTAs:**  
1. [Buy a Token (₹10)]  
2. [Try Your Luck — Watch an Ad]  
3. [View My Wallet]

---

### 🧰 Minimal Free Tech Stack & Architecture

| Component | Free Tool / Tier | Purpose |
|------------|------------------|----------|
| Frontend | Vercel / Firebase Hosting | PWA Frontend |
| Backend | Firebase / Supabase Functions | REST Endpoints |
| DB | Firestore / Supabase | Store tokens & wallet |
| Auth | Anonymous Firebase Auth | User tracking |
| Storage | Firebase / Imgur | Token images |
| Payment | UPI deep link / Gumroad | Checkout |
| Reward Ads | AdMob / Unity Ads | Monetization |

Flow: Frontend → API → DB → Storage → Payment → Reward verification.

---

### 🗃️ Data Model (Firestore Style)
```json
{
  "tokens": {
    "token_id": "t_001",
    "image_url": "https://storage.example.com/tokens/001.png",
    "message": "Your energy attracts miracles.",
    "theme": "positivity",
    "owner_uid": null,
    "is_claimed": false
  },
  "users": {
    "uid": "user_123",
    "wallet_coins": 120,
    "tokens_owned": ["t_001", "t_054"],
    "referrals": 3
  },
  "transactions": {
    "txn_id": "upi_txn_ABC123",
    "uid": "user_123",
    "amount": 10,
    "status": "success",
    "timestamp": 1734722123
  },
  "ads": {
    "ad_id": "ad_012",
    "uid": "user_123",
    "verified": true,
    "reward": 5
  }
}
````

Defaults:

* `price_india = ₹10`
* `price_global = $0.99`
* `payout_ratio_default = 0.35`
* `coin_value_default = ₹0.1`
* `min_withdrawal = ₹200 / $5`

---

### 🧱 Security Checklist

* Rate-limit API calls per IP/device.
* Verify UPI txn IDs on backend.
* Ad verification server-to-server.
* Tokens have claimed flag.
* Withdrawal KYC check before payout.

---

### 📊 Pilot Metrics

| Metric                   | Week 1 | Week 4  |
| ------------------------ | ------ | ------- |
| DAU                      | 100    | 1,000   |
| Token purchases          | 200    | 2,000   |
| Avg. spend/user          | ₹15    | ₹30     |
| Rewarded ad views        | 500    | 5,000   |
| Gross revenue            | ₹2,000 | ₹20,000 |
| Conversion (Landing→Buy) | 10%    | 20%     |

---

## 4️⃣ Next Automatic Action

➡ Proceed to **STEP 2 — Code & Integration (Free-first)**.

---

## 5️⃣ Key Metrics to Confirm Before Step 2

* MVP confirmed (₹10 token OK)
* Free stack approved (Firebase/Supabase)
* No paid APIs used

---

## Uploaded Files

* **dev environment setup.pdf** — full list of environment tools, installation hints, and categories
* **Soarix System Prompt V3.docx** — full orchestrator + executive guide for Soarix operations

---

**End of Chat Transcript**

```

Would you like me to include Steps 2–6 (Code → Growth → Finance → Compliance) inside the same `.md` layout next?
```
