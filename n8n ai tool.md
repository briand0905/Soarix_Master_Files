# 🧠 Soarix x n8n + AI Training — Chat Archive

---

## 🗓️ Date: December 2025  
## 🧑‍💻 Instructor: GPT-5 (Soarix AI Orchestrator)  
## 🧑‍🎓 Trainee: Brian (Founder, Soarix Solutions)  
## 📘 Topic: n8n + AI Automation — Foundational Training

---

### 🧩 MODULE 1 – Introduction & Setup

#### 🧠 THEORY TIME

**What is n8n?**

n8n (pronounced “n-eight-n”) is like your **automation playground** 🎡.  
It connects different apps — Gmail, Google Sheets, Notion, ChatGPT, etc. —  
and lets them talk to each other automatically.

Imagine:  
> “When I get an email 📩 → copy it to Google Sheets 📋 → summarize it with ChatGPT 🤖 → wait for my approval 🚦 before replying.”

That’s a workflow! n8n helps you build this without coding — just drag, drop, and connect boxes called **nodes** 🧱.

---

#### 🧱 n8n = LEGO for Automation 🧱
Each **node** = one LEGO block.
Each block does one small job (send email, fetch data, generate text, etc.).
You snap them together to form your automation robot 🤖.

---

#### 🌍 Why It’s Special
| Feature | Easy Explanation |
|----------|------------------|
| 🧩 **Visual Builder** | You drag and drop nodes instead of writing code. |
| 🌐 **Connect Anything** | Works with 300+ apps (Google, Notion, GitHub, Slack, etc.). |
| 🧠 **AI Friendly** | Plays nicely with ChatGPT, Claude, Gemini, or your own AI. |
| 🔐 **Your Data = Your Control** | You can host it yourself or use the official cloud safely. |

---

#### ☁️ n8n Cloud vs 🖥️ Local Installation

| Version | Description | For Who |
|----------|--------------|----------|
| ☁️ **n8n Cloud** | Run from browser. No install, no coding. | ✅ Beginners |
| 🖥️ **Local n8n** | Install it yourself. Full control, privacy. | 🔒 Advanced users |

💬 **Recommendation:**  
Start with **n8n Cloud** (it’s free & easy). Once confident, we’ll migrate to your local setup using Docker (so you control everything).

---

#### ⚖️ T&Cs & Privacy Reminder
Before using:
- Read **https://n8n.io/legal/terms** & **https://n8n.io/legal/privacy**.
- Understand how your data flows.
- Never share sensitive info without encryption.
- Later, we’ll secure local workflows with environment variables 🔐.

---

#### ✅ Checkpoint 1
You now know:
- What n8n is 🧩  
- Why it’s useful 💡  
- Which version to start with ☁️  

Next: you’ll pick your setup type.

---

### 🚀 OJT (On-the-Job Training)

**Step 1 – Choose Your Setup**
1. Go to **https://app.n8n.cloud/signup**  
2. Create a free account (use your Soarix email if available).  
3. Log in to your dashboard — you’ll see a “New Workflow” button.  

🧭 Expected: A whiteboard-like screen with a plus (+) icon to add nodes.

---

**Step 2 – Build Your First Workflow**

Goal: “Press a button → Send myself a message.”

1. Click the **+ icon** ➕  
2. Choose **‘Manual Trigger’** (this is your start node).  
   🧩 It means: “Start this workflow when I click run.”

3. Click **+ Add Node** → choose **‘Set’** node.  
   - Set → “Text Message”
   - Key: `message`
   - Value: `Hello from n8n! 🚀`

4. Add another node → **‘Webhook Response’** (optional, just for practice).  
   - It shows you the message result.

5. Click **Execute Workflow** ▶️  

You should see `Hello from n8n! 🚀` appear.

🎉 Congrats! You’ve just made your first automation robot.

---

#### 🔒 Safety Reminder:
Never connect APIs or external services without your manual **“AUTHORIZATION NEEDED 🚦”** step.  
We’ll build that next, once you connect your first app.

---

✅ **Checkpoint 2:**  
Did you successfully run your first workflow?  
If yes, we’ll move to **Module 1.5 – Coding Basics for Non-Coders (Lego Style)** next.

If not, tell me where you’re stuck and I’ll fix it step-by-step with you.

---

## 📚 Next Module Preview

### **MODULE 1.5 – Coding Basics (Lego Style 🧱)**

🧠 **Theory:**
- Understand what “variables” and “functions” mean in plain English.  
- Think of “variables” as boxes 🧺 that store info.
- “Functions” are robots 🤖 that do things with that info.

💪 **OJT:**
- Learn to use **Set Node** and **Function Node** in n8n.
- Build a small workflow that prints:
  > “Hello, Batman!”  
  …but changes “Batman” to your own name using a variable.

---

## 📁 Reference Files (Uploaded)

- **Dev Environment Setup.pdf** — foundation guide for Soarix ecosystem tools:contentReference[oaicite:0]{index=0}  
- **Soarix System Prompt V3.docx** — defines Orchestrator’s principles, communication style, and build quality standards:contentReference[oaicite:1]{index=1}  

---

## 🧭 Executive Insight

By learning n8n now:
- You’re creating Soarix’s internal autom
