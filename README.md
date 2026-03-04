# 🐕 CBARQ Dog Breed Behavior Analysis

Exploring whether a dog's breed correlates with measurable behavioral traits, using owner-survey data from the [C-BARQ (Canine Behavioral Assessment and Research Questionnaire)](https://figshare.com/articles/dataset/C_BARQ_survey_on_dog_behavior_and_temperament/715896) dataset.

> *Is a pit bull more likely to bite than a labrador? Breed restrictions exist in apartment complexes and city ordinances across the country — but should a dog's breed determine its fate? This project takes a data-driven look at that question.*

---

## 📌 Project Goal

Assess whether a dog's breed consistently correlates with behavioral traits — including trainability, energy, excitability, chasing, and attachment-seeking behavior — and evaluate whether those correlations are strong enough to be modeled predictively.

---

## 📂 Repository Structure
```
Puppers/
├── CBARQ_wrangling.ipynb          # Data cleaning and preparation
├── CBARQ_EDA.ipynb                # Exploratory data analysis
├── CBARQ_training_modeling.ipynb  # Model training and comparison
├── Proposal.pdf                   # Original project proposal
└── Reports/
  ├── CBARQ_final_report.pdf       # Written summary of findings
  └── CBARQ_model_report.txt       # Summary of final model specs
```

---

## 🗂️ Data

**Source:** [C-BARQ Dataset on Figshare](https://figshare.com/articles/dataset/C_BARQ_survey_on_dog_behavior_and_temperament/715896)

~12,000 dogs, 14 behavioral traits scored by owners on a 1–5 scale. Traits span three categories:

- **Aggressive behaviors** — stranger-directed, owner-directed, dog-directed aggression, and dog rivalry
- **Fearful behaviors** — dog-directed, stranger-directed, nonsocial, and separation-related fear
- **Other traits** — trainability, chasing, touch sensitivity, excitability, attachment/attention-seeking, and energy level

Analysis was limited to the **10 most common breeds**: Australian Shepherd, Border Collie, Doberman Pinscher, German Shepherd, Golden Retriever, Labrador Retriever, Mixed Breed/Unknown, Standard Poodle, Rottweiler, and Soft-Coated Wheaten Terrier.

---

## 🔧 Methods

### Cleaning & Wrangling
- Removed or addressed nulls and inconsistencies across behavioral score columns
- Separated traits into negatively-perceived behaviors (`neg_traits`) and other behaviors (`oth_traits`) based on distribution analysis
- Computed breed-level averages and examined within-breed variability

### Key EDA Finding: Owner Bias
The most significant finding in EDA was **systematic owner bias** in the negative trait categories. Aggressive and fearful behaviors were heavily right-skewed — most scores clustered at the low end of the scale — suggesting owners underreport negative behaviors in their own dogs. This made those traits unreliable for modeling.

The `oth_traits` group (chasing, excitability, energy, trainability, and attachment-seeking) showed a healthy bell-curve distribution and were retained for further analysis. Trainability was mildly left-skewed (owners also tend to overrate their dogs' trainability), but not severely enough to discard.

### Modeling
Four regression models were trained to predict behavioral scores from breed:

| Model | Best NMSE | Train/Test Gap |
|---|---|---|
| **Linear Regression** | **-0.7486** | **Lowest** |
| Lasso Regression | -0.7536 | Moderate |
| XGBoost | -0.7483 | Moderate |
| Random Forest | -0.7486 | Low |

**Linear Regression** was selected as the final model for its minimal train/test gap and competitive NMSE score — a sign of better generalization on this relatively small dataset.

---

## 📊 Key Results

- Breed does appear to have a **small but detectable correlation** with the five retained behavioral traits
- These differences were **not visually obvious** in plots — they were only surfaced through computational testing
- Aggressive and fearful traits could **not be reliably analyzed** due to owner reporting bias
- A meaningful answer to breed-related aggression questions would require professionally-collected observational data, not owner surveys

---

## ⚠️ Limitations & Future Work

- Owner-reported survey data introduces significant bias, particularly for negatively-perceived behaviors
- Analysis was limited to 10 breeds and 5 traits; a broader study would be more informative
- Additional variables worth exploring: age, sex, "fixed" status, and how the dog was acquired (rescued, vs. bred, vs. other)
- A composite feature combining breed + background factors could help disentangle correlation from causation

---

## 🛠️ Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-EC4E20?style=flat)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-4C8CBF?style=flat)

---

## ✒️ Author

**Lindsey Schaeffer** — Data Scientist  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Lindsey_Schaeffer-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/lindsey-schaeffer/)
[![GitHub](https://img.shields.io/badge/GitHub-lindseyschae-181717?style=flat&logo=github&logoColor=white)](https://github.com/lindseyschae)
