# Fine-Tuned AI Coding Assistant

## Overview
A lightweight AI assistant fine-tuned to help engineering students with Python programming questions, built using QLoRA on TinyLlama-1.1B.

## Dataset
Source: iamtarun/python_code_instructions_18k_alpaca (Hugging Face). Filtered from 18,612 to 225 examples — removed overly long entries and syntactically invalid code using Python's compile(). Added 8 hand-written Q&A pairs for conceptual gaps.

## Base Model
TinyLlama-1.1B-Chat-v1.0 — small enough for QLoRA fine-tuning on a free Colab T4 GPU.

## Fine-Tuning Approach
QLoRA (4-bit quantization + LoRA adapters). LoRA config: r=16, alpha=32, target modules q_proj/v_proj. 3 epochs, batch size 4, learning rate 2e-4. Built with Hugging Face transformers, peft, trl.

## Base vs Fine-Tuned Comparison
[PASTE YOUR OUTPUT FROM STEP 2 HERE]

## Demo
[PASTE YOUR GRADIO LINK HERE] (note: link expires ~72hrs after generation)

## How to Run
Open the Colab notebook (linked below) and run all cells in order.
Notebook: [PASTE YOUR COLAB SHARE LINK HERE]

## AI Tools Used
Used Claude (Anthropic) to help plan the fine-tuning pipeline, debug library errors, and structure this README. All code was run and verified personally.

## Limitations & Future Work
Small dataset (225 examples) limits depth of improvement. Model can produce unrelated output for questions phrased differently from training data. With more time: larger dataset, more epochs, hyperparameter tuning.
