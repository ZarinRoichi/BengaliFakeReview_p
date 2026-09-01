# Bengali Fake Review Detection 📝

## 📌 Overview

This repository contains the implementation and experimental pipeline for a comprehensive **Bengali fake review detection benchmark** built on the [Bengali Fake Review Dataset](https://huggingface.co/datasets/shawon95/Bengali-Fake-Review-Dataset).

The study compares **seven methodological paradigms**:

- Supervised transformer classification
- Transformer-based prompt and few-shot adaptation
- Parameter-efficient LLM sequence classification
- Generative label prediction
- Prompt-only open-source LLM inference
- Ensemble learning
- Provider-hosted/API-based LLM evaluation

The study investigates how **task-specific adaptation, model architecture, prompting strategy, model scale, and evaluation distribution** affect Bengali fake-review classification.

A second objective is to determine whether strong results obtained under a balanced benchmark remain robust under a stricter, prevalence-preserving evaluation protocol with stronger leakage controls.

---

## 🔬 Experimental Design

The study uses two complementary evaluation protocols.

### 1. Balanced-Corpus Protocol

This protocol supports broad comparison across all methodological families.

- Fake-class augmentation and Non-Fake undersampling are performed before partitioning.
- Final corpus size: **12,506 reviews**
- Training: **10,004**
- Validation: **1,251**
- Test: **1,251**
- Test distribution is approximately balanced.

This protocol is used primarily for broad methodological benchmarking.

### 2. Prevalence-Preserving Locked Protocol

This protocol provides a stricter confirmatory evaluation.

- Exact duplicates are removed before partitioning.
- Highly similar reviews are grouped using character-level TF-IDF similarity.
- Near-duplicate groups are kept within the same partition.
- Augmentation and undersampling are restricted to the training set.
- Validation and test sets remain untouched and preserve the original class prevalence.

Final partitions:

| Partition | Fake | Non-Fake | Total |
|---|---:|---:|---:|
| Training | 5,345 | 5,345 | 10,690 |
| Validation | 134 | 770 | 904 |
| Locked Test | 134 | 770 | 904 |

The locked test is not used for model selection, prompt development, threshold tuning, or hyperparameter optimisation.

---

## ⚙️ Methods

### Supervised Transformer Encoders

Supervised classification experiments include Bengali-specific and multilingual transformer models such as:

- BanglaBERT
- XLM-R
- mBERT

The models are fine-tuned using binary classification heads.

### Transformer Prompt and Few-Shot Adaptation

Multiple prompt-based strategies are evaluated, including:

- Few-shot classification
- Zero-shot prompting
- Manual prompt fine-tuning
- Demonstration-augmented prompting
- Lightweight automatic prompt search
- LM-BFF-style template generation
- AutoPrompt-style trigger search

### Parameter-Efficient LLM Classification

Bengali-specialised causal LLMs are adapted using **QLoRA** with sequence-classification heads.

Evaluated model families include:

- TituLLM
- TigerLLM
- BanglaLLaMA
- Bangla-Qwen variants

### Generative Label Prediction

The same causal LLM families are also evaluated using a generative formulation:

`Instruction + Review → Fake / Non-Fake label`

This enables a direct comparison between **discriminative classification-head adaptation** and **generative label prediction**.

### Prompt-Only Open-Source LLM Evaluation

Open-source LLMs are evaluated without task-specific parameter updates under:

- Zero-shot prompting
- Few-shot prompting
- Exploratory revised prompts
- Candidate-label scoring

The revised-prompt experiments are treated as **post-hoc prompt-sensitivity analyses** rather than independently selected benchmark configurations.

### Ensemble Learning

Four Bengali-adapted LLM classifiers are combined using:

- Majority voting
- Equal-weight soft voting
- Logistic-regression stacking

### Provider-Hosted LLM Evaluation

Several remotely hosted LLMs are evaluated through APIs using a common zero-shot classification setup.

The experiments record:

- Exact model identifiers
- Prompts
- Decoding settings
- Raw responses
- Retry behaviour
- Token settings
- Parsed predictions
- Generation timestamps

---

## 📊 Evaluation Metrics

The study reports:

- Accuracy
- Weighted Precision
- Weighted Recall
- Weighted F1
- Macro F1
- Fake-class Precision
- Fake-class Recall
- Fake-class F1

**Weighted F1** is used as the primary aggregate comparison metric, while Fake-class measures are especially important under the imbalanced locked protocol.

---

## 📈 Key Findings

- **TituLLM 3B with SeqCLS + QLoRA** achieved the strongest balanced-test performance with **99.12% weighted F1**.
- Under the stricter prevalence-preserving locked evaluation, TituLLM 3B achieved **97.90% weighted F1** and **92.94% Fake-class F1**.
- **BanglaBERT remained highly competitive**, demonstrating that a compact Bengali-specific encoder can rival substantially larger causal LLMs.
- Sequence-classification adaptation outperformed generative label prediction for every paired causal LLM evaluated.
- Task-specific adaptation was substantially more effective than prompt-only inference.
- Prompt revision affected models inconsistently, demonstrating measurable **prompt sensitivity**.
- Provider-hosted LLMs remained below the strongest task-adapted models.
- Ensemble methods were competitive but did not outperform the strongest individual models.
- Model scale alone did not reliably predict classification performance.

---

## 🔍 Error Analysis

Manual inspection of misclassified examples identified several recurring challenges:

- Negation interacting with promotional language
- Very short reviews with limited contextual evidence
- Genuine reviews written in promotional styles
- Fake reviews written as convincing personal experiences
- Shared lexical cues across Fake and Non-Fake classes
- Conflicting textual evidence

The results suggest that task-specific adaptation reduces many errors, while ambiguity in the textual boundary between genuine and deceptive reviews remains difficult.

---

## 🛡️ Leakage and Reproducibility Controls

The locked evaluation includes several safeguards:

- Exact duplicate removal
- Near-duplicate grouping before partitioning
- Group-aware train/validation/test splitting
- Training-only augmentation
- Training-only undersampling
- Fixed random seeds
- Locked-test isolation
- Test-file SHA-256 verification
- Stored model identifiers and inference settings
- Deterministic label parsing for API evaluations

---

## 💻 Implementation

Local experiments were conducted using:

- Python
- PyTorch
- Hugging Face Transformers
- PEFT
- bitsandbytes
- scikit-learn
- pandas
- NumPy
- Google Colab
- NVIDIA T4 GPU

Parameter-efficient LLM adaptation was performed using **LoRA/QLoRA** where appropriate.

---

## 📁 Dataset

Bengali Fake Review Dataset:

https://huggingface.co/datasets/shawon95/Bengali-Fake-Review-Dataset

The original dataset contains:

- **1,339 Fake reviews**
- **7,710 Non-Fake reviews**
- **9,049 reviews in total**

### License

The dataset is distributed under **CC BY-NC-ND 4.0**.

The original dataset and generated review samples are **not redistributed** in this repository.

This repository provides implementation and experimental code for research and educational purposes.

---

## 📝 Research Status

The experimental study has been completed and the associated manuscript has been prepared for submission.
