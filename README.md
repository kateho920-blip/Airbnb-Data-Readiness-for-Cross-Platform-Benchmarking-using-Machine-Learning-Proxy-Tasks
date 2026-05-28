# 📌 Airbnb's Data Readiness for Cross-Platform Benchmarking
> **A Comparative Analysis with Booking.com and Tripadvisor using Machine Learning Proxy Tasks**

[![Academic Project](https://img.shields.io/badge/Academic-HKBU_BBA_FYP-purple?style=for-the-badge)](https://github.com/kateho920)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/kateho920)
[![SQL](https://img.shields.io/badge/SQL-0064a5?style=for-the-badge&logo=postgresql&logoColor=white)](https://github.com/kateho920)
[![Machine Learning](https://img.shields.io/badge/Machine_Learning-F29111?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://github.com/kateho920)

---

## 📖 Project Overview
This repository contains the source code, data methodology, and findings for our Final Year Project (FYP) at Hong Kong Baptist University (HKBU). 

While Online Travel Platforms (OTAs) process massive volumes of user-generated reviews monthly, **a high volume of data does not inherently equal machine learning (ML) readiness**. This project tackles the structural deficiencies in review data—such as positivity bias, the ceiling effect, and label noise caused by "inherited ratings"—by introducing a standardized, multi-dimensional evaluation framework.

### 🎯 Research Objectives
1. **Develop the ADDI Framework:** Create a novel, 5-dimensional framework to mathematically assess review data maturity for ML.
2. **Construct a Benchmark Dataset:** Integrate and standardize 4.38M+ structured and unstructured review rows across Airbnb, Booking.com, and TripAdvisor across three distinct market scales (London, Istanbul, Hong Kong).
3. **Evaluate via Practical ML Tasks:** Test dataset readiness using four proxy downstream tasks: Ranking, Recommendation, Trust & Safety, and Cross-platform Transfer.
4. **Provide Actionable Recommendations:** Formulate empirical strategies for platform data engineers and internal ML teams.

---

## 📐 The Airbnb Data Development Index (ADDI) Framework
Moving beyond basic data hygiene checks, the **ADDI** is a weighted, multi-dimensional score that directly links technical data properties to downstream ML usability:

$$ADDI = 0.15 \times Coverage + 0.20 \times Completeness + 0.20 \times Consistency + 0.20 \times Quality + 0.25 \times Strategic Readiness$$

### 📊 ADDI Assessment Results
Our benchmark dataset achieved an **Overall ADDI Score of 87.73**, indicating very strong overall readiness for benchmarking, though with a critical bottleneck:

* **Consistency (98.27):** Near-perfect schema alignment and rating scale normalization.
* **Quality (96.34):** Excellent hygiene with strong uniqueness and adequate text length after processing.
* **Coverage (93.33):** High volume and entity count, though geographic metadata usability left room for alignment.
* **Completeness (88.77):** Core fields are highly populated, but limited by review date availability on certain platforms.
* **Strategic Readiness (68.22) ⚠️ The Bottleneck:** Severely bottlenecked by low usable row ratios due to missing exact dates and inherited label noise.

---

## 🛠️ Tech Stack & Methodology
* **Language & Core Libraries:** Python (Pandas, NumPy, Scikit-learn)
* **Text Processing:** TF-IDF (Term Frequency-Inverse Document Frequency) for text length and informativeness analysis.
* **ML Models Used:** Logistic Regression and K-Nearest Neighbors (KNN) used as proxy classifiers to evaluate the data signal objectively.
* **Data Scale:** 4.38 Million total reviews (Airbnb: 1.67M | Booking.com: 1.83M | TripAdvisor: 0.88M) across London, Istanbul, and Hong Kong.

---

## 🚀 Key Empirical Results from ML Proxy Tasks

1. **City/Entity Ranking Proxy:** Booking.com displayed the strongest, most granular ranking signal. Airbnb showed moderate, usable performance but is limited by its lack of direct review-level ratings (relying instead on inherited listing-level averages).
2. **Recommendation Proxy:** Rich entity and location metadata successfully support similarity matching. Airbnb demonstrated a clearer, more structured city-level classification (96% comparable pair rate).
3. **Trust & Safety Proxy:** Airbnb contained a notably higher rate of copied/template-like reviews (2.68%) compared to competitors. Applying our weak-supervision template removal filter successfully trimmed 70,730 noisy rows (1.72%). This reduced exact text overlap while keeping model performance (F1-score) completely stable, proving that data quality control directly preserves the core ML signal.
4. **Cross-Platform Transfer Proxy:** Model transferability proved highly asymmetric. Models trained on one platform experienced a strategic readiness gap when predicting target data on another, largely due to mismatched rating scales and platform-specific review styles.

---

## 📈 Strategic Recommendations for Airbnb
To close the strategic readiness gap, this project proposes four core data engineering actions:
* **Implement Review-Level Ratings:** Capture granular guest satisfaction at the individual review level instead of forcing models to inherit static listing-level averages.
* **Build System-Generated Review Quality Filters:** Automatically separate organic, user-generated text from system-generated template code and automated comments.
* **Standardize Metadata Schemas:** Align core schemas across entity IDs, dates, and geographic tags to ensure fair, real-time cross-platform benchmarking.
* **Continuous Benchmarking Pipeline:** Build an internal data pipeline to consistently monitor and audit data readiness against core industry competitors over time.

---

## 📁 Repository Structure
```text
├── data/                  # Data schemas and data dictionary (exclude large raw files)
├── src/
│   ├── data_cleaning.py   # Code for template removal and text normalization
│   ├── addi_score.py      # Script computing the ADDI dimensions and formulas
│   └── ml_proxies.py      # Logistic Regression & KNN proxy tasks pipeline
├── screenshots/           # UI captures, performance graphs, and ADDI charts
├── FYP PPT.pdf            # The final presentation slide deck referenced in this study
└── README.md              # Main project documentation
