# Handling Missing Data in Student Budget Analysis  
*This R project treats and analyzes missing data in a student survey dataset.*

[**Report (PDF – online)**](https://drive.google.com/file/d/157mImsiVVkczX_KFHl7JPwGWtAMXXNEM/view?usp=drive_link)

---

## 🎯 Overview

**Objectives**
- Identify and quantify missing data patterns across survey variables
- Compare three imputation techniques on a student budget dataset
- Ensure reproducibility through documented and versioned R scripts

---

## 🗄️ Data
- **Source:** Student survey, Pays de la Loire region (academic year 2023–2024)
- **Size:** 135 observations, 22 variables (7 quantitative, 15 qualitative)
- **Key Variables:** MOYENNE, ASSIDUITE, RESTAURANT, AGE, STRESS, SOMMEIL, TRAJET
- **Preprocessing:** 10% of cells (297 values) randomly removed to simulate missingness
- **Data Availability:** Provided in `data/student_budget_data_2023_2024.xlsx`

---

## 🧠 Methodology
- **Theoretical Approach:** Binary logistic regression, mean imputation, Multiple Imputation by Chained Equations (MICE)
- **Mathematical Framework:** Predictive Mean Matching (pmm) for continuous variables, logistic regression (logreg) for binary variables, polytomous regression (polyreg) for categorical variables
- **Evaluation Strategy:** Visual comparison of imputed vs. observed distributions via density plots; cross-referencing imputed values against original data

---

## ⚙️ Features
- **Simulate Missingness:** Remove 10% of entries randomly via uniform sampling
- **Analyze Distributions:** Compute univariate and bivariate descriptive statistics
- **Visualize Patterns:** Display missing data patterns using `naniar` upset plots
- **Impute Values:** Apply and compare logistic regression, mean imputation, and MICE
- **Export Results:** Generate reproducible Quarto/PDF reports and imputed datasets

---

## 🧰 Tech Stack
- **Language:** R
- **Numerical Computing & Data Manipulation:** `tidyverse`, `MASS`
- **Econometrics & Statistical Inference:** `car`, `lmtest`, `AER`, `PerformanceAnalytics`, `stats`, `EnvStats`, `mice`, `sjPlot`, `leaps`
- **Data Visualization:** `ggplot2`, `corrplot`, `naniar`, `grid`
- **Reporting & Documentation:** Quarto, `knitr`, `kableExtra`
- **Data Engineering & Acquisition:** `openxlsx`

---

## 📦 Installation

```bash
git clone https://github.com/floriancrochet/master-year1-biostatistics1.git
cd master-year1-biostatistics1
Rscript -e 'install.packages(c("tidyverse", "naniar", "mice", "ggplot2", "car", "PerformanceAnalytics", "corrplot", "AER", "kableExtra", "openxlsx", "lmtest", "sjPlot", "MASS", "EnvStats", "leaps", "grid", "knitr"))'
```

---

## 💻 Usage Example

```r
library(openxlsx)
library(naniar)
library(mice)

Budget <- read.xlsx("data/student_budget_data_2023_2024.xlsx")

gg_miss_upset(Budget)

imputed <- mice(Budget, m = 5, method = "pmm", seed = 123)

budget_complete <- complete(imputed, 3)
write.csv(budget_complete, "Budget_imputed.csv", row.names = FALSE)
```

---

## 📂 Project Structure

```text
master-year1-biostatistics1/
│
├── data/
│   └── student_budget_data_2023_2024.xlsx   # Raw survey dataset
├── report/
│   └── report.pdf                           # Final PDF report
├── LICENSE                                  # MIT License
├── README.md
├── master-year1-biostatistics1.Rproj        # RStudio project file
└── project.qmd                              # Quarto source document
```

---

## 📈 Results

The dataset contains 135 students and 22 variables (7 quantitative, 15 qualitative).
A total of 297 cells (10%) were randomly deleted to simulate missingness.

### Key Findings
- Logistic regression produced consistent imputations for binary qualitative variables.
- Mean imputation offered computational simplicity but introduced distributional bias.
- MICE provided the most robust multivariate consistency across variable types.
- Density plots confirmed that imputed values closely followed observed distributions in the majority of variables.

---

## 📚 References
- Rubin, *Multiple Imputation for Nonresponse in Surveys* (1987)
- van Buuren, *Flexible Imputation of Missing Data* (2018)

---

## 📜 License
This project is released under the MIT License.  
© 2025 Pierre Quintin de Kercadio and Florian Crochet

---

## 👤 Authors
**Pierre Quintin de Kercadio**  
[GitHub Profile](https://github.com/PierreQDK)

**Florian Crochet**  
[GitHub Profile](https://github.com/floriancrochet)

*Master 1 – Econometrics & Statistics, Applied Econometrics Track*

---

## 🤝 Acknowledgments
This work was conducted as part of the Biostatistics 1 (Missing Data) course, supervised by Marie Vaugoyeau.
