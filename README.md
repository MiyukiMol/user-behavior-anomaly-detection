# User Behavior Anomaly Detection for Cybersecurity

## Project Overview
This project explores login-event data to investigate how user behavior analytics and machine learning can support cybersecurity monitoring and Account Takeover (ATO) detection, including cost-sensitive threshold optimization and model interpretability (SHAP).

## Project Structure
- `01_exploratory_data_analysis.ipynb` — Exploratory Data Analysis (EDA) on login-event data
- `02_rule_based_detection.ipynb` — Rule-based detection baseline
- `03_supervised_anomaly_detection.ipynb` — Supervised ATO detection with CatBoost, cost-sensitive threshold optimization, and SHAP explainability ([GitHub Notebook](https://github.com/MiyukiMol/user-behavior-anomaly-detection/blob/main/03_supervised_anomaly_detection.ipynb))[cite: 2]

## Dataset
**Login Data Set for Risk-Based Authentication (RBA)**
- **Source:** Kaggle Dataset (`dasgroup/rba-dataset`)
- **License:** CC BY 4.0, as stated by the dataset source
- **Related paper:** Wiefling et al. (2022), *Pump Up Password Security! Evaluating and Enhancing Risk-Based Authentication on a Real-World Large-Scale Online Service*
- **DOI:** https://doi.org/10.1145/3546069

The dataset contains login-event records from Risk-Based Authentication logs and should be interpreted within its documented scope and label characteristics rather than treated solely as confirmed ground-truth attack logs.

## Initial Findings (EDA Sample)
The following preliminary findings are based on an initial sample of 10,000 rows unless otherwise specified:
- **Login outcomes:** 50.18% failed logins and 49.82% successful logins.
- **ATO labels in the sample:** No positive account-takeover cases were present in the 10,000-row sample.
- **Full-dataset label scan:** 141 positive labels among 31,269,264 records, highlighting severe class imbalance.
- **Time coverage:** The sample spans approximately two hours on a single day.
- **Device types:** Mobile devices account for 66.16% of sample events, followed by desktops at 31.00% and tablets at 2.81%.
- **User activity:** The sample contains 4,743 unique users, with a highly right-skewed distribution of events per user.

## Modeling, Cost Optimization & Interpretability (`03_supervised_anomaly_detection.ipynb`)
- **Model & Reproducibility:** Uses `CatBoostClassifier` with fixed tuned hyperparameters (`random_seed=42`, `early_stopping_rounds=50`) and handles categorical features natively alongside behavioral/contextual signals[cite: 2].
- **Asymmetric Business Cost Framework:** Evaluates thresholds under asymmetric financial assumptions—**€30,000** per False Negative (missed ATO attack), **€30** per False Positive (customer friction / extra verification), and **€3** per True Positive (alert handling)[cite: 2].
- **Optimal Operating Point:** At probability threshold **0.7093** on the chronological test set (**40,029** events: **45** attacks, **39,984** legitimate logins), total expected business loss is minimized to **€101,232** (`FN = 1` → €30,000, `FP = 2,370` → €71,100, `TP = 44` → €132; capturing 44 of 45 attacks).
- **Explainability (SHAP):** Uses `shap.TreeExplainer` to rank top features and visualize feature attributions via summary/beeswarm plots to support detection transparency, SOC triage, and governance.

## Methodology and Limitations
- `Is Account Takeover` is the target label and is excluded from model input features.
- Failed logins do not necessarily indicate malicious activity; contextual and behavioral anomalies should be evaluated carefully.
- Severe class imbalance means accuracy alone is insufficient; precision, recall, F1-score, confusion matrices, and business cost are evaluated.
- Time-aware evaluation is used to prevent temporal leakage.
- Cost parameters (€30,000 / €30 / €3) represent modeled business assumptions that should be calibrated with security, support, and risk stakeholders in production[cite: 2].

## Tools & Libraries
- Python, pandas, NumPy, scikit-learn, CatBoost, SHAP, Matplotlib
- Google Colab / Jupyter Notebook

## How to Run
1. Clone or download this repository.
2. Open the notebooks (`01_exploratory_data_analysis.ipynb`, `02_rule_based_detection.ipynb`, `03_supervised_anomaly_detection.ipynb`) in Google Colab or Jupyter Notebook.
3. Download the dataset from Kaggle and configure file paths as instructed in the notebooks.
4. Run the cells sequentially from top to bottom.

If you use the Kaggle API, configure your credentials securely. Never commit API tokens or credential files.

## Project Status
- [x] Exploratory data analysis
- [x] Rule-based detection
- [x] Supervised machine-learning anomaly detection, cost optimization & SHAP analysis[cite: 2]

## References
- Wiefling, S., et al. (2022). *Pump Up Password Security! Evaluating and Enhancing Risk-Based Authentication on a Real-World Large-Scale Online Service*. ACM Transactions on Privacy and Security. https://doi.org/10.1145/3546069
- Dataset: *Login Data Set for Risk-Based Authentication (RBA)*. Kaggle. https://www.kaggle.com/datasets/dasgroup/rba-dataset