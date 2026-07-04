# Machine Learning Research on the Stellar Classification Dataset (SDSS17)

## OSF Preregistration Style Documentation
* **Project Title:** Machine Learning Research on the Stellar Classification Dataset (SDSS17)
* **Author:** Dimo Dimov
* **Affiliation:** Machine Learning Course 2026 @ SoftUni

---

## 1. Study Information

### 1.1. Hypotheses
* **Primary Hypothesis ($H_1$):** The Machine Learning model will yield a statistically significant lift in the F1-Score for the overlapping GALAXY and QSO classes, demonstrating its capacity to solve problems where deterministic physics formulas meet observational variance.
* **Secondary Hypothesis ($H_2$):** Engineered multi-band photometric color indexes ($u-g, g-r, r-i, i-z$) reduce semantic multicollinearity inherent in raw telescope magnitudes, functioning as superior linear and non-linear separators.
* **Exploratory Hypothesis ($H_3$):** Randomized single-layer feedforward configurations (Extreme Learning Machines) optimize training latency through analytical pseudo-inverse solving but hit a generalization ceiling in capturing hierarchical boundary warps compared to gradient-descent-driven models.

---

## 2. Design Plan

### 2.1. Study Design
This is a computational, multi-paradigm data science benchmark study using a cross-sectional archival dataset. We evaluate and cross-audit the predictive topography of 7 distinct modeling frameworks categorized into three main control/experimental groups:
1. **Deterministic Baselines:** Pure Redshift Heuristic and Advanced Multi-Law Physical Classifier.
2. **Parametric & Non-Parametric ML:** Softmax Logistic Regression, Random Forest Ensembles, and Leaf-wise LightGBM Boosting.
3. **Neural Architectures:** Analytical Extreme Learning Machines (ELM/ELM Forest) and Iterative Backpropagation MLPs.

### 2.2. Blinding / Integrity Measures
Data leakage prevention protocols are strictly applied. Features are isolated, and empirical scaling parameters ($\mu, \sigma$) are computed strictly on the training partition and transferred onto the test split. Programmatic assertion gates audit test-set statistical independence before modeling.

---

## 3. Sampling Plan

### 3.1. Data Source
* **Dataset Name:** Sloan Digital Sky Survey Data Release 17 (SDSS17)
* **Sample Size:** 100,000 observations of space.
* **Data Exclusion Criteria (Post-Collection Filtering):** Instrumentation drops (e.g., -9999 magnitude anomalies) and outliers are systematically filtered using the standard Interquartile Range (IQR) method applied over safe operational boundaries ($1.5 \times \text{IQR}$).

---

## 4. Variables & Feature Engineering

### 4.1. Variables Matrix
* **Target Variable:** `class` (Discrete, Multi-class: `GALAXY` $\rightarrow 0$, `QSO` $\rightarrow 1$, `STAR` $\rightarrow 2$).
* **Astronomical Predictors:** Continuous coordinates (`alpha`, `delta`) and continuous photometric filters (`u`, `g`, `r`, `i`, `z`, `redshift`).
* **Operational Metadata (Dropped):** Unique hardware logs (`obj_ID`, `run_ID`, `rerun_ID`, `cam_col`, `field_ID`, `spec_obj_ID`, `plate`, `MJD`, `fiber_ID`) are discarded to eliminate artificial overfitting.

### 4.2. Analytical Physics Formulations
To bridge raw data with fundamental astrophysics, we hardcode four deterministic physical laws into our features pipeline:
1. **Relativistic Radial Velocity:** $v = z \cdot c$ (Doppler linear approximation).
2. **Pogson's Flux Conversion:** $F = 10^{-\frac{m}{2.5}}$ (Magnitude-to-linear-flux mapping).
3. **Spectral Slope Index:** $\alpha_{\text{spectral}} = \frac{\log_{10}(F_u / F_z)}{\log_{10}(\lambda_u / \lambda_z)}$ (Power-law continuum).
4. **Color-Temperature Proxy:** Classical $u - r$ filters sequence mapping.

---

## 5. Analysis Plan

### 5.1. Evaluation Metrics & Statistical Audit
Models are evaluated comprehensively to ensure resilience against class imbalance (~65% Galaxies vs. ~11% Quasars):
* **Primary Metric:** Macro-averaged F1-Score (guarantees objective minority class auditing).
* **Secondary Metrics:** Multi-class Confusion Matrices, Precision-Recall curves, and relative feature importance weights tracking Information Gain.

### 5.2. Verification & Convergence Thresholds
Hypothesis confirmation relies on achieving performance parity across bootstrapping (Random Forest) and residual gradient corrections (LightGBM), ensuring empirical stability across distinct loss surfaces.
