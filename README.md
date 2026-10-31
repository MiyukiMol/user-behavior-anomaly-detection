# User Behavior Anomaly Detection for Cybersecurity

## Project Overview

This project explores login-event data to investigate how user behavior analytics can support cybersecurity monitoring and account-takeover (ATO) detection.

## Project Structure

- `01_exploratory_data_analysis.ipynb` — Exploratory Data Analysis (EDA)
- `02_rule_based_detection.ipynb` — Planned rule-based detection
- `03_anomaly_detection_ml.ipynb` — Planned machine-learning anomaly detection

The second and third notebooks are planned extensions.

## Dataset

**Login Data Set for Risk-Based Authentication (RBA)**

- Source: [Kaggle Dataset](https://www.kaggle.com/datasets/dasgroup/rba-dataset)
- License: CC BY 4.0, as stated by the dataset source
- Related paper: Wiefling et al. (2022), *Pump Up Password Security! Evaluating and Enhancing Risk-Based Authentication on a Real-World Large-Scale Online Service*
- DOI: https://doi.org/10.1145/3546069

The dataset contains synthetic login-event records and should not be described as confirmed real-world attack logs.

## Initial Findings

The following findings are based on an initial sample of 10,000 rows unless otherwise specified.

- **Login outcomes:** 50.18% failed logins and 49.82% successful logins.
- **ATO labels in the sample:** No positive account-takeover cases were present in the 10,000-row sample.
- **Full-dataset label scan:** 141 positive labels among 31,269,264 records, indicating severe class imbalance.
- **Time coverage:** The sample spans approximately two hours on a single day.
- **Device types:** Mobile devices account for 66.16% of sample events, followed by desktops at 31.00% and tablets at 2.81%.
- **User activity:** The sample contains 4,743 unique users, with a highly right-skewed distribution of events per user.

These are preliminary findings. The first 10,000 rows may not represent the full dataset.

## Methodology and Limitations

- The EDA examines user ID, login timestamp, login success, country, device type, and the account-takeover label.
- `Is Account Takeover` is the target label and must not be used as an input feature.
- Failed logins do not necessarily indicate malicious activity.
- Unusual locations and devices should be evaluated against historical user behavior.
- Severe class imbalance means accuracy alone would be insufficient for evaluating a future detector. Precision, recall, PR-AUC, and confusion-matrix analysis should also be considered.
- Future models should use a leakage-aware evaluation strategy, such as a time-based split.
- The initial sample is limited and should not be treated as representative without further validation.

## Tools

- Python
- pandas
- NumPy
- Matplotlib
- Google Colab
- Jupyter Notebook

## How to Run

1. Clone or download this repository.
2. Open `01_exploratory_data_analysis.ipynb` in Google Colab or Jupyter Notebook.
3. Download the dataset from Kaggle.
4. Follow the notebook's instructions to access the ZIP archive and adjust file paths if necessary.
5. Run the notebook cells from top to bottom.

If you use the Kaggle API, configure your credentials securely. Never commit API tokens or credential files.

## Project Status

- [x] Exploratory data analysis
- [ ] Rule-based detection
- [ ] Machine-learning anomaly detection

## References

Wiefling, S., et al. (2022). *Pump Up Password Security! Evaluating and Enhancing Risk-Based Authentication on a Real-World Large-Scale Online Service*. ACM Transactions on Privacy and Security. https://doi.org/10.1145/3546069

Dataset: *Login Data Set for Risk-Based Authentication (RBA)*. Kaggle. https://www.kaggle.com/datasets/dasgroup/rba-dataset