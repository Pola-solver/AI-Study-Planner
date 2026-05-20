# 📚 AI Study Planner

An interactive, production-ready web application built with Streamlit that helps students dynamically generate optimized, structured study plans. By analyzing user-provided subjects, exam dates, and proficiency levels, the application leverages a locally hosted Large Language Model (LLM) to organize balanced academic schedules.

The system is fully optimized to run efficiently within resource-constrained environments like Kaggle Notebooks utilizing a single GPU.

---

## 🚀 Key Features

- **Blazing Fast Local Inference:** Powered by Microsoft's **Phi-3-mini-4k-instruct** (3.8 Billion parameters), guaranteeing prompt adherence and high-speed schedule generation within seconds.
- **VRAM Optimization (4-bit Quantization):** Integrates `BitsAndBytesConfig` to load the model in 4-bit (`nf4` type with double quantization) and `float16` compute precision. This heavily shrinks the model's footprint to ~2.5GB VRAM, preventing `CUDA Out of Memory (OOM)` errors.
- **Robust Session State Persistence:** Built-in Streamlit `st.session_state` lifecycle management ensures generated tables and raw outputs are cached safely. The data won't disappear if the user triggers a UI re-run or window resizing.
- **Defensive Parsing Engine:** Implements a custom structural bracket-depth tracking algorithm instead of fragile Regex patterns. It isolates, extracts, and validates the raw `{}` JSON tree even if the LLM includes conversational filler or Markdown code blocks (` ```json `).
- **Intelligent Prompt Engineering Rules:** 1. *Interleaved Scheduling:* Prevents consecutive study sessions of the same topic to reduce fatigue and maximize cognitive retention.
  2. *Dynamic Task Rotation:* Automatically rotates through varying pedagogical activities (`قراءة المفاهيم`, `حل تمارين`, `مراجعة شاملة`, `حل امتحانات سابقة`, `مراجعة نهائية`).
  3. *Proportional Durations:* Maps session lengths logically based on task difficulty (e.g., practice exams default to 2.5 hours, while conceptual reviews take 1 hour).
  4. *Guaranteed Coverage:* Ensures every input subject appears a minimum of 4 times, capping total sessions precisely at `len(subjects) * 4`.

---

## 🛠️ Tech Stack

- **Frontend Interface:** Streamlit
- **Machine Learning Hub:** Hugging Face Transformers & Accelerate
- **Quantization Backend:** BitsAndBytes
- **Data Engineering:** Pandas (for parsing JSON structures into dynamic tabular UI components)
- **Networking/Tunneling:** PyNgrok (exposes the local Streamlit port `8501` to a secure, public live link)

---

## 🏃‍♂️ Installation & Deployment Guide

This project is fully automated to run seamlessly inside a **Kaggle Notebook** equipped with a free **GPU T4 x1** accelerator.
