# Urdu OCR — Extracting Text from Urdu Images using Fine-Tuned TrOCR

A deep learning model that reads Urdu text from images — built to solve a problem that barely has solutions in the AI world.

## Why This Matters

Urdu is written in **Nastaliq script** — a cursive, right-to-left writing system where characters change shape depending on their position in a word. Traditional OCR engines like Tesseract fail on it. This means millions of historical Urdu documents, newspapers, and handwritten records remain unsearchable and undigitized.

This project builds an OCR tool specifically for Urdu, using modern transformer architecture instead of rule-based approaches.

## Live Demo

> **Note on Deployment:** Hugging Face recently moved server-side Gradio SDK to a paid tier. The interactive demo was built, tested, and verified within Google Colab (screenshots in notebook).

| Link | Description |
|------|-------------|
| 📓 [Colab Demo Notebook](https://colab.research.google.com/github/Noisy77/urdu-ocr-codesaviours-si26-bilal/blob/main/week5/SI26-Week5-Colab.py) | Interactive notebook with live demo |
| 🤗 [HuggingFace Space](https://huggingface.co/spaces/Noisy77/urdu-ocr-codesaviours-si26-bilal) | HuggingFace Space repository |
| 🎥 **Loom Demo** | *Coming soon* |

## How It Works

The model uses **TrOCR** (Transformer-based OCR) by Microsoft — it combines:
1. **Vision Transformer (ViT)** — "looks" at the image and extracts visual features
2. **Text Transformer (decoder)** — "writes" the text character by character based on what it saw

We fine-tuned this on a custom dataset of 403 Urdu images, teaching the model to map Nastaliq script patterns directly to digital Urdu characters.

## Results

| Metric | Value |
|--------|-------|
| Training Loss | 19.21 → **0.07** (3 epochs) |
| Learning Capability | ✅ Strong convergence |
| Partial Recognition | ✅ e.g., predicting `ح` for `حرف` |

> **What I'd improve:** Swap the decoder tokenizer from English RoBERTa to a multilingual model (`xlm-roberta-base` or custom Urdu sentencepiece tokenizer) to fully decode the characters the model is visually identifying.

## Dataset

**403 images** compiled from multiple sources:

| Source | Count | Description |
|--------|-------|-------------|
| News Screenshots | 31 | BBC Urdu, Dawn Urdu, Jang |
| Isolated Characters | 100 | RAVI dataset |
| Handwritten Characters | 273 | Cursive handwriting samples |

Backgrounds: clean white, digital interfaces, and paper scans.

## How to Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/Noisy77/urdu-ocr-codesaviours-si26-bilal.git
cd urdu-ocr-codesaviours-si26-bilal

# 2. Install dependencies
pip install -r week5/hf_space/requirements.txt

# 3. Download model files from Google Drive and place in week5/hf_space/
#    Files needed: config.json, generation_config.json, pytorch_model.bin, tokenizer files

# 4. Launch the Gradio app
python week5/hf_space/app.py
# Opens at http://localhost:7860
```

```

## Project 2 — Code Switching Language Identification

Built alongside this OCR project, the second project tackles **Roman Urdu + English code-switching** — identifying which words in a mixed-language sentence are Urdu and which are English.

| Component | Link |
|-----------|------|
| 📊 Dataset (161 sentences, 1658 labels) | [HuggingFace Dataset](https://huggingface.co/datasets/Noisy77/code-switching-codesaviours-si26-bilal) |
| 🤖 Trained Model (XLM-RoBERTa) | [HuggingFace Model](https://huggingface.co/Noisy77/code-switching-model-si26-bilal) |
| 💻 GitHub Repo | [code-switching-codesaviours-si26-bilal](https://github.com/Noisy77/code-switching-codesaviours-si26-bilal) |

---

Built by **Bilal** | Code Saviours ML/AI Internship — Batch SI-26 | 2026
