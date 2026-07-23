# Urdu OCR Project | Code Saviours SI-26 | Bilal

## Project Overview

This project focuses on building an Optical Character Recognition (OCR) system specifically designed for Urdu text. Over the course of 5 weeks, we will collect data, preprocess images, build a dataset pipeline, fine-tune a TrOCR model, and deploy the final solution.

---

## Research Summary

### What is OCR (Optical Character Recognition)?

OCR (Optical Character Recognition) is a technology that converts images of text — such as scanned documents, photographs of signs, or screenshots — into machine-readable text data. It works by analysing the shapes, patterns, and structures of characters within an image and mapping them to known characters in a given language. OCR is widely used in digitising printed documents, automating data entry from forms, and making text searchable within image-based files like PDFs. Modern OCR systems leverage deep learning and computer vision techniques, such as convolutional neural networks (CNNs) and transformer-based models, to achieve high accuracy even on complex or noisy images.

### Why is Urdu OCR harder than English OCR?

Urdu OCR is significantly more challenging than English OCR for several reasons. First, Urdu is written right-to-left (RTL) and uses a **cursive, connected script** — characters change shape depending on their position in a word (initial, medial, final, or isolated), which dramatically increases the complexity of character recognition. Second, Urdu uses the **Nastaliq** writing style for most printed and handwritten text, which is diagonal and has characters stacked at varying heights, unlike the linear Naskh script used in Arabic OCR — this makes line segmentation and character boundary detection extremely difficult. Third, Urdu contains numerous **diacritical marks** (dots and other markers above/below characters) that distinguish otherwise identical base shapes, and these small details are easily lost in low-resolution or noisy images. Finally, the availability of large, well-labelled Urdu OCR datasets is far more limited compared to English, which hampers model training.

### Real-World Use Cases for Urdu OCR

1. **Digitising historical Urdu documents and books**: Pakistan and South Asia have a vast literary heritage in Urdu — millions of books, newspapers, court records, and government documents exist only in printed or handwritten form. An effective Urdu OCR system could digitise these archives, making them searchable, preservable, and accessible to researchers and the general public.

2. **Automating data extraction from Urdu forms and ID documents**: Government offices, banks, and institutions in Pakistan frequently deal with forms, CNIC cards, and documents written in Urdu. An OCR system could automatically extract names, addresses, and other fields, dramatically reducing manual data entry effort and errors while speeding up administrative processes.

---

## Why We Need a Better Model

## Gap Analysis — Tesseract vs Actual Text

### Comparison Table

| Image | Actual Text | Tesseract Output | What Went Wrong |
|-------|------------|------------------|-----------------|
| news_screenshot_001.png | ایران کی امریکی حملوں میں 50 افراد کی ہلاکت کی تصدیق | میں کسی کی ڈکٹیشن نہیں لوں گا... بحران جب صدر اور وزیر ا | Picked up wrong headline, cut off mid-word |
| news_screenshot_002.png | فیچر اور تجزیے | فیچر اور تجزیے ✓ (but rest garbled: 1" --× ) | Got heading right but gibberish symbols mixed in |
| news_screenshot_003.png | پاکستان میں ڈیزل 31.05 اور پٹرول 5.44 روپے مہنگا | بالواسطہ ہراسانی پر پانچ لاکھ روپے... | Completely different text detected — wrong region of page |
| news_screenshot_004.png | پاکستان کے خلاف 365 رنز کی ناقابل شکست اننگز | 75 7۸ہ اخدتدننت... 53077123157773 | Mostly garbled numbers and broken characters |
| news_screenshot_005.png | زیارت حملے کے خلاف دھرنا ختم | کشمیر کی وادی ہماری ہے... | Read a different article entirely |

### Summary

**Tesseract fails on Urdu because** it was primarily designed for Latin-based scripts and struggles with the fundamental characteristics of Urdu text. The Nastaliq script's cursive, connected nature means characters flow into each other and change shape based on position — Tesseract's segmentation algorithms cannot reliably identify character boundaries. The right-to-left direction causes word and line ordering errors. Diacritical marks (dots above/below characters) are frequently misread or ignored, turning one character into a completely different one. On full-page screenshots with mixed content (images + text + headlines), Tesseract fails to correctly isolate text regions, often reading the wrong section entirely or producing garbled numbers instead of text. This is why we need to fine-tune a deep learning model (TrOCR) specifically trained on our Urdu dataset.

---

## Week Progress

- [x] Week 1: Setup, Research, Data Collection
- [x] Week 2: Preprocessing & Tesseract Baseline
- [ ] Week 3: Dataset Expansion & PyTorch Dataset
- [ ] Week 4: Model Training & Evaluation
- [ ] Week 5: Deployment
