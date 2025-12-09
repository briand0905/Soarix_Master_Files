# 🎓 Two-Way Voice Tutor AI Guide

> A complete no-code build guide for a multilingual, role-based AI tutor with voice interaction, RAG, labs, quizzes, and secure upgrade path.  
> **Author**: [Your Name]  
> **Date**: December 4, 2025  
> **Status**: MVP Built • No-Code • Ready to Upgrade

---

## 🎯 Project Vision

Build a **two-way voice + optional video AI tutor** that:
- 🗣️ Listens and speaks in **15+ languages** (auto-detect + reply)
- 📚 Teaches **role-based IT tracks** (Pentester, Data Scientist, etc.)
- 🔍 Uses **RAG** (Retrieval-Augmented Generation) for accurate lessons
- 🧪 Offers **labs, quizzes, progress tracking, flashcards**
- 🛡️ Is **safe for security topics** (defensive only; offensive → simulated labs)
- 🎨 Has **clean web + mobile UI** with:
  - Dark mode (default)
  - Light mode: white background + light blue (`#3B82F6`) accent
- 🔁 Is **upgradeable** from no-code → low-code → full stack

---

## 🧰 What You Need (Prerequisites)

### Hardware
- ✅ PC: Ryzen 7 7800X3D + Radeon 7800XT
- ✅ USB mic or headset (for clear STT)
- ✅ Optional: External SSD (for VM labs)

### Accounts & Services
- ✅ [OpenAI](https://openai.com) – GPT-5 access
- ✅ [ElevenLabs](https://elevenlabs.io) – Multilingual TTS
- ✅ [TryHackMe](https://tryhackme.com) / [HackTheBox](https://www.hackthebox.com) – Free lab accounts
- ✅ Google/Microsoft account – For sign-up ease

### Software
- ✅ Chrome browser
- ✅ PDF reader
- ✅ VS Code (optional, for future upgrades)

---

## 🛠️ Recommended No-Code Platform: Voiceflow

🔗 [https://www.voiceflow.com](https://www.voiceflow.com)  
✅ Free tier available  
✅ Supports: STT, TTS, RAG, custom system prompts, web chat embed

---

## 🚶 Step-by-Step Setup (One Step at a Time)

### ✅ Step 1: Sign Up for Voiceflow
- Go to [https://www.voiceflow.com](https://www.voiceflow.com)
- Click “Sign Up”
- Use your Google account or email
- Select **Free Plan** (no credit card needed)
- Confirm: You see the **dashboard**

👉 **Confirm**: Done

---

### ✅ Step 2: Create a New Voice Assistant Project
- In dashboard, click **“Create New Project”**
- Choose **“Voice Assistant”**
- Name: `IT Tutor - Pentester Track`
- Click **Create**
- Confirm: You’re inside the editor

👉 **Confirm**: Done

---

### ✅ Step 3: Set the Master Tutor System Prompt
- In project → **Settings → System Prompt**
- Paste the following:

```text
You are a multilingual, voice-first tutoring agent for IT and general education. Teach in small spoken chunks (~6–10 seconds) unless asked for more. Use a 3-part structure for spoken replies:
1) 1–2 plain sentences,
2) 1 analogy or tiny example,
3) 1 quick check question or next step.

Auto-detect the user's language and reply in it. Support modes: Teach, Quiz, GuidedPractice, LabCoach, Review.

For cybersecurity, provide only defensive, legal, lab-safe guidance; refuse or redirect any harmful/illegal requests (e.g., "I can't help with real-world attacks, but I can show you how to defend in a lab like TryHackMe").

When a user asks a question:
(a) Search your knowledge base (RAG) and include up to 2 short citations,
(b) Then answer conversationally,
(c) Offer a 1-step lab or a 1-question quiz.

Keep jargon minimal. If used, define in one plain line. Provide bilingual glosses on request.

Intents (if available): set_mode(mode), set_language(code), search_docs(query), save_progress(summary), show_diagram(topic).
```

👉 **Confirm**: Prompt saved

---

### ✅ Step 4: Connect Speech-to-Text (STT)
- Go to **Integrations → Speech-to-Text**
- Choose: **OpenAI Whisper** (recommended)
- Enable: **Auto-detect language**

👉 **Confirm**: STT connected

---

### ✅ Step 5: Connect Text-to-Speech (TTS) via ElevenLabs
- Sign up at [https://elevenlabs.io](https://elevenlabs.io) (Free tier)
- Get API key: Profile → **API Key**
- In Voiceflow: **Integrations → Text-to-Speech → ElevenLabs**
- Paste API key
- Choose a voice (e.g., "Rachel" for English)

👉 **Confirm**: TTS working

---

### ✅ Step 6: Download Seed PDFs for RAG
Download these free resources:

| Topic | Source |
|------|--------|
| Windows Basics | [Microsoft IT Docs](https://learn.microsoft.com/en-us/windows/) → Save as `windows-basics.pdf` |
| Networking Fundamentals | [Cisco NetAcad - Intro to Networking](https://www.netacad.com/courses/networking/introduction-networking) → Free course → Download materials |
| OWASP Top 10 | [OWASP Top 10 2021 PDF](https://owasp.org/www-project-top-ten/) |

Save all to your desktop.

👉 **Confirm**: PDFs downloaded

---

### ✅ Step 7: Upload PDFs to Knowledge Base (RAG)
- In project → **Knowledge Base** → Click “+ Add Document”
- Upload:
  - `windows-basics.pdf`
  - `networking-fundamentals.pdf`
  - `owasp-top10-2021.pdf`
- Wait for indexing (1–2 minutes)

👉 **Confirm**: RAG documents uploaded

---

### ✅ Step 8: Design Core Conversation Flow

#### Block 1: Welcome + Language Detect
> "Hi! I'm your IT tutor. Say your goal — like 'Teach me Windows basics' or 'Help me become a pentester.'"

Set to **listen for speech**, auto-detect language.

#### Block 2: Intent Detection
Enable detection for:
- "Teach me [topic]"
- "Quiz me on [topic]"
- "Start pentester roadmap"
- "Switch to [language]"

#### Block 3: Teach Mode Example
> "Think of Windows like a filing cabinet. Folders are drawers, files are documents.  
> Lab: Press Win+R, type 'cmd', then type 'dir'.  
> What do you see?"

#### Block 4: Quiz Mode
> "Quick check: What does 'dir' do?  
> a) Deletes files  
> b) Lists files and folders ✅  
> c) Reboots the PC"

#### Block 5: Lab Coach
> "Want to try a real lab? Go to:  
> https://tryhackme.com/room/passwordattacks"

👉 **Confirm**: Flow designed

---

### ✅ Step 9: Add Safety Guardrails

#### Refusal Rule for Harmful Requests
If user says: *"How do I hack Facebook?"*  
→ Respond:

> "I can't help with real-world attacks — that’s illegal and unethical. But I can show you how to defend systems in a safe lab. Want to try a TryHackMe room on password security?"

Then link: `https://tryhackme.com/room/passwordattacks`

👉 **Confirm**: Safety rule added

---

### ✅ Step 10: Add Basic Progress Tracking

Use variables:
- `current_topic = "Windows Basics"`
- `labs_completed = 1`
- `quizzes_passed = 1`

After each success:
> "Great job! You're 10% into the Pentester roadmap."

👉 **Confirm**: Progress tracking added

---

### ✅ Step 11: Customize UI (Dark + Light Mode)

In **Share → Web Chat → Customize**:

#### Dark Mode (Default)
- Background: `#0E1117`
- Text: `#E6EDF3`
- Accent: `#3B82F6`

#### Light Mode
- Background: `#FFFFFF`
- Text: `#0F172A`
- Accent: `#3B82F6`

👉 **Confirm**: UI colors set

---

### ✅ Step 12: Test Your Tutor

Say into mic:
> “I’m a beginner. Teach me Windows basics in English. Use analogies, give me a lab, and quiz me.”

Expected response:
> "Think of Windows like a filing cabinet. Folders are drawers, files are documents.  
> Lab: Press Win+R, type 'cmd', then type 'dir'.  
> Quick quiz: What does 'dir' do?  
> a) Deletes files  
> b) Lists files and folders ✅  
> c) Reboots the PC"

👉 **Confirm**: Working!

---

## 🔐 Security & Ethics Checklist

| Risk | Mitigation |
|------|-----------|
| PII Leakage | Disable logging; don’t store personal data |
| Prompt Injection | Use strict system prompt; block harmful intents |
| Unauthorized Access | Use 2FA on Voiceflow & ElevenLabs |
| Malicious Output | Enforce refusal rules for hacking/exploits |
| RAG Poisoning | Only upload trusted, vetted PDFs |

✅ All mitigations applied.

---

## 🔄 Upgrade Path (Future-Proof)

| When You're Ready | Next Step |
|-------------------|----------|
| Want mobile app? | Use Voiceflow embed or build React Native app |
| Want more control? | Migrate to **Next.js + FastAPI** (Low-Code) |
| Want video avatar? | Integrate **HeyGen** or **DeepBrain AI** |
| Want local RAG? | Switch to **Pinecone** or **pgvector** |
| Want multi-user? | Add auth with **Supabase** or **Firebase** |

---

## 📎 Ready-to-Paste Prompts

### A. Master Tutor System Prompt
(See Step 3)

### B. Curriculum Designer Prompt
```text
You are a role-based curriculum designer. Produce a complete roadmap for: Pentester.
Include: 8-week path, weekly topics, prerequisites, 3 labs (with setup steps), 3 projects, 15 quiz questions.
Format as JSON.
```

### C. Content Ingestor Prompt
```text
Act as a content ingestion assistant. Given a folder of PDFs, output:
1. CSV manifest: filename, title, language, role_tags, summary
2. Python script to extract text, chunk, embed (OpenAI), and upsert to pgvector.
Include pip packages and docker-compose for Postgres + pgvector.
```

### D. QA / Safety Test Prompt
```text
Generate 30 test cases for an AI tutor:
- STT accuracy
- Language detect
- RAG citation correctness
- Refusal to answer harmful requests
- UI dark/light toggle
Include expected result and severity.
```

---

## 🚀 Launch & Share

- Get embed link: **Share → Web Chat → Copy Link**
- Share: “Try my AI IT tutor: [your-link]”
- Collect feedback from friends/test users

---

## 🏁 Final Notes

You now have a **fully functional, secure, no-code AI tutor** that:
- Speaks and listens in multiple languages
- Teaches real IT skills with labs and quizzes
- Uses accurate RAG sources
- Looks professional
- Is safe and ethical

And when you're ready to go further — **low-code or full stack** — this guide scales with you.

🎯 **Next Phase Suggestions**:
- Generate full JSON roadmap for Pentester
- Build Next.js frontend template
- Automate PDF ingestion pipeline
- Add spaced repetition flashcards

Let me know which one you'd like next!
```

---

