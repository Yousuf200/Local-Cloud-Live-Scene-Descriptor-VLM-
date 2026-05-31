# Local-Cloud Live Scene Descriptor (VLM)

An automated scene description tool that hooks into a webcam stream (supporting external USB cameras) and utilizes a Vision-Language Model (VLM) to analyze and describe physical environments in real time. 

By leveraging Google Colab's free T4 GPU backend alongside an active Ollama instance, this project processes live visual frames in roughly 1 to 1.5 seconds, avoiding local laptop CPU overhead.

## 🚀 Features
- **Real-Time Sampling:** Automatically intercepts live browser-based webcam frames every 10 seconds.
- **External Camera Support:** JavaScript hardware scanning dynamically binds to external USB webcams over integrated laptop cameras.
- **T4 GPU Accelerated:** Offloads heavy matrix calculations to a cloud GPU for near-instant text generation.
- **Efficient VLM Stack:** Uses `qwen3.5:2b` for lightweight, context-aware, concise scene descriptions.

---

## 🛠️ Setup & Execution Instructions

This project is fully optimized to run within **Google Colab** to make use of free GPU acceleration.

### 1. Environment Initialization
Open a new notebook in Google Colab, change your runtime type to **T4 GPU**, and run the environment initialization cell:

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
