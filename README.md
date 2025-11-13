# Handling Missing Data in Student Budget Analysis  
*A reproducible R project for the treatment and analysis of missing data in student survey datasets.*

---

## 📘 Overview
This project focuses on the **detection, visualization, and imputation of missing data** within a survey dataset of students from the *Pays de la Loire* region (academic year 2023–2024).  
It was developed as part of a **Biostatistics course on missing data**, and aims to ensure reliable and complete analyses despite incomplete information.

**Objectives**
- Identify and quantify missing data across variables  
- Compare multiple imputation techniques  
- Ensure reproducibility and transparency through documented R scripts  

---

## ⚙️ Features
- Automatic simulation of missing data (10% randomly removed entries)  
- Descriptive statistical analysis (univariate and bivariate)  
- Visualization of missing patterns using `{naniar}`  
- Implementation and comparison of three imputation methods:  
  - Binary logistic regression  
  - Mean imputation  
  - Multiple Imputation by Chained Equations (MICE)  
- Data export and reproducible reporting in Quarto/PDF format  

---

## 🧰 Tech Stack
**Language:** R  
**Libraries:** `tidyverse`, `naniar`, `mice`, `ggplot2`, `car`, `PerformanceAnalytics`, `corrplot`, `AER`, `kableExtra`, `openxlsx`, `lmtest`, `sjPlot`  

---

## ⚙️ Installation
Clone the repository and open it in RStudio:

```bash
git clone https://github.com/<your-username>/missing-data-student-budget.git
cd missing-data-student-budget
```

Then, install the required R packages:

```r
install.packages(c("tidyverse", "naniar", "mice", "ggplot2", 
                   "car", "PerformanceAnalytics", "corrplot", 
                   "AER", "kableExtra", "openxlsx", "lmtest", "sjPlot"))
```

---

## 📚 Usage Example

```r
# Import dataset
Budget <- read.xlsx("data/student_budget_data_2023_2024.xlsx")

# Introduce 10% random missing values
source("src/create_missing_values.R")

# Visualize missing data
library(naniar)
gg_miss_upset(Budget)

# Apply MICE imputation
library(mice)
imputed <- mice(Budget, m = 5, method = "pmm", seed = 123)

# Export results
write.csv(complete(imputed), "Budget_imputed.csv", row.names = FALSE)
```

Additional analyses and visualizations are available in the Quarto report (`Rapport_Pierre_Florian.qmd`).

---

## 📂 Project Structure

```
missing-data-student-budget/
│
├── data/                     # Raw and imputed datasets
├── src/                      # R scripts for imputation and analysis
├── rapport/                  # Quarto and PDF reports
├── assets/                   # Visualizations and figures
├── requirements.R             # List of R dependencies
└── README.md
```

---

## 📊 Results
The dataset includes **135 students** and **22 variables** (7 quantitative, 15 qualitative).  
A total of **297 cells (10%)** were randomly deleted to simulate missingness.

Three imputation techniques were compared:  
- Logistic regression showed good performance for binary variables.  
- Mean imputation offered simplicity but introduced bias.  
- MICE provided robust, multivariate consistency.  

Example visualization:

![Missing Data Visualization](./assets/missing_data_upset.png)

---

## 🧠 References
For theoretical and methodological background:
- Vaugoyeau, *Les données manquantes* (course material, 2024)【11†01_cours_donnees_manquantes.pdf】  
- van Buuren, *Flexible Imputation of Missing Data* (2018)  
- Rubin, *Multiple Imputation for Nonresponse in Surveys* (1987)  

---

## 📜 License
This project is released under the **MIT License**.  
© 2025 Pierre Quintin de Kercadio and Florian Crochet

---

## 👤 Authors
**Pierre Quintin de Kercadio**  
[GitHub Profile](https://github.com/PierreQDK)  

**Florian Crochet**  
[GitHub Profile](https://github.com/floriancrochet)

*Master 1 – Econometrics & Statistics, Applied Econometrics Track*

---

## 💬 Acknowledgments
This work was carried out within the framework of the *Biostatistics 1 (Missing Data)* course taught by **Marie Vaugoyeau**.  
Special thanks to the open-source R community for their contributions to reproducible data analysis.
