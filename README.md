# 💍 Wedding Planner AI — Smart Wedding Planning Platform

> An AI-powered wedding planning platform developed as part of the coursework at **Esprit School of Engineering**.  
> The system combines multiple AI modules to assist couples in planning every aspect of their wedding.

---

## 📌 Project Overview

This project is built by a team of 3 members, each responsible for a different AI objective. Together, the three modules form a complete intelligent wedding planning assistant covering **bridal makeup**, **food & catering**, and **venue selection**.

| Module | Objective | Member |
|--------|-----------|--------|
| 💄 Bridal Makeup Recommendation | Recommend and visualize personalized makeup for the bride | Member 1 |
| 🍽️ Food & Catering Recommendation | Recognize dishes and recommend a complete wedding menu | Member 2 |
| 🏛️ Venue Classification & Enhancement | Classify venue styles and generate decorated venue visuals | Member 3 |

---

## 🎯 Global Objective

Build an end-to-end AI platform that helps couples :
- Find the most suitable **makeup look** based on the bride's facial features
- Get a personalized **catering menu** based on food preferences
- Visualize **venue decoration** suggestions before booking

---

## 💄 Module 1 — Bridal Makeup Recommendation

### Description
Given a portrait photo of the bride, the system automatically recommends the most suitable makeup look based on her facial features and generates a visual preview of the result.

### Pipeline
```
Bride photo
    │
    ▼
Gemini Vision API → facial traits JSON (7 keys)
    │
    ▼
sentence-transformers → bride vector (384 dims)
    │
    ▼
cosine similarity → best matching CSV profile (100 profiles)
    │
    ▼
build_sd_prompt() → Stable Diffusion text prompt
    │
    ▼
SD v1.5 + LoRA fine-tuned → bride photo with makeup applied
    │
    ▼
XAI → UMAP embedding visualization + leave-one-out trait importance
```

### Technologies
| Component | Technology |
|-----------|-----------|
| Facial trait extraction | Gemini Vision API (`gemini-3-flash-preview`) — multimodal |
| Semantic embeddings | sentence-transformers (`all-MiniLM-L6-v2`) — local |
| Profile matching | cosine similarity — scikit-learn |
| Image generation | Stable Diffusion v1.5 + LoRA fine-tuning |
| Explainability | UMAP visualization + perturbation-based feature attribution |

### Dataset
- Custom CSV — 100 bridal profiles with 7 facial traits + 9 makeup columns
- Custom fine-tuning dataset — 15 labeled bridal makeup images + captions

### Notebooks
- `bridal-makeup/notebooks/01_lora_finetuning.ipynb` — LoRA fine-tuning of Stable Diffusion
- `bridal-makeup/notebooks/02_makeup_recommendation.ipynb` — full end-to-end pipeline

---

## 🍽️ Module 2 — Food & Catering Recommendation

### Description
The food module combines computer vision and a hybrid recommendation system to suggest the best catering menu for a wedding based on the couple's food preferences.

### Features
- Automatic dish recognition from a photo using **MobileNetV2**
- Hybrid personalized recommendation using **TF-IDF + user ratings**
- Explainable AI with **Grad-CAM**
- Natural language recommendation chatbot
- Complete menu generator (appetizer + starter + main + dessert)

### Technologies
| Component | Technology |
|-----------|-----------|
| Dish recognition | MobileNetV2 — Transfer Learning + Fine-tuning |
| Recommendation | TF-IDF + Cosine Similarity + GradientBoosting |
| Explainability | Grad-CAM |
| Interface | Gradio |

### Dataset
- **Food-11** : 16,643 dish images (11 categories) — Kaggle
- **Food Recommendation System** : 400 dishes + 511 ratings — Kaggle

### Results
- Computer Vision model accuracy : **83.6%**
- Recommendation model accuracy : **74%**

### Notebooks
- `food-catering/Wedding_Planner_Food.ipynb` — main notebook

---

## 🏛️ Module 3 — Venue Classification & Enhancement

### Description
The venue module classifies the style of a wedding venue from an image and generates a decorated version of that venue while preserving its original structure using ControlNet.

### Features
- Venue style classification (Rustic / Luxury / Garden / Modern / Classic)
- Structure-preserving venue enhancement using **ControlNet + Stable Diffusion**
- Canny edge detection for structure conditioning
- Occlusion-based explainability heatmap

### Pipeline
```
Venue image
    │
    ├──► CNN classifier → predicted style (e.g. Rustic, 92%)
    │
    └──► Canny edge detection → conditioning image
              │
              ▼
         ControlNet + SD v1.5 + decoration prompt
              │
              ▼
         Enhanced decorated venue image
```

### Technologies
| Component | Technology |
|-----------|-----------|
| Classification | Pretrained CNN — fine-tuned on venue images |
| Generative enhancement | ControlNet + Stable Diffusion v1.5 |
| Edge detection | OpenCV Canny |
| Explainability | Occlusion-based heatmap |
| Evaluation | FID score, CLIP score, confusion matrix |

### Notebooks
- `venue/notebooks/classification_venues.ipynb`
- `venue/notebooks/controlnet_wedding_generation.ipynb`
- `venue/notebooks/test_generation.ipynb`

---

## 🗂️ Repository Structure

```
Wedding_Planner_AI/
│
├── bridal-makeup/
│   ├── notebooks/
│   │   ├── 01_lora_finetuning.ipynb
│   │   └── 02_makeup_recommendation.ipynb
│   ├── data/
│   │   ├── bridal_makeup_dataset.csv
│   │   └── makeup_finetune_dataset.csv
│   └── assets/
│       └── pipeline_architecture.png
│
├── food-catering/
│   ├── Wedding_Planner_Food.ipynb
│   ├── 1662574418893344.csv
│   └── ratings.csv
│
├── venue/
│   ├── notebooks/
│   │   ├── classification_venues.ipynb
│   │   ├── controlnet_wedding_generation.ipynb
│   │   └── test_generation.ipynb
│   ├── classification_dataset/
│   ├── wedding_data/
│   └── outputs/
│
└── README.md
```

---

## ⚙️ Installation

```bash
# Core dependencies
pip install torch torchvision
pip install diffusers transformers accelerate peft
pip install sentence-transformers scikit-learn
pip install google-genai
pip install tensorflow keras
pip install pandas numpy Pillow matplotlib opencv-python
pip install gradio umap-learn
```

---

## 🔑 API Keys Required

| Module | API | Where to get it |
|--------|-----|----------------|
| Bridal Makeup | Gemini API key | [aistudio.google.com](https://aistudio.google.com) — free |

> ⚠️ Never hardcode API keys in notebooks. Use environment variables or Kaggle Secrets.

---

## 🧩 Explainable AI Summary

| Module | XAI Method |
|--------|-----------|
| Bridal Makeup | UMAP embedding visualization + leave-one-out feature attribution |
| Food & Catering | Grad-CAM on MobileNetV2 conv layers |
| Venue | Occlusion-based heatmap on ControlNet conditioning image |

---

## 📊 Results Summary

| Module | Model | Performance |
|--------|-------|-------------|
| Bridal Makeup | Cosine similarity matching | 80.7% similarity score |
| Bridal Makeup | LoRA fine-tuned SD | Visual makeup generation |
| Food & Catering | MobileNetV2 | 83.6% accuracy |
| Food & Catering | Hybrid recommender | 74% accuracy |
| Venue | CNN classifier | 92% confidence (example) |
| Venue | ControlNet SD | Structure-preserving generation |

---

## 🚀 Platform
- **Kaggle** (GPU T4 — free 30h/week) — training and inference
- **Google Colab** — prototyping
- **Google AI Studio** — Gemini Vision API (free tier)
- **Hugging Face** — pretrained models and LoRA weights hosting

---

## 🔮 Future Improvements
- Expand training datasets for all three modules
- Integrate all three modules into a unified web application
- Add user authentication and preference profiles
- Deploy via Flask or FastAPI backend
- Improve XAI visualizations with interactive dashboards

---

## 🙏 Acknowledgments
This project was developed under the guidance of professors at **Esprit School of Engineering**.  
Smart Wedding Planning Platform — AI Project — 2025/2026.
