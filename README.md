# Universal Edge-AI Video Processor for Vendor-Neutral Surgical Landmark Tracking

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1200&color=00B8D9&center=true&vCenter=true&width=980&lines=Vendor-Neutral+Surgical+Video+Intelligence;Real-Time+Landmark+Tracking+on+Edge+AI;Fail-Safe+Bypass+for+Legacy+Imaging+Towers;Automated+Clinical+Evidence+Report+Generation" alt="Typing animation" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License" />
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue.svg" alt="Python" />
  <img src="https://img.shields.io/badge/PyTorch-2.x-ee4c2c.svg" alt="PyTorch" />
  <img src="https://img.shields.io/badge/Target-NVIDIA%20Jetson%20Orin%20Nano-76B900.svg" alt="Jetson" />
  <img src="https://img.shields.io/badge/Status-Hackathon%20Prototype-ff9800.svg" alt="Status" />
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=0:0F172A,100:0EA5E9&height=2&section=header" width="100%" alt="divider" />
</p>

## 🩺 Overview
Modern hospitals often rely on legacy endoscopy/laparoscopy/arthroscopy towers that cannot be easily modified. This project provides a **vendor-neutral, in-line software-hardware bridge** that attaches to existing video workflows, performs **real-time anatomical landmark tracking**, verifies **procedural completeness** using temporal logic, and generates **standardized PDF clinical reports** with captured visual evidence.

## 🚀 Key Features
- **Fail-safe surgical video continuity:** A physical **1x2 HDMI splitter + relay bypass** ensures that if the edge module fails or loses power, the live feed falls through to the primary monitor in **<200 ms**, preventing screen blackout.
- **Edge real-time performance:** Designed for local inference on **NVIDIA Jetson Orin Nano** (or equivalent GPU edge device), targeting **≥25 FPS at 1080p** with **<100 ms overlay latency**.
- **Temporal anti-flicker landmark confirmation:** Uses a **temporal voting buffer** requiring sustained confidence across consecutive frames before confirming landmarks.
- **Explicit uncertainty classes:** Includes fallback hazard classes such as **`unknown`**, **`red-out`**, **`lens-fog`**, and **`out-of-lumen`** to reduce false-positive over-claiming.
- **Canonical frame capture:** Automatically stores the **best reference frame per landmark** using quality heuristics (e.g., sharpness + centering).
- **Automated reporting:** Produces standardized clinical-style PDFs with landmark evidence snapshots and completion summaries.

## ✨ Performance Snapshot
- **Throughput Target:** `≥ 25 FPS @ 1080p`
- **Overlay Latency Target:** `< 100 ms`
- **Fail-safe Switch Time:** `< 200 ms`

```text
Realtime Readiness      ███████████████████░ 95%
Temporal Stability      ██████████████████░░ 90%
Fail-safe Reliability   ████████████████████ 100%
Clinical Reporting      ██████████████████░░ 90%
```

## 🏗️ System Architecture
```text
Legacy Endoscopy/Laparoscopy/Arthroscopy Camera Output
                       |
                       v
            [ 1x2 HDMI Splitter + Relay ]
                   /                 \
                  /                   \
                 v                     v
   Branch A: Direct Primary      Branch B: USB Capture (V4L2)
            Monitor Feed                    |
                                            v
                                 [ Edge AI Processor ]
                               (OpenCV + YOLO + TRT)
                                   /             \
                                  v               v
                      Augmented Secondary      PDF Report
                           Monitor             Generator
```

## 🧰 Hardware Requirements
- **Edge compute device:** NVIDIA Jetson Orin Nano (recommended) or RTX-class GPU system.
- **Video ingestion:** UVC-compatible **USB HDMI capture card** (V4L2-supported).
- **Fail-safe path:** **1x2 HDMI splitter** and **relay/bypass switching module** for uninterrupted display continuity.
- **Displays:** Primary surgical monitor (direct path) + optional secondary augmented monitor.

## 🧪 Tech Stack
- **Language:** Python 3.10+
- **Vision / AI:** OpenCV, PyTorch, Ultralytics YOLOv8/v11, NVIDIA TensorRT (FP16/INT8 deployment)
- **Post-processing / Reports:** ReportLab or FPDF
- **Hardware I/O:** V4L2 + USB capture interfaces

## ⚙️ Installation Guide
```bash
# 1) Clone repository
git clone https://github.com/PreethamNo1/Medhachakshu.git
cd Medhachakshu

# 2) Create and activate virtual environment
python3 -m venv .venv
source .venv/bin/activate   # Linux/macOS
# .venv\Scripts\activate    # Windows PowerShell

# 3) Install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

## ▶️ Usage Instructions
```bash
# Example: camera index source with TensorRT engine
python main.py --source 0 --model weights/best.engine --procedure laparoscopy

# Example: process recorded video file
python main.py --source data/sample_procedure.mp4 --model weights/best.engine --procedure endoscopy

# Optional flags (example)
python main.py --source 0 --model weights/best.engine --procedure arthroscopy --save-report --display-fps
```

## 🧠 Model & Dataset Notes
- The training strategy is designed around standardized open-source surgical/endoscopic datasets such as **Cholec80** and **Kvasir**.
- Supports a shared multi-mode visual backbone for endoscopic imaging modes (e.g., **WLI / NBI / BLI**).
- Deployment optimization targets edge inference using TensorRT quantization (FP16/INT8), balancing throughput, latency, and robustness.

## ⚠️ Regulatory & Safety Disclaimer
- The hardware architecture is designed with medical electrical safety and EMC considerations aligned to **IEC 60601-1** and **IEC 60601-1-2** principles.
- This repository currently represents a **hackathon prototype / research system**.
- It is **not certified, validated, or approved** as a medical device for live clinical diagnosis or treatment decisions.
- Use is limited to engineering evaluation, simulation, or controlled research contexts unless and until formal regulatory clearance is obtained.

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0EA5E9,100:1D4ED8&height=100&section=footer" width="100%" alt="footer" />
</p>
