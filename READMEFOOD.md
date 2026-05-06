# 🍽️ Food & Catering Module — Wedding Planner IA

## Description
Ce module est responsable de la recommandation de plats pour les mariages.
Il combine Computer Vision et un système de recommandation hybride pour suggérer
le meilleur menu selon les préférences du couple.

## Fonctionnalités
- 📸 Reconnaissance automatique de plats depuis une photo (MobileNetV2)
- 💍 Recommandation hybride personnalisée (TF-IDF + notes utilisateurs)
- 🔍 Explainable AI avec Grad-CAM
- 🤖 Chatbot de recommandation en langage naturel
- 🍽️ Générateur de menu complet (apéritif + entrée + plat + dessert)

## Technologies utilisées
- Python, TensorFlow, Keras
- MobileNetV2 (Transfer Learning + Fine-tuning)
- TF-IDF + Cosine Similarity
- GradientBoosting Classifier
- Grad-CAM (Explainable AI)
- Gradio / Google Colab

## Datasets
- **Food-11** : 16,643 images de plats (11 catégories) — Kaggle
- **Food Recommendation System** : 400 plats + 511 ratings — Kaggle

## Résultats
- Précision du modèle Computer Vision : **83.6%**
- Précision du modèle de recommandation : **74%**

## Structure
food/
├── Wedding_Planner_Food.ipynb  ← Notebook principal
├── Survey_Wedding_Food_Planner_IA.docx  ← Survey
├── 1662574418893344.csv  ← Dataset plats
└── ratings.csv  ← Dataset ratings
