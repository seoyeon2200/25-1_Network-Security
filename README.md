# 25-1_Network-Security

## 📌 Objective
This project aims to build a **flow-based machine learning model** to detect network intrusions using real-world traffic data. The key steps include:

- Extracting statistical features from packet-level data  
- Aggregating packets into flows (5-tuple based)  
- Training a **Random Forest** classifier  
- Evaluating the model with various performance metrics  

---

## 📁 Dataset Description

| Dataset | Type      | File Name              |
|---------|-----------|------------------------|
| CAIDA   | Benign    | `caida_60_sec_new.csv` |
| CIC     | Malicious | `cic_60_sec_new.csv`   |
| UNSW    | Malicious | `unsw_60_sec_new.csv`  |

Each CSV contains packet-level records with:
- `SrcIP`, `DstIP`, `SrcPort`, `DstPort`, `Protocol`, `Packet Size`, `Time Stamp`

---

## 🔍 Feature Extraction

### 🛠️ Process
1. **Load data** using pandas  
2. **Group into flows** using 5-tuples: (SrcIP, DstIP, SrcPort, DstPort, Protocol)  
3. **Extract features** from each flow:
   - `Flow Size`, `Flow Duration`  
   - `Packet Size`: mean, min, max, std  
   - `IAT (Inter-Arrival Time)`: mean, min, max, std  
   - `Packet Size Entropy`, `IAT Entropy`  
   - `Packet Rate`  

### 💡 Rationale
- Flow-based stats represent session behavior  
- Entropy and timing stats help detect stealthy or irregular patterns  
- All features are lightweight and effective for real-time applications  

---

## 🤖 Model Training

- **Classifier**: Random Forest  
- **Train/Test Split**: 70:30  
- **Training Data**: Combined flow data from:
  - CAIDA (benign)  
  - CIC (malicious)  
  - UNSW (malicious)

---

## 📊 Evaluation Results

| Metric      | Value   |
|-------------|---------|
| Accuracy    | 100%    |
| Precision   | 99–100% |
| Recall      | 100%    |
| F1-Score    | 99–100% |
| ROC-AUC     | 0.9995  |

### 📌 Confusion Matrix
- **True Negatives (TN)**: ~20,000  
- **False Positives (FP)**: 75  
- **False Negatives (FN)**: 5  
- **True Positives (TP)**: 39,238  

### 📈 ROC Curve
- AUC ≈ **0.9994**  
- The ROC curve stays near the top-left corner, showing excellent separability.

---

## 🔎 Analysis

- High **recall** → effective at catching intrusions  
- High **precision** → minimal false alarms  
- Flow-level **entropy and timing** features are highly informative  
- **Random Forests** handle complex interactions well  

---

## ✅ Conclusion

This project validates the use of **flow-based ML** for intrusion detection:
- Simplifies raw packets into meaningful flows  
- Extracted features generalize well to various attack types  
- Ensemble models like Random Forests deliver strong performance  

---
