This project is an Exploratory Data Analysis (EDA) on the famous Pima Indians Diabetes dataset. It includes medical information for Pima women aged 21 and older, and its goal is to explore patterns associated with diabetes.

 link :https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database

Step 1 Summary , Real Dataset Information

🔍 Dataset Understanding & Initial Inspection (Real Values)

Rows & Columns:
768 rows, 9 columns

Columns:
Pregnancies, Glucose, BloodPressure, SkinThickness,
Insulin, BMI, DiabetesPedigreeFunction, Age, Outcome

Data Types:
All features are numeric.

Missing Values:
There are no formal NaNs, but there are biologically impossible zeros:

Glucose → 5 zeros

BloodPressure → 35 zeros

SkinThickness → 227 zeros

Insulin → 374 zeros

BMI → 11 zeros

Real Descriptive Stats:

Mean Glucose ≈ 120.9

Mean BMI ≈ 31.99

Mean Age ≈ 33.24

Max Pregnancies = 17

Target Distribution (actual):

0 → 500 samples (65.1%)

1 → 268 samples (34.9%)
→ The dataset is imbalanced.

Initial Observations:

Glucose, BMI, and Age appear to be the strongest early indicators.

Insulin contains many zeros and may need imputation.

Dataset requires cleaning before analysis.

Step 2 — Data Cleaning

🧼 1. Identifying Invalid Zero Values

Several features contained biologically impossible zeros:

Glucose → 5 zeros

BloodPressure → 35 zeros

SkinThickness → 227 zeros

Insulin → 374 zeros

BMI → 11 zeros

These were treated as invalid values.

🔧 2. Replacing Invalid Values

All invalid zeros were replaced using the median of each respective column.
Median was chosen to avoid distortion from outliers and preserve natural distribution.

After replacement:

No unrealistic zero values remained

Distributions became smoother and more reliable

🧹 3. Outlier Check

Outliers were reviewed but not aggressively removed, as EDA benefits from analyzing the natural variability of the data.

🔍 4. Final Validation

After cleaning:

No missing or invalid values remained

Dataset became ready for visualization and deeper analysis

Step 3 — Statistical Analysis, Calculations & Feature Grouping

In this step, after data cleaning, detailed statistical analysis and feature grouping were performed to better understand the dataset’s behavior.

🧮 1. Descriptive Statistics

For all features, the following metrics were calculated:

Mean

Median

Min / Max

Standard Deviation

Quartiles (Q1, Q3)

IQR

🔑 Key Real Results:

Mean Glucose ≈ 120.9

Mean BMI ≈ 31.99

Mean Age ≈ 33.24

Max Pregnancies = 17

These stats revealed which features have high variability (Glucose, BMI, Age) and which are more stable.

📊 2. Target Distribution

Actual class distribution:

0 → 65.1% (Non-diabetic)

1 → 34.9% (Diabetic)

Indicating that the dataset is imbalanced.

🗂 3. Feature Grouping (Binning)

Several numeric features were grouped for clearer insights.

● Age Groups:

20–29 → Young

30–39 → Adult

40–49 → Middle-aged

50+ → Senior

● BMI Categories:

< 18.5 → Underweight

18.5–24.9 → Normal

25–29.9 → Overweight

≥ 30 → Obese

● Pregnancies Groups:

0–2 → Low

3–5 → Medium

6+ → High

Grouping made it easier to observe patterns in diabetes prevalence across age, BMI, and pregnancy counts.

🧠 Summary of Step 3

Statistical metrics provided a clear picture of feature distributions.

Class imbalance was confirmed.

Step 4 , Data Visualization

In this step we visually explored the cleaned dataset using Matplotlib . The goal of visualization was to understand feature distributions, detect bivariate relationships, and extract actionable insights for further analysis and modeling.

Grouping helped reveal meaningful patterns such as higher diabetes rates in obese individuals and older age groups.

Each figure contains a short title, a description of plotted data, a few key insights, and suggestions for next steps. Visuals include histograms, boxplots, density plot , countplots for the target, scatterplots, line plot , bar plot , pie plot and a correlation heatmap.

Glucose , Density Plot (KDE)

<img width="824" height="534" alt="Screenshot 2025-11-29 230036" src="https://github.com/user-attachments/assets/abf781a0-d7e1-434e-a178-aadc770b683b" />

The Kernel Density Estimate (KDE) plot was used to examine the distribution of Glucose values in the Pima Indians dataset.

Key observations:

Mode: ~100–110, the most frequent glucose level in the dataset.

Skewness: Right-skewed; higher glucose values are less frequent but significant.

Range: Most observations are concentrated between 75–150.

Outliers: Very high glucose values (>200) exist but are rare.

Conclusion / Insight:

Glucose is a key feature for diabetes prediction.

Right skew indicates notable cases with high glucose levels.

For models sensitive to normality, log transformation or normalization may be considered for this feature.



