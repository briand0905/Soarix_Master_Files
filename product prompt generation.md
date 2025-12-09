

You are an expert software product engineer, web devand prompt-crafting assistant whose job is to convert short product ideas into complete, model-ready prompts and then to support generation, assembly, testing, and hardening of runnable code. Follow the interaction pattern and strict output formats

pasted

I'll help you convert product ideas into complete, model-ready prompts and support code generation. Since you haven't provided a specific idea, I'll proceed with the DEFAULT PRODUCT: ThePulseNow.com.

Using default product: ThePulseNow. I'll generate a tree-first decision map and then a linear execution plan.

1) Short Clarifying Summary
ThePulseNow.com is a global news aggregator with AI summarization, region-aware translation (capped at Top-10 languages per region), and monetization through ads/payments. Major constraints: API cost control (OpenAI GPT-4 with fallbacks), translation caps, legal attribution requirements. Highest-risk assumptions: API quota management, geo-detection accuracy, payment gateway regional compliance.

2) Decision Tree (TREE-FIRST)
ThePulseNow Architecture Decision Tree
=======================================

[ROOT: Product Architecture]
    |
    ├─[A: Tech Stack]
    │   ├─[A1: MEAN/MERN] Cost:Med, Complex:Med, Risk:React-SSR issues, Audience:Scale
    │   ├─[A2: Next.js+FastAPI] ★MVP★ Cost:Low, Complex:Low, Risk:Python/JS split, Audience:MVP
    │   └─[A3: Django Full] Cost:Low, Complex:High, Risk:Frontend limitations, Audience:Enterprise
    │
    ├─[B: Infrastructure]
    │   ├─[B1: AWS Full] Cost:High, Complex:High, Risk:Cost overruns, Audience:Scale
    │   ├─[B2: Vercel+CloudRun] ★MVP★ Cost:Low, Complex:Low, Risk:Vendor lock, Audience:MVP
    │   └─[B3: Self-hosted K8s] Cost:Med, Complex:Very High, Risk:Ops burden, Audience:Enterprise
    │
    ├─[C: Translation Strategy]
    │   ├─[C1: Google Translate API] Cost:High, Complex:Low, Risk:Quota limits, Audience:Scale
    │   ├─[C2: OpenAI+Fallback] ★MVP★ Cost:Med, Complex:Med, Risk:Quality variance, Audience:MVP
    │   └─[C3: Open-source only] Cost:Low, Complex:High, Risk:Poor quality, Audience:Budget
    │
    ├─[D: Monetization]
    │   ├─[D1: Ads only] Cost:Low, Complex:Low, Risk:Low revenue, Audience:MVP
    │   ├─[D2: Ads+Payments] ★MVP★ Cost:Med, Complex:Med, Risk:Payment compliance, Audience:MVP
    │   └─[D3: Subscription] Cost:Med, Complex:High, Risk:User acquisition, Audience:Scale
    │
    └─[E: Data Ingestion]
        ├─[E1: RSS+Scraping] ★MVP★ Cost:Low, Complex:Med, Risk:Rate limits, Audience:MVP
        ├─[E2: News APIs] Cost:High, Complex:Low, Risk:API costs, Audience:Scale
        └─[E3: Manual curation] Cost:Med, Complex:Low, Risk:Scale limits, Audience:Niche

★ Recommended MVP Path: A2+B2+C2+D2+E1
Rationale: Balance of low initial cost, quick deployment, and room to scale
3) Full Model-Ready "Full-Project Generation" Prompt
prompt
You are an expert Senior Fullstack Engineer. Generate a runnable project for: ThePulseNow.com - a global news aggregator with AI summarization, region-aware translation, and monetization.

Use the tech stack: Frontend Next.js 14 + TypeScript + Tailwind CSS + Framer Motion + Lottie; Backend Python FastAPI; DB Supabase Postgres; Cache Upstash Redis; Task queue Celery; AI OpenAI GPT-4 summarization with fallback; Geo MaxMind GeoIP2 + IP-API fallback; Payments Razorpay (India) + PayPal (non-India).

CRITICAL REQUIREMENTS:
- English-first SEO (all URLs/slugs in English)
- Top-10 languages per region translation cap
- X-Region-Suggested-Language header on all responses
- Cookie/localStorage preference persistence for anon users
- Supabase profile persistence for authenticated users
- Redis caching for summaries/translations (24hr TTL)
- Quota checks before ALL paid API calls with graceful fallbacks
- Legal attribution disclaimers on all article pages

STRICT OUTPUT FORMAT:
1) First print a complete file tree
2) Then for EVERY file print header: //// FILE: <path>
3) Follow immediately with a fenced code block containing exact file contents
4) No extra narrative, no numbered lists - only file-tree then file blocks
5) If truncated, print token: CONTINUE

REQUIRED FILES:
- README.md (with exact setup steps, curl examples)
- .env.example (all required ENV vars)
- setup_dev.sh (migrations, seeds, local run)
- Dockerfile, docker-compose.yml
- Backend: FastAPI app with /api/articles, /api/translate, /api/summarize, /api/payments/webhook
- Frontend: Next.js pages with language toggle, article display, embed components
- Database: Supabase schema (articles, translations, user_preferences, payment_sessions)
- Redis: Caching helpers for summaries/translations
- Celery: Background tasks for ingestion, summarization
- Tests: pytest backend, Jest frontend, Playwright e2e
- CI: .github/workflows/ci.yml
- Seed data: Top-10 trending regions, sample articles

FUNCTIONAL REQUIREMENTS:
- Ingest RSS feeds from major news sources
- AI summarization with 3-bullet format
- Translation with caching and Top-10 cap enforcement
- GeoIP detection with MaxMind primary, IP-API fallback
- Payment flow: detect region → show appropriate gateway → issue signed session token
- Ad slots with regional targeting placeholders
- Social embeds (Twitter, Instagram, YouTube)
- PWA configuration with offline support
- Accessibility: ARIA labels, keyboard navigation

VALIDATION & ERROR HANDLING:
- Check API quotas before calls: if exhausted, show "Translation/Summary unavailable"
- Rate limiting middleware (100 req/min per IP)
- Input sanitization for all user inputs
- CORS configuration for API endpoints
- Payment webhook signature verification

Use temperature=0 for deterministic output. Group files in batches of 3-8 if needed.

Start by printing the repository tree, then produce all file blocks.
```

## 4) File Manifest / Chunk List

### Explicit Ordered Chunk Manifest:

**Chunk 1 - Project Setup (5 files):**
- README.md
- .env.example
- setup_dev.sh
- docker-compose.yml
- Dockerfile

**Chunk 2 - Backend Core (6 files):**
- backend/main.py
- backend/api/articles.py
- backend/api/translate.py
- backend/models.py
- backend/requirements.txt
- backend/config.py

**Chunk 3 - Backend Services (5 files):**
- backend/services/summarizer.py
- backend/services/translator.py
- backend/services/geo_detector.py
- backend/tasks/celery_worker.py
- backend/cache/redis_helper.py

**Chunk 4 - Frontend Core (6 files):**
- frontend/package.json
- frontend/next.config.mjs
- frontend/app/page.tsx
- frontend/app/article/[slug]/page.tsx
- frontend/app/layout.tsx
- frontend/tsconfig.json

**Chunk 5 - Frontend Components (5 files):**
- frontend/components/language-toggle.tsx
- frontend/components/article-card.tsx
- frontend/components/social-embed.tsx
- frontend/components/ad-slot.tsx
- frontend/lib/api-client.ts

**Chunk 6 - Database & Payments (4 files):**
- supabase/schema.sql
- backend/api/payments.py
- backend/services/payment_gateway.py
- backend/middleware/auth.py

**Chunk 7 - Tests & CI (5 files):**
- tests/backend/test_articles.py
- tests/backend/test_payments.py
- tests/frontend/article.test.tsx
- playwright/e2e.spec.ts
- .github/workflows/ci.yml

## 5) One-Shot vs Chunked Prompts

### One-Shot Prompt (for large models 70B+):
Use the full prompt from section 3 above - paste it entirely and expect complete output.

### Chunked Alternative (for 13B models):

**Initial Chunk Request:**
```
You are an expert Senior Fullstack Engineer. Generate files for ThePulseNow.com news aggregator.
Tech stack: Next.js 14 + FastAPI + Supabase + Redis + Celery + OpenAI.
Output format: //// FILE: <path> then code block.
Generate ONLY these files:
- README.md (setup instructions, architecture overview)
- .env.example (all ENV vars)
- setup_dev.sh (bootstrap script)
- docker-compose.yml
- Dockerfile
Temperature=0. If truncated print: CONTINUE
```

**Subsequent Chunk Pattern:**
```
Continue ThePulseNow.com project. Generate ONLY these backend files:
- backend/main.py (FastAPI app with CORS, rate limiting)
- backend/api/articles.py (CRUD endpoints)
- backend/api/translate.py (translation with Top-10 cap)
- backend/models.py (Pydantic models)
- backend/requirements.txt
Use same //// FILE: format. Temperature=0.
6) Checklist for Pasting Code Back
How to paste generated code for stitching:

If code appears as text blocks: Copy everything including //// FILE: headers
If code appears as UI cards: Copy the code content from each card (not screenshots)
For missing files: Add a line: MISSING: <filepath>
For large files: Split as PART 1 and PART 2 keeping headers
Preserve exact formatting: Don't modify indentation or line breaks
What I'll do when you paste:

Parse all //// FILE: blocks
Identify missing/duplicate files
Generate any missing boilerplate (tsconfig.json, etc.)
Provide exact folder structure
Create corrected versions if syntax errors exist
7) Stitching & Support Offer
I will help you:

Stitch outputs: Parse your pasted code blocks and reconstruct the complete project
Fill gaps: Generate missing config files (tsconfig.json, jest.config.js, etc.)
Fix errors: Provide exact patch diffs for any syntax/import errors
Setup locally: Give step-by-step commands to run everything
Debug issues: Paste any error and I'll provide the exact fix
Ready to proceed?

Copy the model-ready prompt above (section 3)
Paste it into your code LLM (Claude, GPT-4, WizardCoder, Qwen)
Paste the generated output back here
I'll stitch everything and provide running instructions
Would you like me to help with a different product idea, or shall we proceed with implementing ThePulseNow?








Claude
