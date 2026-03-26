# 🌌 HTRU2 Pulsar Candidate Detection

**Linear vs. Non-Linear Classifiers on Imbalanced Astrophysical Data**

This project is a data science research endeavor aimed at addressing the classification and detection of Pulsar candidates from cosmic radio signals. It focuses on resolving a core challenge in Machine Learning: **Extreme Class Imbalance**.

---

## 📑 Table of Contents
- [Introduction](#-introduction)
- [Key Features](#-key-features)
- [Dataset](#-dataset)
- [Methodology & Results](#-methodology--results)
- [Repository Structure](#-repository-structure)
- [Installation & Usage](#-installation--usage)
- [Author](#-author)

---

## 🚀 Introduction
Detecting Pulsars in astronomical surveys (like the HTRU project) is akin to finding a "needle in a haystack." In the HTRU2 dataset, true Pulsar signals constitute only **9.1%** of the samples, while the remaining **90.9%** consists of background noise and artificial Radio Frequency Interference (RFI).

Instead of rushing to deploy complex "black-box" Deep Learning models, this project conducts an in-depth comparative analysis between a linear model (**Logistic Regression**) and a non-linear model (**RBF Support Vector Classifier**). The objective is to establish an optimal decision boundary that ensures high predictive accuracy while maintaining the transparency and low computational latency required for real-time signal filtering systems.

---

## 🌟 Key Features
1. **Overcoming Optimism Bias:** Discarding the standard ROC-AUC metric (which is heavily skewed by the massive volume of True Negatives) and prioritizing **Precision-Recall AUC (PR-AUC)** as the ultimate evaluation criterion for extreme imbalance.
2. **Rigorous Evaluation Strategy:** Implementing **Stratified 5-Fold Nested Cross-Validation** coupled with Grid Search for hyperparameter tuning to completely prevent data leakage and evaluation bias.
3. **Application of Occam's Razor:** Utilizing the **Paired Student's t-test** to statistically prove that the added complexity of a non-linear kernel (RBF) is mathematically redundant, thereby cementing Logistic Regression as the optimal solution.
4. **Explainable AI (XAI) Agent:** Developing an XAI diagnostic interface that extracts the learned coefficients of the Logistic Regression model to explain predictions based on actual astrophysical morphology (e.g., Profile Kurtosis and Skewness).

---

## 📊 Dataset
* **Name:** HTRU2 Dataset (High Time Resolution Universe Survey)
* **Source:** [UCI Machine Learning Repository (ID: 372)](https://archive.ics.uci.edu/dataset/372/htru2)
* **Size:** 17,898 instances (1,639 Pulsars vs. 16,259 RFI Noise samples).
* **Features:** 8 continuous numerical variables (4 describing the Integrated Pulse Profile and 4 describing the DM-SNR Curve).

---

## 🔬 Methodology & Results

The data pipeline integrates Z-score Standardization and Cost-Sensitive Learning (Class-weight balancing) to force the algorithms to prioritize the minority class (Pulsars).

### Experimental Results (Mean ± Std across 5-Fold CV)
| Model | PR-AUC | F1-Score | Recall @ Precision 0.9 | Train Time |
| :--- | :---: | :---: | :---: | :---: |
| Baseline (Majority) | 0.0916 | 0.0000 | 0.0000 | ~ 0.01 s |
| **Logistic Regression** | 0.9226 ± .012 | 0.8406 ± .011 | **0.8666 ± .039** | **0.21 s** |
| **RBF SVC** | **0.9268 ± .012** | **0.8680 ± .008** | 0.8635 ± .040 | 24.28 s |

### 💡 Key Conclusion:
Although the RBF SVC achieved a marginally higher PR-AUC score, the **Paired t-test (p-value = 0.2905)** revealed that this performance difference lacks statistical significance. 
Guided by **Occam's Razor**, **Logistic Regression** is declared the superior operational framework because it:
* Delivers statistically equivalent predictive power.
* Operates with an approximate **114-fold decrease** in computational latency (0.21s vs 24.28s).
* Provides 100% transparency, enabling seamless integration with our XAI diagnostic agent.

---

## 📂 Repository Structure

```text
📦 AI1902_G8_DAP391m_FinalReport
 ┣ 📜 HTRU2.ipynb               # Main Source Code (Jupyter Notebook) covering EDA, Train, Test, and XAI pipeline
 ┣ 📜 DAP391m_HTRU2_SciRep.pdf  # Scientific Report (IEEE 2-column format)
 ┣ 📜 DAP391m_HTRU2_Speech.pdf  # Presentation Slides (Beamer LaTeX)
 ┣ 📜 README.md                 # Project Documentation (This file)
 ┣ 📜 .gitignore                # Git ignore file
 ┗ 📜 LICENSE                   # Open-source license
```

---

## ⚙️ Installation & Usage

To reproduce the experiments conducted in this study, you can clone this repository and execute the Jupyter Notebook locally or via Google Colab.

**1. Clone the Repository:**
```bash
git clone [https://github.com/your-username/AI1902_G8_DAP391m_FinalReport.git](https://github.com/your-username/AI1902_G8_DAP391m_FinalReport.git)
cd AI1902_G8_DAP391m_FinalReport
```

**2. Install Dependencies:**
This project requires Python 3.8+ and the following core libraries:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn ucimlrepo
```

**3. Run the Notebook:**
Open `HTRU2.ipynb` using Jupyter Notebook or VS Code and run the cells sequentially. The notebook is configured to automatically fetch the dataset from the UCI API.

---

## 👨‍💻 Author
* **Ngoc M. Luong (SE203746)**
* **Course:** AI-DS Project (DAP391m) - Class AI1902
* **Institution:** FPT University, Vietnam
* Semester: Spring 2026

*If you find this project helpful or interesting, please consider giving it a ⭐️!*

Bản tiếng Anh này vẫn giữ trọn vẹn sự đanh thép trong lập luận và bố cục trình bày rành mạch. Chúc dự án của bạn thu hút được nhiều sự chú ý trên GitHub!
