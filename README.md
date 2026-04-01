# Workforce Compensation Trends — Montgomery County Government

Analysis of public employee compensation data from Montgomery County Government (2019–2024) using data mining techniques in R. The project uncovers hidden patterns in salary distribution, identifies distinct compensation profiles, and examines structural gender disparities across departments and grades.

---

## Dataset

| Property | Details |
|---|---|
| Source | Montgomery County Government — Data.gov (public dataset) |
| Records | 57,000+ observations |
| Period | 2019 – 2024 |
| Variables | Base Salary, Overtime Pay, Longevity Pay, Department, Grade, Gender, Year |
| Access | Publicly available — no download script needed |

---

## My Contributions

### 1. Exploratory Data Analysis (`ALY6040_Project_EDA.Rmd`)
- Removed 3,636 duplicate records and handled missing values
- Conducted outlier detection using boxplots for Base Salary by Gender
- Analyzed salary distributions across 44 departments
- Produced five-number summaries and IQR-based outlier bounds for top departments (POL, HHS, FRS, DOT)
- Built correlation matrix using `corrplot` for numeric salary components

### 2. K-Means Clustering (`Module_3_Technique_Practice.Rmd`)
- Filtered data to 2024 to avoid year-on-year salary drift
- Standardized numeric features (Base Salary, Overtime Pay, Longevity Pay) using z-scores
- Applied Elbow Method via `fviz_nbclust()` to determine optimal k = 4
- Ran K-Means with `nstart = 25` for stability; visualized clusters using PCA-based 2D projection (`fviz_cluster`)
- Profiled 4 clusters by mean/median salary — from entry-level (Cluster 2) to senior/executive (Cluster 1)
- Validated cluster separation using **Kruskal-Wallis test** (p < 0.05) and pairwise **Wilcoxon rank-sum tests**

### 3. SVM Analysis — Gender & Salary (`Module_4_Technique_Practice.Rmd`)
- Converted Base Salary into Low / Medium / High tiers using tertiles
- Built SVM classifier (RBF kernel) on 70/30 stratified split to predict salary level
- Compared models with and without Gender — removing Gender did not affect accuracy
- Applied **one-class SVM** trained on male employees and tested on female records
- Found that 70%+ of female employees deviated from the male compensation structure
- Visualized gender disparity using PCA-based plot of inliers vs. outliers

---

## Key Findings

- **Grade and Year** are the strongest drivers of base salary — structural, not demographic
- **Gender** had minimal predictive power in classification models
- Despite this, the one-class SVM revealed that over **70% of female employees** do not match the male salary pattern — suggesting role access disparities rather than direct pay inequality
- K-Means identified **4 distinct compensation profiles** validated through statistical testing

---

## Tech Stack

`R` `dplyr` `ggplot2` `factoextra` `cluster` `e1071` `caret` `corrplot` `readr`

---

## View Rendered Outputs

Click the links below to view the fully rendered reports with all plots, tables, and results:

| File | Preview |
|---|---|
| Exploratory Data Analysis | [View](https://htmlpreview.github.io/?https://github.com/ashnasolkar/workforce-compensation-trends/blob/main/exploratory_data_analysis.html) |
| K-Means Clustering | [View](https://htmlpreview.github.io/?https://github.com/ashnasolkar/workforce-compensation-trends/blob/main/kmeans_clustering.html) |
| SVM Analysis | [View](https://htmlpreview.github.io/?https://github.com/ashnasolkar/workforce-compensation-trends/blob/main/svm_analysis.html) |

---

## How to Run

1. Download the Montgomery County Employee Salary datasets (2019–2024) from [Data.gov](https://catalog.data.gov/dataset/employee-salaries-2024)
2. Run `ALY6040_Project_EDA.Rmd` first — this generates the cleaned file `Employee_Salaries_2019_to_2024.csv`
3. Run `Module_3_Technique_Practice.Rmd` for clustering analysis
4. Run `Module_4_Technique_Practice.Rmd` for SVM analysis

> All `.Rmd` files can be knitted in RStudio to produce a formatted report.

---

## References

- Montgomery County Government. (2025, April 8). Employee Salaries – 2024 [Dataset]. Data.gov. https://catalog.data.gov/dataset/employee-salaries-2024
- Montgomery County Government. (2025). Employee Salaries – 2024: About the data. Montgomery County Open Data Portal. https://data.montgomerycountymd.gov/Human-Resources/Employee-Salaries-2024/2nq6-auk8/about_data
- Montgomery County Government. (2006). Montgomery County Personnel Regulations (MCPR), Section 1A: Classification and Compensation. Montgomery County Government. https://www.montgomerycountymd.gov/HR/Resources/files/regulation/MCPR01AE.pdf
- Montgomery County Government. (2024). Pay grade and salary distribution FY2024 (PMR 2024 v2). Montgomery County Government. https://www.montgomerycountymd.gov/HR/Resources/Files/Classification/Compensation%20Documents/FY25/PMR%202024%20v2%2005162024.pdf
- Kabacoff, R. (2015). R in action: data analysis and graphics with R (Third edition.). Manning Publications.
