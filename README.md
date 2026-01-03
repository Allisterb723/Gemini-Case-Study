# AI-Assisted Systems Engineering Portfolio

> **Architecting Hardware, Robotics, & Simulation workflows with Google Gemini 1.5 Pro.**

## 📖 Overview
This repository documents a series of technical case studies demonstrating the application of Large Language Models (LLMs) in **Systems Engineering**.

Unlike standard generative AI use cases (text/image generation), this portfolio focuses on **"Reasoning Chains"**—utilizing the model's logic capabilities to debug hardware conflicts, architect industrial firmware, and reverse-engineer proprietary algorithms.

**Core Philosophy:** Using AI as a logic partner to solve "Edge Case" problems where standard documentation fails.

---

## 🛠️ Case Studies

### 1. [Hardware Architecture & Signal Logic](./hardware-architecture/monitor-signal-logic.md)
**The Challenge:** Bypassing OS-level driver locks to force an Ultrawide 120Hz signal through an incompatible active splitter.
* **Key Technique:** EDID Hex Decoding & Timing Override.
* **Outcome:** Restored full bandwidth capabilities on Novatek chipsets via custom CRU injection.

### 2. [Industrial Automation (Robotics)](./industrial-automation/klipper-robotics.md)
**The Challenge:** Converting a consumer 3D printer into a high-voltage industrial unit utilizing distributed computing.
* **Key Technique:** Firmware Physics Optimization & Jinja2 Logic Scripting.
* **Outcome:** Achieved industrial speeds with active resonance compensation (Input Shaping) on a 48V architecture.

### 3. [Algorithmic Optimization (Game Physics)](./algorithmic-logic/forza-physics-exploit.md)
**The Challenge:** Reverse-engineering a proprietary "Performance Index" classification algorithm to optimize a competitive chassis.
* **Key Technique:** Comparative Component Analysis & Constraint Engineering.
* **Outcome:** Successfully "tricked" the classification engine to allow an X-Class hypercar into a lower competitive bracket.

### 4. [Simulation Environment Engineering](./simulation-engineering/assetto-srwe-override.md)
**The Challenge:** Injecting runtime memory overrides to force a triple-screen render resolution (10320x1440) on a locked engine.
* **Key Technique:** Runtime Window Injection (SRWE) & Geometric Projection.
* **Outcome:** Achieved seamless triple-screen rendering without Nvidia Surround, preserving desktop productivity.

---

## 👨‍💻 Technical Stack
* **AI Model:** Google Gemini 1.5 Pro (Vertex AI / Advanced)
* **Hardware Tools:** Custom Resolution Utility (CRU), Input Shapers (ADXL345), Active Signal Hardware.
* **Software Stack:** Klipper, Mainsail, Python, SRWE, Windows Kernel Debugging.

---
*Author: Allister Barnes*
