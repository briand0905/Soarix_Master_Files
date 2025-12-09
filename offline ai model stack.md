# Offline AI Workstation Setup Guide  
For: AMD 7800XT (16GB VRAM) + AMD 7800X3D  
Target OS: Windows (preferred) → Pop!_OS fallback  
Goal: Fully offline AI environment for LLMs, images, video, 3D, OCR, and agents.

---

# 1) FULL OFFLINE MODEL STACK  
All models chosen to work **offline**, **run on AMD GPUs**, and support **Soarix** operations.

---

## 🧠 LLMs (Chat, Writing, Research, Coding)

### Core Models
- **Kimi K2** → long-form writing, polished prose  
- **Kimi K1.5** → lightweight drafting  
- **DR-Tulu** → deep reasoning, research, logic  
- **OLMo 3 Base** → efficient general-purpose model  
- **OLMo 3 Reasoning** → small reasoning model  
- **Qwen 3 7B** → chat + coding  
- **Qwen 3 14B** → strong reasoning + creativity  
- **Qwen 3 32B** → offline GPT-4-lite for accuracy  
- **Minimax M2 / GLM 4.6** → coding & debugging  
- **Qwen 3 VL** → multimodal, PDFs, screenshots  

---

## 📄 PDF, Docs & OCR
- **DeepSeek OCR** → extremely accurate offline OCR  
- **Qwen 3 VL** → interpret and summarize PDFs  

---

## 🖼️ Images (Editing, Segmentation, Generation)
- **Qwen Image Edit** → natural language editing  
- **SAM 3** → segmentation and masks  
- **Stable Diffusion XL** → optional image generation  
- **Stable Diffusion 1.5** → very fast generation  

---

## 🧱 3D & Reconstruction
- **SAM 3D** → 2D → 3D mesh reconstruction  
- **AnyLight / LiteNeRF** → lightweight 3D recon on AMD  
- **Instant-NGP CPU fallback** → if GPU fails  

---

## 🎥 Video Generation
- **WAN 2.2 Mini / Quantized** → short video generation  
- **I2V-S / I2V-Base** → image-to-video  
- **RIFE/FILM** → frame interpolation  

---

## 🎤 Speech (Optional)
- **Whisper** → speech → text  
- **F5-TTS / YourTTS** → text → speech  

---

# 2) BUSINESS USE CASE MAPPING  
Simple explanation of how Soarix uses each model.

---

## **Soarix AI (Apps, SaaS, Automations)**
- Qwen 14B/32B → main “brain”  
- DR-Tulu → reasoning  
- Minimax M2 / GLM 4.6 → coding agents  
- Qwen 3 VL → PDF/UI understanding  
- DeepSeek OCR → automation  

**Purpose:** Build powerful offline agents & SaaS tools.

---

## **Soarix Studios (3D, Video, Immersive Design)**
- SAM 3 → segmentation  
- SAM 3D → mesh creation  
- SDXL → concept art  
- WAN 2.2 → video generation  
- RIFE/FILM → smoothing  

**Purpose:** Creative asset pipeline.

---

## **Soarix Media (Marketing)**
- Kimi K2 → long writing  
- Qwen 14B → ads + posts  
- Qwen Image Edit → photo editing  
- SDXL → creative content  
- Whisper/F5-TTS → voice workflows  

---

## **Soarix Publishing**
- Kimi K2 → books  
- DR-Tulu → research  
- OLMo → summarization  
- Qwen VL → reading source docs  

---

## **Soarix Nexus (R&D)**
- All reasoning models  
- Vision + 3D + video models  

**Purpose:** Experimentation + innovation.

---

## **Internal Tools**
- DeepSeek OCR → contracts  
- Qwen VL → screenshots/PDFs  
- Minimax M2 → coding assistant  
- OLMo Reasoning → lightweight logic  

---

# 3) OS Decision Summary

### **Windows Pros**
- Easiest  
- LM Studio works perfectly  
- ComfyUI works (DirectML)

### **Windows Cons (AMD-specific)**
- Some 3D/video models do not run  
- Slower for heavy workloads  
- Mixed DirectML support

---

### **Pop!_OS Pros**
- Best ROCm support  
- Maximum AMD performance  
- All models (LLM, image, video, 3D) work reliably

### **Pop!_OS Cons**
- Learning curve  
- Some manual installs

---

# 4) What is AllenAI (AI2)?  
AI2 = Allen Institute for AI  
- Nonprofit  
- Open-source  
- High-quality research  
- They created **OLMo** series  
- 100% free  
- Excellent for offline use  

Their models are already included:
- **OLMo 3 Base**  
- **OLMo 3 Reasoning**

---

# 5) Current Decision Logic

The plan is:

1. **Start with Windows** (easiest path, works for ~80% use cases).  
2. If video or 3D models fail → **switch to Pop!_OS** for full AMD acceleration.

---

# 6) NEXT QUESTION  
**Which OS do you want to proceed with first?**  
- Windows (recommended first attempt)  
- Pop!_OS (maximum performance)

