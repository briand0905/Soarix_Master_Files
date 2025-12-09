# ðŸ§  Soarix Executive + Base System Setup Guide

## Overview
This document captures the detailed plan for structuring and running Soarix Solutions as a multi-branch AI-first company. It includes both the **Build System** (technical base for websites, apps, SaaS) and **Executive Operator System** (business and operations management via AI).

---

## Key Sections
- Soarix Base System (for building products)
- Executive Operator Prompts (for running each branch)
- Executive Dashboard Controller (for cross-branch management)
- General Prompt Builder (for client & new product ideation)
- Chat Structure Plan (for ChatGPT/Claude + Minimax/Ollama)
- Tooling & Environment Plan (for Pop!_OS & Windows)
- Offline & Online AI Configuration Strategy
- Next Steps for Implementation

---

## Summary of Architecture

| Layer | Function | Tools |
|-------|-----------|--------|
| **Build Layer** | Builds websites, SaaS, and apps using the Soarix Base System | Minimax M2, GLM 4.6, Ollama, LM Studio |
| **Executive Layer** | Runs operations, clients, reports, and revenue generation | ChatGPT, Claude |
| **Dashboard** | Central management for all branches | ChatGPT (Dashboard Controller Prompt) |

---

## Branches & Prompts

| Branch | Build Prompt | Executive Prompt |
|---------|----------------|------------------|
| Soarix Solutions | Uses Base System | Corporate Operator |
| Soarix Media | Uses Base System | Marketing Operator |
| Soarix AI | Uses Base System | SaaS/Product Operator |
| Soarix Studios | Uses Base System | Creative Operator |
| Soarix Nexus | Uses Base System | R&D Operator |

---

## Offline/Online AI Setup Plan

### Online Stack
- **Builder AIs:** Minimax M2 / GLM 4.6
- **Operator AIs:** ChatGPT / Claude

### Offline Stack
- **Core tools:** Ollama + LM Studio
- **Models to download:** GPT-OSS-120B, Llama 2/3, Mistral 7B/13B, Stable Diffusion, Whisper/Coqui
- **Storage:** Backblaze B2 + MinIO (dev)

---

## Implementation Phases
1. **Set Up Dev Environment (Pop!_OS & Windows)**  
   Includes Dockerized stack, MongoDB, Redis, n8n, Grafana, etc.

2. **Install & Configure Offline AI (Ollama / LM Studio)**  
   Download and quantize models with commercial-safe licenses.

3. **Load Soarix Base System Prompt**  
   Pin in builder AIs (Minimax / GLM / Ollama).

4. **Load Executive Prompts (per branch)**  
   Pin in ChatGPT / Claude, one per chat.

5. **Launch Dashboard Controller**  
   Use for company-wide synchronization, reporting, and KPI tracking.

6. **Start Operations & Build Cycle**  
   Executive Prompts guide project flow, Base System handles builds, Dashboard oversees everything.

---

## Next Actions
- Choose **Offline-First** or **Hybrid-Cloud** deployment model.
- Request detailed step-by-step runbooks when ready by saying:  
  **â€œShare the steps.â€**

---

*Generated and compiled automatically by GPT-5 (Soarix Project AI Partner).*
