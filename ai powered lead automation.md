```md
# AI-powered Lead Intake & Qualification — n8n Workflow
> A single-file reference for the entire chat: full design, node configs, prompts, code snippets, testing, and deployment checklist.  
> Copy-paste this file into your editor or n8n docs.

---

## CONTENTS
1. Workflow Overview  
2. Architecture Diagram (text)  
3. Node-by-node Configuration  
4. AI Agent Configuration  
5. Data Handling & DB Schema  
6. Integration Points (APIs + auth)  
7. Logic & Decision Making (branches, retries)  
8. Step-by-step Implementation (exact settings & snippets)  
9. Code Snippets (JS)  
10. HTTP Request JSON examples  
11. Credentials Setup in n8n  
12. Prompts & Templates (LLM + email)  
13. Testing & Validation Guide (cases + edge cases)  
14. Deployment Checklist  
15. Optimization & Scaling  
16. Monitoring & Logging  
17. Sample n8n JSON skeleton  
18. Final notes & next steps

---

## 1. WORKFLOW OVERVIEW
**Purpose (simple):**  
Inbound leads arrive via webhook → normalized → enriched by company/person API → classified by an LLM into `sales` / `nurture` / `spam` → appropriate CRM upsert and personalized email → log everything to Postgres → retries & alerts for failures.

**Use case chosen:** AI-powered lead intake, qualification, CRM onboarding, follow-up email, audit logging, retry/fallback flows.

---

## 2. ARCHITECTURE DIAGRAM (text)
```

[Webhook Trigger] --> [Set: Normalize Input] --> [IF: Validate Email]
├─> true --> [HTTP Request: Enrichment] --> [IF: Enrichment OK]
│                ├─> true --> [AI: Intent Classifier (LLM)] --> [Switch: Intent]
│                │           ├─> Sales Ready --> [CRM: Upsert Contact] --> [Send Email]
│                │           ├─> Nurture --> [CRM: Upsert Contact] --> [Send Nurture Email]
│                │           └─> Spam --> [Set: Mark Spam] --> [DB: Log]
│                └─> false --> [Set: Mark Enrichment Failed] --> [DB: Log] --> [Retry Queue]
└─> false --> [Set: Invalid Input] --> [Respond / Reject] --> [DB: Log]

All critical nodes → [Catch Error Node] --> [Slack/Email Alert] + [DB: Error Log]
Retry Queue ← Cron Trigger + Postgres SELECT loop

````

---

## 3. NODE-BY-NODE CONFIGURATION

> Use these exact names in n8n so the workflow is easy to read.

### Node: `Webhook: lead-intake`
- **Type:** Webhook
- **HTTP Method:** POST
- **Path:** `lead-intake`
- **Response Mode:** `On Received`
- **Response Code:** `200`
- **Response Body:** `{ "status": "received" }`
- **Security:** validate `x-soarix-secret` header (see credentials)
- **Next:** `Set: Normalize Input`

---

### Node: `Set: Normalize Input`
- **Type:** Set
- **Purpose:** Normalize inputs to stable keys
- **Fields (expressions):**
  - `lead_email` = `{{ $json["email"] || $json["lead_email"] || ($json.contact && $json.contact.email) }}`
  - `lead_name` = `{{ $json["name"] || $json["lead_name"] || (($json["first_name"] || "") + " " + ($json["last_name"] || "")).trim() }}`
  - `lead_source` = `{{ $json["source"] || "web_form" }}`
  - `raw_payload` = `{{ $json }}`
  - `received_at` = `{{ $now.toISOString() }}`
- **Keep Only Set:** true
- **Next:** `IF: Validate Email`

---

### Node: `IF: Validate Email`
- **Type:** IF
- **Conditions (combined AND):**
  1. `lead_email` is not empty
  2. `lead_email` matches regex `^[^\s@]+@[^\s@]+\.[^\s@]+$`
- **True branch:** `HTTP Request: Enrichment`
- **False branch:** `Set: Invalid Input`

---

### Node: `HTTP Request: Enrichment`
- **Type:** HTTP Request
- **Purpose:** Enrich lead with company/person data (example: Clearbit)
- **Method:** `GET`
- **URL (example):**  
  `https://person.clearbit.com/v2/people/find?email={{ $json["lead_email"] }}`
- **Headers:** `Authorization: Bearer {{ $credentials.clearbitApi.key }}`
- **Response Format:** JSON
- **Retry Options:** Enabled (or handle via IF on status)
- **Next:** `IF: Enrichment OK`

---

### Node: `IF: Enrichment OK`
- **Type:** IF
- **Check:** `$node["HTTP Request"].json` contains expected fields (e.g., `company` or `name`)
- **True:** `AI: Intent Classifier`
- **False:** `Set: Mark Enrichment Failed`

---

### Node: `AI: Intent Classifier`
- **Type:** OpenAI node (or HTTP Request to OpenAI)
- **Model:** `gpt-4o-mini` (or `gpt-4o` if available)
- **Temperature:** `0.0`
- **Max Tokens:** `256`
- **System Prompt:** (see Prompts section)
- **User Input:** embed normalized lead + enrichment
- **Expected Output:** Strict JSON `{"intent":"sales|nurture|spam","confidence":0.00,"reason":"...","tags":["..."],"email_snippet":"..." }`
- **Next:** `Switch: Intent` (parse JSON if needed)

---

### Node: `Switch: Intent`
- **Type:** Switch
- **Routes:**
  - `intent == "sales"` → Sales branch
  - `intent == "nurture"` → Nurture branch
  - `intent == "spam"` → Spam branch
  - default → `manual_review`

---

### Node: `CRM: Upsert Contact` (HubSpot example)
- **Type:** HubSpot (native) or HTTP request
- **Operation:** Create or Update
- **Key fields:**
  - `email` = `{{ $json.lead_email }}`
  - `firstname` = `{{ $json.lead_name.split(" ")[0] || "" }}`
  - `lastname` = `{{ $json.lead_name.split(" ").slice(1).join(" ") || "" }}`
  - `company` = `{{ $json.enrichment && $json.enrichment.company && $json.enrichment.company.name || "" }}`
  - custom prop `soarix_intent` = `{{ $json.intent }}`
  - `soarix_tags` = `{{ $json.tags ? $json.tags.join(",") : "" }}`
- **Auth:** OAuth2
- **Next:** `SendGrid: Send Email` (branch-specific) → `Postgres: Insert Log`

---

### Node: `SendGrid: Send Email`
- **Type:** SendGrid (native) or HTTP Request
- **From:** `sales@yourdomain.com`
- **To:** `{{ $json.lead_email }}`
- **Subject:** Branch-specific (e.g., Sales: `Quick intro — {{ $json.lead_name }}`)
- **Body (HTML/text):** Use `{{ $json.ai_result.email_snippet }}` in template
- **Next:** `Postgres: Insert Log`

---

### Node: `Set: Mark Spam`
- **Type:** Set
- **Fields:** `status = "spam"`, `note = {{ $json.reason || "Marked by AI" }}`
- **Next:** `Postgres: Insert Log`

---

### Node: `Set: Mark Enrichment Failed`
- **Type:** Set
- **Fields:** `status = "enrichment_failed"`, `retry_count = 0`, `next_retry_at = {{ $now.add({ minutes: 15 }).toISOString() }}`
- **Next:** `Postgres: Insert Log` and `Retry Queue` (Cron-based)

---

### Node: `Postgres: Insert Log`
- **Type:** Postgres
- **Operation:** Insert
- **Table:** `lead_logs`
- **Columns mapping:**
  - `lead_email`, `lead_name`, `lead_source`, `enrichment_json`, `ai_result_json`, `status`, `raw_payload`, `received_at`, `retry_count`, `next_retry_at`
- **Next:** `Respond to Webhook` (if manual)

---

### Node: `Respond to Webhook` (final)
- **Type:** Respond to Webhook (use if webhook is manual response mode)
- **Response Code:** `200`
- **Body:**  
  ```json
  {
    "status": "ok",
    "lead_email": "{{$json.lead_email}}",
    "action": "{{$json.status || 'queued'}}",
    "message": "Lead processed"
  }
````

---

### Node: `Catch Error Node`

* **Type:** Error Trigger / Catch Error
* **Purpose:** Catch exceptions and route to alert + error log
* **Connected to:** `Slack: Alert` and `Postgres: Error Log`
* **Slack Message Example:** `Error in node {{$error.node.name}}: {{$error.message}}. Lead: {{$json.lead_email}}`

---

### Node: `Retry Queue` (Cron + Postgres)

* **Type:** Cron Trigger (every 15 minutes) → Postgres SELECT
* **Select:** `SELECT * FROM lead_logs WHERE status='enrichment_failed' AND next_retry_at <= now() AND retry_count < 5;`
* **Loop:** Re-run `HTTP Request: Enrichment` for each row, increment `retry_count`, set `next_retry_at` to exponential backoff (15m * 2^retry_count)
* **If retry_count >= 5:** set `status='manual_review'` + Slack alert

---

## 4. AI AGENT CONFIGURATION

**LLM Choice (recommended):**

* Primary: **OpenAI** `gpt-4o-mini` (cost/latency friendly)
* Fallback: `gpt-3.5-turbo` for cheaper backup
* Alternative: **Anthropic Claude** for privacy-sensitive deployments
* Local options only if you self-host (Llama 2/3, Orca, etc.)

**System Prompt (exact):**

```
You are a concise lead-qualification assistant. Given a lead's email, name, enrichment data (company, job title, size), and raw form fields, return a strict JSON with fields: intent (sales|nurture|spam), confidence (0.00-1.00), reason (1-2 sentences), tags (array of strings), and a one-sentence email_snippet for personalization. Use deterministic answers. Do not include any other text.
```

**Tools for the agent:**

* n8n HTTP Request nodes provide integration to company DB or sales-rule microservices.
* Agent must not call external tools directly outside n8n.

**Memory / Context:**

* Keep per-lead context ephemeral; store only `ai_result_json` in DB.
* For conversational agents, store a short summary (50–200 chars) in Redis or DB.

**Token & Cost Strategy:**

* `temperature: 0.0`, `max_tokens: 256`
* Short structured prompts; provide a strict JSON schema to reduce output length and parsing issues.
* Cache enrichment results for 24 hours.

---

## 5. DATA HANDLING & DB SCHEMA

**Normalized input shape:**

```json
{
  "lead_email":"alice@example.com",
  "lead_name":"Alice Example",
  "lead_source":"web_form",
  "raw_payload": { ... },
  "received_at":"2025-11-21T06:00:00.000Z"
}
```

**AI output shape (expected):**

```json
{
  "intent":"sales",
  "confidence":0.92,
  "reason":"Asking about pricing for 50 seats.",
  "tags":["SaaS","Pricing"],
  "email_snippet":"We help growing teams scale seats with predictable pricing and onboarding."
}
```

**Postgres table `lead_logs` (recommended columns):**

* `id` SERIAL PRIMARY KEY
* `lead_email` TEXT NOT NULL
* `lead_name` TEXT
* `lead_source` TEXT
* `enrichment_json` JSONB
* `ai_result_json` JSONB
* `status` TEXT
* `raw_payload` JSONB
* `received_at` TIMESTAMPTZ
* `updated_at` TIMESTAMPTZ DEFAULT now()
* `retry_count` INT DEFAULT 0
* `next_retry_at` TIMESTAMPTZ NULL
* Indexes: `lead_email`, `(status, next_retry_at)`

**Validation rules:**

* Email regex check.
* If missing name, set to `"Unknown"`.
* If critical fields missing → reject with `400` or log `invalid_input`.

---

## 6. INTEGRATION POINTS (APIs + Auth + Endpoints)

### Clearbit (example)

* **Auth:** API Key (header `Authorization: Bearer <KEY>`)
* **Endpoints:** `https://person.clearbit.com/v2/people/find?email=...` or company endpoints by domain
* **Response:** JSON — map to `enrichment_json`
* **Rate limits:** Handle `429` with exponential backoff; if 5xx → retry; if 4xx → stop and mark failed

### OpenAI

* **Auth:** `Authorization: Bearer <OPENAI_KEY>`
* **Endpoint:** `https://api.openai.com/v1/chat/completions`
* **Body:** chat messages (system + user)
* **Rate limits:** watch 429 — backoff and retry / fallback to smaller model
* **Error handling:** On 5xx, fallback to `gpt-3.5-turbo` or queue for manual review

### HubSpot

* **Auth:** OAuth2 (recommended)
* **Endpoint:** `/crm/v3/objects/contacts` (create/update)
* **Behavior:** Upsert by searching email first to avoid duplicates
* **Rate limit:** HubSpot per-app limits — handle 429

### SendGrid

* **Auth:** `Authorization: Bearer <SENDGRID_KEY>`
* **Endpoint:** `https://api.sendgrid.com/v3/mail/send`
* **Request:** JSON with `personalizations`, `content`
* **Error handling:** Retry once, then log and manual follow-up

---

## 7. LOGIC & DECISION MAKING

**Branches:**

* `IF: Validate Email` → proceed or reject
* `IF: Enrichment OK` → proceed to AI or mark enrichment_failed
* `Switch: Intent` → `sales` / `nurture` / `spam` / `manual_review`

**Retry logic:**

* External API 429/5xx → exponential backoff (1s, 2s, 4s) for node retries
* Enrichment failures → set `retry_count` and `next_retry_at` (15m * 2^retry_count), Cron-based retry up to 5 times
* Email send failure → 1 immediate retry, then queue for manual

**Looping:**

* Retry Cron selects rows and loops per row. Use `SplitInBatches` to control parallelism to respect rate limits.

**Escalation:**

* After `retry_count >= 5`, set `status = manual_review` and notify Slack `#ops`.

---

## 8. STEP-BY-STEP IMPLEMENTATION (practical, paste-ready)

> Build this in the n8n UI in the order below. Use the node configs from section 3. Use credential placeholders (do not paste real keys here).

1. Create **Webhook** node named `Webhook: lead-intake`. Set method `POST`, path `lead-intake`, `On Received` response.
2. Add **Set** node `Set: Normalize Input`. Add fields per section 3.
3. Add **IF** node `IF: Validate Email`. Configure combined rules (not empty + regex).
4. Add **HTTP Request** node `HTTP Request: Enrichment`. Configure URL to enrichment provider, headers with `Clearbit API Key` credential.
5. Add **IF** node `IF: Enrichment OK`. Check `$node["HTTP Request"].json` content.
6. Add **OpenAI** node `AI: Intent Classifier` (or HTTP Request). Paste the system prompt and user message embedding `{{ $json }}`. Set `temperature=0` `max_tokens=256`.
7. Add **Switch** node `Switch: Intent`. Map `intent` to branches `sales/nurture/spam`.
8. Add **CRM: Upsert Contact** node (HubSpot). Map properties and use email as key.
9. Add **SendGrid** node `SendGrid: Send Email` in each branch. Use `email_snippet` for personalized body.
10. Add **Set** nodes `Set: Mark Spam` and `Set: Mark Enrichment Failed`.
11. Add **Postgres** node `Postgres: Insert Log` to persist every run.
12. Add **Respond to Webhook** (if needed for manual response).
13. Create **Error Trigger** node (Catch) to send Slack alerts and log errors.
14. Create **Cron** node for retries (every 15 minutes) + Postgres SELECT + loop to re-run enrichment and increment `retry_count`.

---

## 9. CODE SNIPPETS (JS) — Use minimal code nodes only where necessary

### Deduplicate check (Code)

```javascript
// Input: $json.lead_email
const leadEmail = ($json.lead_email || "").toLowerCase();
const result = await $postgres.query('SELECT id FROM lead_logs WHERE lead_email = $1 LIMIT 1', [leadEmail]);
if(result.rows && result.rows.length) {
  return [{ json: { already_exists: true, id: result.rows[0].id } }];
}
return [{ json: { already_exists: false } }];
```

> Note: n8n has native Postgres node. Prefer that when possible.

### Exponential backoff calculation (Set or Code)

```javascript
const retry = $json.retry_count || 0;
const minutes = 15 * Math.pow(2, retry);
const nextRetryAt = new Date(Date.now() + minutes * 60 * 1000).toISOString();
return [{ json: { retry_count: retry + 1, next_retry_at: nextRetryAt } }];
```

---

## 10. HTTP REQUEST JSON EXAMPLES

### OpenAI ChatCompletion

```json
{
  "model":"gpt-4o-mini",
  "messages":[
    {"role":"system","content":"You are a concise lead-qualification assistant..."},
    {"role":"user","content":"Lead data: {\"email\":\"alice@example.com\",\"name\":\"Alice\"}"}
  ],
  "temperature":0.0,
  "max_tokens":256
}
```

### SendGrid send

```json
{
  "personalizations":[
    {"to":[{"email":"alice@example.com"}],"subject":"Thanks for reaching out"}
  ],
  "from":{"email":"sales@soarix.com"},
  "content":[{"type":"text/html","value":"<p>Hi Alice, ...</p>"}]
}
```

---

## 11. CREDENTIALS SETUP IN N8N (what to create)

* **Clearbit API Key** (HTTP header)
* **OpenAI API Key** (OpenAI credential)
* **HubSpot OAuth2** (client ID, secret; configure redirect URL to n8n)
* **SendGrid API Key**
* **Postgres DB** (host, port, user, password, db)
* **Slack** (Webhook URL or Bot token for alerts)
* **Webhook Secret**: `x-soarix-secret` (string stored in Secrets/Credentials)

**Security tips:** Use n8n credentials store; restrict UI; rotate keys periodically.

---

## 12. PROMPTS & TEMPLATES

### System prompt (copy-paste)

```
You are a concise lead-qualification assistant. Given a lead's email, name, enrichment data (company, job title, size), and raw form fields, return a strict JSON with fields: intent (sales|nurture|spam), confidence (0.00-1.00), reason (1-2 sentences), tags (array of strings), and a one-sentence email_snippet for personalization. Use deterministic answers. Do not include any other text.
```

### User prompt template

```
LeadData: {{ JSON.stringify($json) }}
Return only JSON with fields: intent, confidence, reason, tags, email_snippet.
```

### Sales email template (HTML)

```
Subject: Quick intro — we help {{ $json.enrichment.company.name || "teams like yours" }}

Hi {{ $json.lead_name || "there" }},

{{ $json.ai_result.email_snippet }}

Are you open to a 15-minute call to explore this?

— Sales, Soarix Solutions
```

---

## 13. TESTING & VALIDATION GUIDE

### Test Cases

1. **Sales happy path**

   * Input: `{ "email":"alice@startup.com", "name":"Alice", "source":"website" }`
   * Expect: Enrichment OK, AI returns `sales`, HubSpot upsert, email sent, DB row status `sales_sent`.

2. **Nurture**

   * Input: similar; AI returns `nurture`
   * Expect: Contact upsert, nurture email, DB status `nurture_queued`.

3. **Spam**

   * Input: spam-like content
   * Expect: logged as spam, no email.

4. **Invalid email**

   * Input missing `@` or empty email
   * Expect: `invalid_input` response and DB entry.

5. **Enrichment 429**

   * Simulate 429
   * Expect: `enrichment_failed`, `retry_count` set, queued for retry Cron.

6. **LLM error**

   * Simulate 500 from OpenAI
   * Expect: fallback or `manual_review`, Slack alert.

### Edge Cases

* Duplicate leads (same email) → Upsert not duplicate
* Missing name → default to `Unknown`
* Concurrent bursts → validate concurrency limits and SplitInBatches

### Validation steps

* Verify `lead_logs` entries for all test inputs
* Check HubSpot for created contact
* Check SendGrid activity for sent emails
* Verify Slack alerts for errors

---

## 14. DEPLOYMENT CHECKLIST

1. Add all credentials to n8n.
2. Create DB table `lead_logs` and indexes.
3. Configure webhook secret and IP allowlist.
4. Limit concurrency for critical nodes (enrichment & LLM).
5. Configure Catch Error → Slack & DB error log.
6. Run tests in staging environment and validate results.
7. Set up DB backups and n8n backup plan.
8. Configure monitoring (Datadog/Prometheus) for rate/latency.
9. Plan API key rotation and incident runbook for `manual_review` queue.
10. Export & version the workflow JSON.

---

## 15. OPTIMIZATION & SCALING

**Execution time**

* Cache enrichment by domain for 24 hours (Redis or DB).
* Use `gpt-4o-mini` or cheaper classification model.
* Use `SplitInBatches` for multi-item processing.

**Cost**

* Keep prompts short; `temperature: 0.0`; `max_tokens: 256`.
* Cache repeated AI outputs for identical payloads.

**Scalability**

* Use Postgres with connection pooling.
* Run multiple n8n workers; use a job queue for heavy tasks.
* Offload enrichment to background worker workflows.

---

## 16. MONITORING & LOGGING

* Log every run to `lead_logs`.
* Send critical errors to Slack `#soarix-alerts`.
* Send metrics to Datadog (count by intent, avg LLM tokens).
* Add uptime monitor for the webhook endpoint.

---

## 17. SAMPLE N8N JSON SKELETON (import into n8n and extend)

```json
{
  "name": "Lead Intake AI Qualification",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "lead-intake",
        "responseMode": "onReceived",
        "responseData": "={{{\"status\":\"received\"}}}"
      },
      "name": "Webhook: lead-intake",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [240, 300]
    },
    {
      "parameters": {
        "values": {
          "string": [
            {"name": "lead_email", "value": "={{$json[\"email\"] || $json[\"lead_email\"]}}"},
            {"name": "lead_name", "value": "={{$json[\"name\"] || $json[\"lead_name\"]}}"},
            {"name": "lead_source", "value": "={{$json[\"source\"] || \"web_form\"}}"},
            {"name": "received_at", "value": "={{$now.toISOString()}}"}
          ]
        }
      },
      "name": "Set: Normalize Input",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [500, 300]
    },
    {
      "parameters": {
        "conditions": {
          "combined": {
            "rules": [
              {"rule": {"value1": "={{$json[\"lead_email\"]}}", "operation": "isNotEmpty"}},
              {"rule": {"value1": "={{$json[\"lead_email\"]}}", "operation": "matchesRegex", "value2": "^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$"}}
            ],
            "operation":"and"
          }
        }
      },
      "name": "IF: Validate Email",
      "type": "n8n-nodes-base.if",
      "typeVersion": 1,
      "position": [760, 300]
    }
  ],
  "connections": {
    "Webhook: lead-intake": {"main": [[{"node":"Set: Normalize Input","type":"main","index":0}]]},
    "Set: Normalize Input": {"main": [[{"node":"IF: Validate Email","type":"main","index":0}]]}
  }
}
```

> Import and extend with other nodes using the UI.

---

## 18. FINAL NOTES & NEXT STEPS

* This file is a complete, production-ready blueprint for an n8n workflow that handles lead intake, enrichment, AI-based qualification, CRM upsert, email follow-up, logging, retries, and alerts.
* If you want an **importable full workflow JSON** with placeholders for API keys and exact node configs (every node fully expanded), I can generate that next.
  (I will insert placeholders like `{{OPENAI_API_KEY}}`, `{{HUBSPOT_CLIENT_ID}}`, etc., so you can safely paste real keys in n8n credentials.)

---

*End of document.*
If you'd like the full importable n8n JSON with all nodes filled and placeholders for your credentials, say "Generate importable workflow JSON" and I will produce it next.
