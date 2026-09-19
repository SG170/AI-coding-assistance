# 🐍 CodeMate — Fine-Tuned AI Coding Assistant

A lightweight AI assistant fine-tuned to help engineering students with Python programming questions and concepts — built as part of the Lunorsoft AI Developer assignment (Option 2: Fine-Tuning).

---

## 📖 Overview

CodeMate is a Python programming tutor built by fine-tuning an open-source language model (TinyLlama-1.1B-Chat) on a curated dataset of programming Q&A pairs. The goal was to create a model that responds more naturally and relevantly to beginner-level Python questions than the untouched base model, using QLoRA — a lightweight, efficient fine-tuning method that makes training feasible on a free-tier GPU.

---

## 📊 Dataset

- **Source:** [`iamtarun/python_code_instructions_18k_alpaca`](https://huggingface.co/datasets/iamtarun/python_code_instructions_18k_alpaca) (Hugging Face)
- **Original size:** 18,612 examples
- **Filtering process:**
  - Removed overly long instructions (>200 chars) and outputs (>500 chars) to keep training focused and efficient
  - Validated every remaining example using Python's `compile()` to catch syntactically broken code (indentation errors, malformed snippets) — this alone removed 33 flawed examples
  - Manually reviewed samples by eye to catch off-topic or mismatched instruction/output pairs
- **Final size:** 225 examples
- **Custom additions:** 8 hand-written Q&A pairs covering conceptual gaps the source dataset lacked — comparisons like `==` vs `is`, common error handling (`ZeroDivisionError`, `IndexError`), and basic OOP concepts (`__init__`)

---

## 🧠 Base Model

**TinyLlama-1.1B-Chat-v1.0**

Chosen deliberately for its small size (1.1B parameters), which made QLoRA fine-tuning practical on a free Google Colab T4 GPU within a tight timeline — while still being large enough to produce coherent, structured responses.

---

## ⚙️ Fine-Tuning Approach

| Setting | Value |
|---|---|
| Method | QLoRA (4-bit quantization + LoRA adapters) |
| LoRA rank (r) | 16 |
| LoRA alpha | 32 |
| Target modules | `q_proj`, `v_proj` |
| Epochs | 3 |
| Batch size | 4 (gradient accumulation: 4) |
| Learning rate | 2e-4 |
| Precision | 4-bit (NF4) |

**Frameworks:** Hugging Face `transformers`, `peft`, `trl` (SFTTrainer), `bitsandbytes`

Only a small fraction of the model's total parameters were actually trained (the LoRA adapters), keeping training fast and memory-efficient while leaving the base model's general knowledge intact.

---

## 🔍 Base vs Fine-Tuned Comparison

Below are direct before/after comparisons on the same questions:
<img width="639" height="257" alt="image" src="https://github.com/user-attachments/assets/be0c2fbf-b85b-44b9-8f4a-43ebf840465b" />
