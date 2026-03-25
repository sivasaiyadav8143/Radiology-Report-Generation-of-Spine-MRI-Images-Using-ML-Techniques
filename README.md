# 🧠 Radiology Report Generation of Spine MRI Images Using Machine Learning Techniques

This repository contains the implementation of my **Major Project** for the  
**Post Graduate Program (PGP) in Artificial Intelligence & Machine Learning**  
offered by **The University of Texas at Austin**.

The project explores automated generation of **radiology reports** from **Spine MRI images** using a combination of **Computer Vision**, **Deep Learning**, and **Natural Language Processing**. It aims to support radiologists by reducing reporting time, improving consistency, and enabling scalable diagnostic assistance in clinical environments.

---

## 📌 Table of Contents
- [Overview](#overview)
- [Motivation](#motivation)
- [Dataset](#dataset)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Methodology](#methodology)
- [Model Architectures](#model-architectures)
- [Training Details](#training-details)
- [Results](#results)
- [Next Steps](#next-steps)
- [Tech Stack](#tech-stack)

---

## 🩻 Overview

This project focuses on generating **clinically meaningful radiology impressions** from **Spine MRI images**.  
Unlike prior work that focuses mainly on **chest X‑rays** or **single‑view lumbar MRIs**, this work incorporates **multiple spine MRI views** (cervical, lumbar, etc.) and generates **detailed, structured radiology reports**.

The pipeline integrates:

- **Transfer Learning (CheXNet, ResNet50)** for feature extraction  
- **Encoder–Decoder architecture with LSTMs** for text generation  
- **Uni‑Directional & Bi‑Directional LSTM variants**  
- **BLEU‑based evaluation** for report quality  

---

## 🎯 Motivation

Radiology reporting is time‑intensive and requires deep expertise. Automating this process can:

- Assist radiologists in high‑volume settings  
- Improve reporting consistency  
- Support rural or resource‑limited hospitals  
- Reduce cognitive load for clinicians  

> “Providing automated support for this task has the potential to ease clinical workflows and improve both the quality and standardization of care.”

---

## 📂 Dataset

The dataset consists of **560 Spine MRI images** collected from a private hospital.

- **420 images** used for training  
- **140 images** used for testing  
- Images are grayscale  
- Reports are masked to protect PII  
- Data augmentation applied to balance problematic vs. non‑problematic cases  

### Preprocessing steps:
- Removal of special characters  
- Addition of `<Start>` and `<End>` tokens  
- Conversion of DICOM → JPG  
- Image resizing to 224×224  

---

## 🔍 Exploratory Data Analysis

Key insights from EDA:

- Gender‑wise distribution of patients  
- Age distribution across cervical & lumbar cases  
- Word frequency analysis of radiology impressions  
- Word cloud of most common diagnostic terms  
- Image dimension variability  

Example insight:  
> “Females are facing more spinal disc issues in our case.”

---

## 🧩 Methodology

The pipeline consists of:

### **1. Feature Extraction (CV)**
Using pretrained CNNs:
- **CheXNet** → 1024‑dim features  
- **ResNet50** → 2048‑dim features  

### **2. Report Generation (NLP)**
Encoder–Decoder architecture with:
- Embedding layer (300‑dim vectors)  
- Uni‑Directional LSTM  
- Bi‑Directional LSTM  
- Dense layers + Dropout  
- Softmax output over vocabulary  

### **3. Decoding**
- Greedy Search  
- Beam Search (optional)

---

## 🏗 Model Architectures

### **CheXNet + Bi‑Directional LSTM**
- Total params: **2.22M**
- Trainable params: **2.17M**

### **ResNet50 + Uni‑Directional LSTM**
- Total params: **1.78M**
- Trainable params: **1.73M**

ResNet50‑based models performed significantly better on Spine MRI images.

---

## 🏋️ Training Details

- Framework: **TensorFlow + Keras**
- Epochs: **20**
- Loss: Categorical Cross‑Entropy
- Optimizer: Adam
- Evaluation Metric: **BLEU‑1 to BLEU‑4**
- Environment: Google Colab

> “Resnet50 is doing far better than CheXNet on the Spine MRIs which is clear from the BLEU scores.”

---

## 📊 Results

### **BLEU Score Comparison**

| Attempt | Model     | LSTM Type      | BLEU‑1 | BLEU‑2 | BLEU‑3 | BLEU‑4 |
|--------|-----------|----------------|--------|--------|--------|--------|
| 1 | CheXNet | Uni | 0.101 | 0.078 | 0.081 | 0.101 |
| 2 | CheXNet | Bi | 0.090 | 0.063 | 0.064 | 0.064 |
| 3 | ResNet50 | Uni | **0.262** | **0.231** | **0.212** | **0.203** |
| 4 | ResNet50 | Bi | 0.238 | 0.206 | 0.186 | 0.179 |

**ResNet50 + Uni‑Directional LSTM** achieved the best performance.

---

## 🚀 Next Steps

- Combine **multiple MRI slices per patient**  
- Experiment with **VGG, AlexNet, DenseNet**  
- Train for **more epochs**  
- Integrate **Attention Mechanisms**  
- Explore **Transformer‑based architectures** (e.g., ViT + GPT‑style decoder)

---

## 🛠 Tech Stack

- Python  
- TensorFlow / Keras  
- NumPy, Pandas  
- NLTK  
- Matplotlib / Seaborn  
- Google Colab  
- Selenium (for automated data extraction)
