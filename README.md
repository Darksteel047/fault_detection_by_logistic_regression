# Fault Detection in 3-Phase Power System (ML Classification)
Machine Learning • Feature Engineering • Power Systems • Random Forest

This project predicts fault vs normal conditions in a three-phase electrical system using voltage and current measurements.
It follows a full machine learning pipeline, including data cleaning, feature engineering, EDA, model training, tuning, and explainability.

---

# Project Overview

Electrical faults cause significant current surges and voltage dips. This project uses instantaneous and RMS features derived from 3-phase voltages and currents to classify:
- 0 → Normal condition
- 1 → Fault condition
A tuned Random Forest model achieves near-perfect performance with strong physical interpretability.

---

# Dataset

The dataset contains:
- Instantaneous currents: Ia, Ib, Ic
- Instantaneous voltages: Va, Vb, Vc
- Derived RMS features: Ia_rms, Ib_rms, Ic_rms, Va_rms, Vb_rms, Vc_rms
- Target label: target (0/1)
RMS features were engineered because they reflect true power system behavior under fault conditions.

---

# Exploratory Data Analysis (EDA)

Key findings:
- ✔ Current spikes during faults: RMS currents increase sharply under fault conditions.
- ✔ Voltage dips during faults: RMS voltage significantly decreases during faults.
- ✔ Instantaneous values are noisy: Raw values fluctuate due to AC waveform zero-crossings.
- ✔ Correlation patterns: RMS currents correlate strongly with each other; RMS voltages correlate strongly; Inverse correlation between RMS voltage & RMS current
- ✔ RMS features cleanly separate classes: These became the primary predictors.

---

# Modeling Approach

Models trained:
- Logistic Regression
- Support Vector Machine
- K-Nearest Neighbors
- Random Forest
(All models wrapped in clean preprocessing pipelines)

The best model was selected based on Accuracy and F1-Score.

---

# Final Model: Random Forest (Tuned)

Best Hyperparameters (via RandomizedSearchCV, 5-fold CV):
n_estimators: 332  
max_depth: 100  
min_samples_split: 9  
min_samples_leaf: 4  
max_features: 'log2'

Performance on Test Set
Metric|	Score
|---|---|
Accuracy|	1.00
Precision|	1.00
Recall|	1.00
F1-Score|	1.00
False Positives|	5
False Negatives|	1

The model achieves near-perfect classification, with extremely low false misses — ideal for safety-critical systems.

---

# Feature Importance (Explainability)

Top predictors:

Feature|	Importance
|---|---|
Ia_rms|	0.2888
Ib_rms|	0.1980
Va_rms|	0.1134
Vb_rms|	0.1022

Interpretation:

- RMS currents are the strongest indicators of faults
- RMS voltages contribute significantly (voltage dips)
- Raw instantaneous values contribute minimally due to waveform noise
- Importance ranking matches electrical theory of short-circuit events

This makes the model trustworthy and domain-aligned.

---

# Tech Stack

- Python
- Pandas / NumPy
- Scikit-Learn
- Seaborn / Matplotlib
- RandomizedSearchCV
- Power systems domain knowledge

---

# Key Learnings

- RMS values are essential for electrical fault classification
- Pipelines help avoid data leakage
- Random Forests are robust and interpretable for power systems
- ML + electrical domain knowledge greatly improves performance
- Hyperparameter tuning significantly boosts model reliability

---

# Future Work (Optional Section)

- Deploy model using Streamlit / Flask API
- Add time-series-based fault location detection
- Introduce imbalance handling (SMOTE, class weights)
- Extend dataset with more fault types (L-G, L-L, 3-phase faults)

---

# References

- Power systems theory (fault behavior, RMS quantities)
- Scikit-Learn documentation
- Kaggle dataset providers

