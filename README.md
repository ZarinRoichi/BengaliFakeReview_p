# Bengali Fake Review Detection 📝

## 📌 Overview
This repository contains the implementation and experimental pipeline for a comprehensive **Bengali fake review detection benchmark** built on the [Bengali Fake Review Dataset](https://huggingface.co/datasets/shawon95/Bengali-Fake-Review-Dataset).

The study compares multiple modeling paradigms, including:

- Supervised transformer encoders
- Parameter-efficient LLM fine-tuning
- Discriminative classification-head adaptation
- Generative label prediction
- Zero-shot and few-shot prompting
- Prompt sensitivity analysis
- Ensemble learning
- Provider-hosted/API-based LLM evaluation

The main objective is not only to identify the best-performing model, but also to examine how different adaptation and prompting strategies affect reliability and generalization in Bengali fake review classification.

⚠️ **License Notice**
- The original dataset is licensed under **CC BY-NC-ND 4.0**.
- The dataset itself is **not redistributed** in this repository.
- Only preprocessing, augmentation, splitting, training, and evaluation code is provided.
- This repository is intended strictly for **research and educational purposes**.

---

## ⚙️ Experimental Workflow

### 1. Data Splitting
- The original dataset is first divided using a stratified **80/10/10 train/validation/test split**.
- A fixed random seed is used for reproducibility.
- Validation and test sets remain unchanged throughout the experiments.

### 2. Training-Set Processing
All augmentation and balancing operations are applied **only to the training split**.

#### FAKE-class augmentation
- Random punctuation modification
- Character swaps
- Thin-space insertion

#### NON-FAKE balancing
- Training-only undersampling is used to obtain an approximately balanced class distribution.

### 3. Model Training and Evaluation

The benchmark evaluates several methodological settings:

#### Supervised Encoders
Fine-tuned transformer-based classification models are used as supervised baselines.

#### Parameter-Efficient LLM Adaptation
LLMs are adapted using techniques such as **LoRA/QLoRA** for efficient task-specific training.

#### Discriminative LLM Classification
LLMs are fine-tuned with classification heads for direct FAKE/NON-FAKE prediction.

#### Generative Label Prediction
Causal language models are trained or prompted to generate the target class label.

#### Prompt-Based Evaluation
Open-source and hosted LLMs are evaluated under **zero-shot and few-shot prompting** settings.

#### Prompt Sensitivity
Alternative prompt formulations are tested to analyze how instruction wording influences model predictions.

#### Ensemble Learning
Predictions from multiple models are combined to evaluate whether ensemble strategies improve robustness and overall performance.

#### API-Based LLM Evaluation
Provider-hosted LLMs are evaluated using controlled prompts and consistent test samples.

---

## 📊 Evaluation Protocol

The experiments are designed to reduce data leakage and ensure consistent comparison across models.

- Training-only augmentation and balancing
- Clean validation and test partitions
- Fixed random seed
- Consistent preprocessing across methods
- Identical held-out samples for model comparison
- Weighted F1 used as a primary comparison metric
- Additional evaluation under a prevalence-preserving locked test setting

---

## 🔍 Research Focus

The project investigates several questions beyond standard classification accuracy:

- How do supervised encoders compare with adapted LLMs?
- Does task-specific LLM adaptation outperform prompt-only inference?
- How do discriminative and generative adaptation strategies differ?
- How sensitive are LLM predictions to prompt wording?
- Do ensemble methods provide consistent improvements?
- How well do models generalize under a more realistic class distribution?

---

## 🚀 Current Extensions

Current work includes:

- Broader comparison of LLM adaptation strategies
- Prompt-sensitivity evaluation
- Provider-hosted LLM benchmarking
- Error and misclassification analysis
- Reliability and generalization analysis across evaluation settings

---

## 📁 Dataset

Bengali Fake Review Dataset:  
https://huggingface.co/datasets/shawon95/Bengali-Fake-Review-Dataset

The original dataset is not included in this repository due to its licensing conditions.
