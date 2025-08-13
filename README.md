# 🦴 Osteoarthritis X-ray Image Classification — EDA, Preprocessing & CNN Modeling

Reproducible pipeline for classifying knee osteoarthritis from radiographs: **image EDA → preprocessing & augmentation → CNN modeling (Sequential & Functional, plus a transfer-learning trial) → evaluation**.

> ⚠️ Research/education only — **not** for clinical use.

---

## 🎯 Objectives

* Describe the dataset through image-centric EDA
* Build a clean preprocessing + augmentation pipeline
* Train and compare **custom CNNs** (Sequential & Functional) and a **MobileNet** variant
* Evaluate with **Accuracy, Precision, Recall, F1** and learning curves
* Summarize insights and next steps

---

## 🗂️ Dataset

* Knee **X-ray images** with class labels (see notebook for class names).
* Split into **train / validation / test**.

---

## 🔎 Image EDA

* **Distribution per class** (counts/ratios).
* **Variability overview** (visual samples across classes).
* **RGB/intensity histograms** to inspect brightness/contrast.
* **Aspect ratio** distribution and **native resolution** statistics (width×height).

---

## 🧼 Preprocessing & Augmentation

**Normalization**

* Pixel values scaled from **\[0, 255] → \[0, 1]**.

**Data augmentation (train only)**

* Horizontal shift (±10% width)
* Vertical shift (±10% height)
* Shear transform
* Zoom in/out (±10%)
* Horizontal flip
* Random brightness **90%–110%**

**Generators**

* Used `class_mode='sparse'` to provide **integer labels** (efficient with sparse cross-entropy losses).

---

## 🧠 Models

* **Baseline Custom CNN (Sequential API)**
* **Custom CNN (Functional API)**
* **MobileNet transfer learning** with a custom classification head

**Training setup**

* Loss: (sparse) **categorical cross-entropy**
* Optimizer: **Adam**
* Callbacks: early stopping / best-checkpoint (see notebook)

---

## 📈 Evaluation

* Metrics: **Accuracy, Precision, Recall, F1** (validation & test)
* **Learning curves** (loss/accuracy across epochs)

> Note: This study **does not** include a confusion matrix or misclassification error analysis.

---

## ✅ Results

* The **baseline custom CNN** provides the strongest and most stable performance on this dataset/split.
* The **MobileNet** modification **underperformed** relative to the baseline in this setup.

---

## 📌 Conclusion

* Image EDA confirms diverse **resolutions/aspect ratios** and noticeable **intensity variance** across classes.
* **Normalization + targeted augmentation** (shift/zoom/shear/flip/brightness) improves generalization without over-distorting anatomy.
* Using `class_mode='sparse'` simplifies the pipeline and pairs well with **sparse cross-entropy**.
* On this dataset, a **custom CNN** outperformed the **MobileNet** transfer baseline.
* The pipeline is reproducible and ready for further tuning and deployment experiments.
