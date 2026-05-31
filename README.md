# Accessibility-Focused Local-Cloud Live Scene Descriptor (VLM)

An automated assistive tool designed for users with visual impairments. It captures live video streams from external USB webcams and utilizes a Vision-Language Model (VLM) to analyze physical environments, printing textual scene descriptions and reading them aloud via text-to-speech (TTS) in near real time.

By combining Google Colab's cloud T4 GPU backend for image evaluation and the HTML5 Speech Synthesis Web API for audio presentation, this project operates smoothly without requiring a high-end local GPU.

## 🚀 Features
- **Real-Time Assistive Audio:** Automatically outputs clean text-to-speech audio updates summarizing changes in the physical environment.
- **External Camera Priority:** Built-in JavaScript device scanner automatically searches for and locks onto external USB webcams.
- **Optimized Latency:** Utilizes `qwen3.5:2b` to generate ultra-fast, descriptive, context-aware 1-sentence summaries in ~1.2 seconds.
- **Zero Overhead on Laptop:** Offloads intensive AI inference steps safely to a cloud T4 engine.

---

## 🛠️ Setup & Execution Instructions

This repository runs efficiently directly within web browser instances via **Google Colab**.

### 1. Environment Initialization
Open a new notebook in Google Colab, shift your hardware runtime type to **T4 GPU**, and execute the environment configuration block:

```python
# Install backend dependencies and pull the lightweight vision model
!sudo apt update && sudo apt install -y zstd pciutils
!curl -fsSL [https://ollama.com/install.sh](https://ollama.com/install.sh) | sh

import subprocess
import time

print("Booting local Ollama server inside cloud space...")
subprocess.Popen(["ollama", "serve"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
time.sleep(5) 

!ollama pull qwen3.5:2b
!pip install ollama opencv-python
