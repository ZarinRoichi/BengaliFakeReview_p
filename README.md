# Bengali Fake Review Detection 📝

## 📌 Overview
This project focuses on detecting **fake reviews in Bengali** using a combination of classical ML, deep learning, transformer-based models, and LLM fine-tuning.  
The work is built on the [Bengali Fake Review Dataset](https://huggingface.co/datasets/shawon95/Bengali-Fake-Review-Dataset).  

⚠️ **License Notice**:  
- Dataset is under **CC BY-NC-ND 4.0**.  
- The dataset itself is **not redistributed** here.  
- Only preprocessing, augmentation, and splitting **code** is provided.  
- Intended strictly for **research & educational purposes**.  

---

## ⚙️ Workflow
1. **Preprocessing**  
   - Normalized text (whitespace, punctuation cleanup).  
   - Deduplication using RapidFuzz.  

2. **Augmentation (FAKE class only)**  
   - Random punctuation tweaks (`!`, `!!`, `…`).  
   - Random character swaps.  
   - Thin-space insertion.  

3. **Balancing**  
   - Ensured 1:1 ratio between FAKE and NON-FAKE.  

4. **Splitting**  
   - Stratified **80/10/10** Train/Validation/Test split.  
   - Fixed seed for reproducibility.  

5. **Model Training & Evaluation**  
   - Fine-tuned transformer & LLM models.  
   - Evaluated both single models and ensemble methods.  

---

## 📊 Results

| Model | Acc. | Prec. | Rec. | F1 |
|-------|------|-------|------|----|
| **BanglaBERT** | **97.9%** | 98.2% | 99.3% | 98.8% |
| XLM-R | 97.3% | 97.6% | 99.3% | 98.4% |
| mBERT | 87.3% | 87.7% | 86.7% | 87.2% |
| Gemma-2B | 84.4% | 71.2% | 84.4% | 77.2% |
| Gemini | 73.0% | 75.6% | 73.0% | 63.9% |
| Bangla-s1k-llama-3.2-3B | 97.17% | 97.39% | 96.85% | 97.09% |
| culturax-base-3b-seqcls | 97.21% | 97.27% | 97.02% | 97.14% |
| BanglaLLama-3.2-3b-alpaca | 97.21% | 97.33% | 96.97% | 97.14% |
| Bangla-s1k-qwen-2.5-3B | 97.36% | 97.48% | 97.13% | 97.29% |
| **Ensemble (Weighted Soft Vote)** | **97.62%** | 97.70% | 97.43% | 97.56% |
| Stacking Ensemble | 97.39% | 97.54% | 97.15% | 97.33% |

👉 Fine-tuned **BanglaBERT** gave the best single-model results (F1 = 98.8%).  
👉 Ensemble (Weighted Soft Vote) slightly improved robustness (F1 = 97.56%).  
👉 Prompt-only LLMs underperformed compared to fine-tuned models.  


