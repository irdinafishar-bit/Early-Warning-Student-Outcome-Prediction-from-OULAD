# Online-Learning-Engagement-Performance
Early-warning academic outcome prediction using the Open University Learning Analytics Dataset (OULAD). Benchmarks non-traditional architectures, Hyperdimensional Computing (HDC) and Weight-Agnostic Neural Networks (WANN), against tree-based ensembles across Standard, RFE, and Autoencoder feature paradigms.

# Online Learning Engagement & Performance

## 📌 Project Overview
In blended and asynchronous Open Distance Learning (ODL) environments, student attrition and sudden withdrawal are critical institutional challenges. Traditional academic analytics often detect underperformance too late—typically after mid-term exams or major assignment deadlines.

This project develops an early-warning predictive system using the **Open University Learning Analytics Dataset (OULAD)** to classify student academic outcomes into a binary **Pass vs. Non-Pass** target (consolidating *Pass/Distinction* vs. *Fail/Withdrawn*). Crucially, this study explores whether non-traditional computational frameworks, **Hyperdimensional Computing (HDC)** and **Weight-Agnostic Neural Networks (WANN)**, can match or surpass traditional ensemble baselines, particularly under aggressive feature compression.

---

## 📊 Dataset: Open University Learning Analytics Dataset (OULAD)
* **Source:** [Open University Knowledge Media Institute](https://analyse.kmi.open.ac.uk/open-dataset)
* **Scale:** 32,593 unique student records across 7 distinct modules and multiple chronological presentations.

### Relational Schema
The pipeline integrates seven relational CSV tables into a unified master matrix (`master_dataset.csv`):
1. **`studentInfo.csv`**: Core student demographics, socio-economic index (`imd_band`), prior education, studied credits, disability status, and `final_result`.
2. **`studentRegistration.csv`**: Module registration and withdrawal timelines (`date_registration`, `date_unregistration`).
3. **`studentVle.csv`**: Transactional Virtual Learning Environment (VLE) interaction logs (`sum_click`, `date`).
4. **`vle.csv`**: Semantic lookup mapping `id_site` to virtual resource types (e.g., *forumng, quiz, resource, homepage*).
5. **`courses.csv`**: Module catalog and presentation durations (`module_presentation_length`).
6. **`studentAssessment.csv`**: Student submission dates, late indicators (`is_banked`), and assessment scores (0–100).
7. **`assessments.csv`**: Assessment types (TMA, CMA, Final Exam), nominal deadlines, and grade weights.

---

## ⚙️ Data Integration & Feature Engineering
Following the methodology established by Yulianto et al. (2025), our preprocessing pipeline performs:
* **Temporal Click Splitting**: Aggregates total VLE interactions (`sum_click`) and splits them into pre-course engagement (`Before_Clicks`, `date < 0`) and active-course engagement (`After_Clicks`, `date >= 0`).
* **Formative Assessment Aggregation**: Computes student-level `mean_score` across module assessments.
* **Dual-Stage Imputation**: Applies linear interpolation (`interpolate(method='linear')`) followed by column-mean fallback (`fillna`) to handle missing records without introducing heavy bias.
* **Academic Domain Encoding**: Categorizes modules into **STEM** (`BBB`, `DDD`, `EEE`, `FFF`, `GGG`) and **Social Sciences** (`AAA`, `CCC`).

---

## 📈 Key Exploratory Data Analysis (EDA) Insights
* **Balanced Binary Target**: Consolidating outcomes yields a near-symmetric split of **47.20% Pass** (15,385 records) and **52.80% Non-Pass** (17,208 records).
* **Behavioral Engagement**: `sum_click` exhibits a strong right-skew; Non-Pass students cluster sharply near zero engagement, while Pass students show sustained VLE interaction.
* **Assessment Boundary**: `mean_score` displays clear class separation, with Pass students clustering in the 70–90 score range.
* **Socio-Economic & Demographic Trends**: Higher prior educational attainment, lower deprivation indices (higher `imd_band`), and mature age brackets (`35–55` and `55<=`) correlate with higher retention and pass rates.

---

## 🎯 Research Benchmark & Experimental Paradigms
This project benchmarks models against the peer-reviewed baseline by **Yulianto et al. (2025)** (*"Binary Classification of Academic Outcomes Using Ensemble Learning and Neural Networks: A Case Study on OULAD"*) across three feature paradigms:
1. **Standard Paradigm**: Full 38-feature consolidated matrix.
2. **Recursive Feature Elimination (RFE)**: Top 5 features selected via Random Forest.
3. **Autoencoder Paradigm**: 5-dimensional latent representation trained over 50 epochs.

### Reference Baseline Targets (Standard 38-Feature Track — Pass vs. Non-Pass)
| Model | Accuracy | Precision | Recall | F1 Score | ROC AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Gradient Boosting** | **75.50%** | 64.90% | **76.60%** | **69.60%** | **83.40%** |
| **LightGBM** | **75.50%** | 64.90% | 75.50% | 69.40% | **83.40%** |
| **Random Forest** | 74.20% | 66.00% | 66.40% | 65.00% | 82.80% |
| **AdaBoost** | 74.20% | 66.30% | 65.10% | 64.50% | 82.80% |
| **Voting Classifier** | 72.00% | **67.80%** | 49.70% | 54.90% | 82.40% |
| **Deep Neural Network** | 69.60% | 62.09% | 49.72% | 55.22% | *N/A* |

### Proposed Alternative Architectures
* **Hyperdimensional Computing (HDC)**: Uses high-dimensional vector-symbolic mapping for low-compute, single-pass learning resilient to sparse binary demographic features.
* **Weight-Agnostic Neural Networks (WANN)**: Evaluates network topologies rather than fine-tuned weights to test whether relational behavioral structures alone can drive early-warning predictions.

---

## 🚀 Getting Started

### Prerequisites
* Python 3.8+
* `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`

### Running the Pipeline
1. Clone this repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/Online-Learning-Engagement-Performance.git
   cd Online-Learning-Engagement-Performance
