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




