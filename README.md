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

Insulin , Dual Density Plot (KDE by Outcome)

<img width="935" height="534" alt="Screenshot 2025-11-29 235547" src="https://github.com/user-attachments/assets/94c7a727-1f9e-4bb7-b14e-ffc8ef4cea86" />

A Kernel Density Estimate (KDE) plot was created for Insulin levels based on the target variable Outcome:

Outcome = 0 (Non-diabetic) — Blue
Distribution is concentrated at lower values (peak ~80–90) and relatively sharp, indicating a higher density of samples in the lower range.

Outcome = 1 (Diabetic) — Orange
Distribution is concentrated at higher values (peak ~150–170) and more spread out.

Key observations:

Separability: Values below 100 mainly belong to non-diabetic patients, and values above 150 mainly belong to diabetic patients.

Overlap: The ~100–180 range indicates cases where insulin alone cannot clearly distinguish diabetes; other features should be considered.

Zero values: Attention should be paid to zero (missing/invalid) values, as the blue peak may partly reflect them.

Conclusion / Insight:

Insulin is a strong feature for differentiating diabetic and non-diabetic patients.

Samples in the overlap region require additional features (Glucose, BMI, Age) for accurate classification.

For modeling, this feature should be included along with other key variables, and zero values should be cleaned or imputed.

Glucose , Density Plot by Outcome

<img width="967" height="546" alt="Screenshot 2025-11-30 001445" src="https://github.com/user-attachments/assets/d5ba2bef-886a-464a-aef5-abf1ae85c116" />

This Kernel Density Estimate (KDE) plot shows the distribution of Glucose (plasma glucose concentration) based on Outcome (diabetes diagnosis):

Outcome = 0 (Non-diabetic) — Blue
Distribution is concentrated around normal values (~100) and is relatively symmetric.

Outcome = 1 (Diabetic) — Orange
Distribution is shifted toward higher values (peak ~130–140) with right skewness, indicating the presence of high glucose cases.

Key observations:

Overlap: ~100–120 range shows partial overlap between the two groups.

Separability: Values above 125–130 mostly belong to the diabetic group.

Diagnostic threshold: Around 120, where the density of Outcome=1 surpasses Outcome=0, can be considered as an approximate boundary.

Conclusion / Insight:

Glucose is likely the strongest predictive feature for diabetes.

Higher glucose values are directly associated with diabetes risk.

For modeling, this feature is highly informative, but due to overlap in the borderline range, other features should also be considered.

BMI , Density Plot by Outcome

<img width="1006" height="618" alt="Screenshot 2025-11-30 002753" src="https://github.com/user-attachments/assets/ca327f54-962f-425c-a1db-3cf6b291ed83" />

This Kernel Density Estimate (KDE) plot shows the distribution of BMI (Body Mass Index) based on Outcome (diabetes diagnosis):

Outcome = 0 (Non-diabetic) — Blue
Distribution is concentrated around 29–30 (overweight to class 1 obesity) and relatively symmetric.

Outcome = 1 (Diabetic) — Orange
Distribution is shifted toward higher values with a peak around 33–34 (obesity). Right skewness is present with a long tail toward very high BMI.

Key observations:

Overlap: 25–35 range shows substantial overlap between groups.

Separability: BMI < 25 → low diabetes probability, BMI > 35 → high diabetes probability.

Zero values: Attention to zero/invalid values is necessary; assume invalid values were handled before plotting

Conclusion / Insight:

BMI is an important risk factor for diabetes; mean BMI is higher in the diabetic group.

BMI is a strong predictor, but not as strong as Glucose or Insulin.

For modeling, BMI should be used alongside other features.

Outcome , Bar Plot (Target Variable Distribution)

<img width="557" height="448" alt="Screenshot 2025-12-01 135624" src="https://github.com/user-attachments/assets/6a4f9981-9b5b-4763-9ff1-7f671e14bd3b" />

This bar plot shows the distribution of the Outcome variable in the Pima Indians Diabetes dataset. This visualization is crucial for understanding the presence of class imbalance in the data.

Key Observations

Outcome = 0 (Non-Diabetic): ~500 samples

Outcome = 1 (Diabetic): ~268 samples

Total observations: ~768

This means that the non-diabetic class has almost twice as many samples as the diabetic class.

Analysis of Average Glucose by Outcome

<img width="661" height="441" alt="Screenshot 2025-12-01 142537" src="https://github.com/user-attachments/assets/33fef361-f505-4299-a7ce-495be22d8783" />

This visualization examines the average blood glucose level (Glucose) across two groups of patients: diabetic and non-diabetic. A bar chart was used to illustrate the mean Glucose value for each outcome class.

Key Observations

Average Glucose for Non-Diabetic patients (Outcome = 0):
Approximately 110.

Average Glucose for Diabetic patients (Outcome = 1):
Approximately 141.

Significant difference between the two groups:
On average, diabetic individuals have 31 units higher glucose levels compared to non-diabetic individuals.

Conclusion

This clear difference confirms that Glucose is a strong predictive feature for diabetes in this dataset.
These findings are also consistent with earlier visualizations such as the Glucose KDE plot, where the distribution for diabetic patients shifted noticeably toward higher values.

Analysis of Average BMI by Outcome

<img width="638" height="448" alt="Screenshot 2025-12-01 143749" src="https://github.com/user-attachments/assets/c5135ccc-8257-4c28-951d-9ba6031414a8" />

This bar plot compares the average Body Mass Index (BMI) between diabetic and non-diabetic patients. It provides a quantitative perspective on how obesity correlates with diabetes in the Pima Indians Diabetes dataset.

Key Observations

Average BMI for Non-Diabetic patients (Outcome = 0):
Approximately 30.5, which falls within the overweight to Class I obesity range.

Average BMI for Diabetic patients (Outcome = 1):
Approximately 35, corresponding to Class II obesity in medical classification.

Clear difference between the two groups:
Diabetic individuals have, on average, about 4.5 units higher BMI than non-diabetic individuals.

Conclusion

This visualization clearly confirms the strong link between higher BMI and increased likelihood of diabetes in this dataset.
These findings align with previous visual analyses, such as the BMI KDE plot, where the distribution for diabetic patients was shifted toward higher BMI values.

Analysis of Average Insulin by Outcome

<img width="665" height="448" alt="Screenshot 2025-12-01 150533" src="https://github.com/user-attachments/assets/04ad3aa4-3b6a-43a1-a208-3d0ad92c6305" />

This bar plot compares the average serum insulin levels between diabetic and non-diabetic patients. It provides a quantitative view of how insulin levels vary across the two classes of the target variable (Outcome).

Key Observations

Average Insulin for Non-Diabetic patients (Outcome = 0):
Approximately 125 units.

Average Insulin for Diabetic patients (Outcome = 1):
Approximately 185 units.

Significant difference:
Diabetic individuals have, on average, about 60 units higher insulin levels compared to non-diabetic individuals.

Conclusion and Importance

The plot highlights Insulin as a strong predictive and discriminative feature in the dataset.

The noticeable difference between the two groups aligns with known physiological concepts such as:

Insulin resistance

Hyperinsulinemia
These factors are commonly associated with or precede Type 2 diabetes, supporting the significance of this feature in further modeling and analysis.

Scatter Plot Analysis: Glucose vs. BMI by Outcome

<img width="811" height="521" alt="Screenshot 2025-12-01 182712" src="https://github.com/user-attachments/assets/50719648-254b-4b45-9341-e80a6e70736a" />

This scatter plot visualizes the relationship between Glucose (blood sugar level) and BMI (Body Mass Index), with points color-coded based on the target variable Outcome (0 = Non-Diabetic, 1 = Diabetic).
It provides valuable insight into how the combination of these two features contributes to diabetes prediction.

Key Observations

Non-Diabetic Group (Outcome = 0 , Blue):
Most blue points appear in the lower-left region, indicating lower BMI and lower glucose levels.

Diabetic Group (Outcome = 1 , Orange):
Orange points are more concentrated in the upper-right region, reflecting higher BMI and higher glucose levels.

Overlap Region:
A noticeable overlap exists between Glucose levels of 90–140 and BMI levels of 25–35.
This suggests that neither feature alone perfectly separates the two classes.

Combined Separability

Low-Risk Zone:
Glucose < 100 and BMI < 25 → Almost all points are blue (very low diabetes risk).

High-Risk Zone:
Glucose > 150 and BMI > 35 → Orange points dominate (high diabetes risk).

Conclusion

Positive Correlation:
Higher BMI tends to be associated with higher glucose levels.


Strong Combined Predictive Power:
Together, these features help machine learning models draw a meaningful decision boundary between classes.

Feature Engineering Potential:
This visualization suggests the possibility of creating new engineered features, such as a combined metabolic risk index, to enhance model performance.

Scatter plot , Glucose vs Age colored by Outcome

<img width="838" height="536" alt="Screenshot 2025-12-01 183121" src="https://github.com/user-attachments/assets/7303a8bc-e314-4eb5-bae6-b1a8458953d7" />

The scatter plot visualizes the joint relationship between Glucose (blood sugar) and Age, with points colored by Outcome (blue = non-diabetic, orange = diabetic). This view helps assess how age and glucose together relate to diabetes risk.

Key observations

Glucose strong across ages: Diabetic points (orange) consistently occupy higher glucose values across all ages—Glucose is a strong independent predictor.

Risk increases with age: The density of diabetic points rises with age, particularly after ~40 years.

Overlap region: Approximate overlap around Glucose ≈ 90–140 and Age ≈ 25–45 where class separation is unclear using only these two features.

Relatively clear zones:

Low-risk: Age < 35 and Glucose < 120 → mostly non-diabetic.

High-risk: Age > 50 and Glucose > 160 → mostly diabetic.

Conclusion & modeling implications

Interactive effect: Age alone is weaker, but combined with Glucose it amplifies diabetes risk — “high Glucose + older age” is a notably strong signal.

Modeling use: Consider modeling interaction terms (e.g., Age * Glucose) or age-stratified thresholds to improve classifier performance.

Practical suggestion: Use the scatter insights to engineer features or to set stratified decision thresholds in downstream models.

Scatter Plot: BMI vs Age (Colored by Outcome)

<img width="684" height="520" alt="Screenshot 2025-12-01 194211" src="https://github.com/user-attachments/assets/6e5be2e0-5bc9-4011-bee6-8fb2ee4dd9b4" />

This chart visualizes the relationship between Age (x-axis) and BMI (y-axis), with points colored based on Outcome (0 = non-diabetic, 1 = diabetic). The plot helps identify how the combination of age and body mass index relates to the likelihood of diabetes.

Key Insights

Age Effect:
Younger individuals (20–30 years) mostly fall into the non-diabetic class, especially at lower BMI values.
As age increases—particularly above 40—the density of diabetic cases rises across almost all BMI ranges.

BMI Effect:
Higher BMI values (35+) show a noticeably larger concentration of diabetic cases.
Lower BMI values (<25) are strongly associated with non-diabetic outcomes across all ages.

Combined Risk Pattern:

Low-risk zone: Age < 40 and BMI < 25 — mostly non-diabetic.

High-risk zone: Age > 45 and BMI > 35 — high concentration of diabetic cases.

Overlap zone: Age 20–40 with BMI 25–35 — significant overlap between both classes, indicating limited separability using these two features alone.

Conclusion

There is no strong linear correlation between Age and BMI, but both variables independently contribute to diabetes risk. Their combined interaction strengthens the predictive signal, making them valuable inputs for machine learning models. However, for better class separation, additional metabolic features (e.g., Glucose, Insulin) are necessary.

Scatter Plot: Insulin vs Glucose (Colored by Outcome)

<img width="825" height="533" alt="Screenshot 2025-12-01 195133" src="https://github.com/user-attachments/assets/c37b863d-af4d-47f0-9dd8-c4f63526bebd" />

This scatter plot visualizes the relationship between Glucose (x-axis) and Insulin (y-axis), with points colored based on the Outcome variable (0 = non-diabetic, 1 = diabetic). Since both features are strong predictors of diabetes, this plot is one of the most important bivariate analyses in the dataset.

Key Observations

Strong Positive Correlation:
There is a clear positive correlation between glucose levels and insulin levels. As glucose increases, insulin tends to rise in both diabetic and non-diabetic groups.

High Class Separability:
The distinction between the two outcome classes is much clearer here than in many other feature pairs.

Low-risk region: Glucose < 100 and Insulin < 100 are predominantly non-diabetic.

High-risk region: Glucose > 150 and Insulin > 200 show a strong dominance of diabetic cases.

Overlap zone: Glucose 100–150 and Insulin 100–200 display mixed points, indicating cases that require additional diagnostic information.

Note on Zero Values:
Insulin values of zero often indicate missing data in the original dataset. The low density near y = 0 suggests such values were either removed or imputed before plotting.

Conclusion

The combination of Glucose and Insulin provides one of the strongest two-dimensional separations in the dataset. A machine learning model can form an effective decision boundary using only these two features, and they are expected to carry significant weight in predictive models for diabetes.

Scatter Plot: BloodPressure vs Age (Colored by Outcome)

<img width="864" height="539" alt="Screenshot 2025-12-01 210852" src="https://github.com/user-attachments/assets/8a492cdf-8464-40f7-810d-ca9a79787098" />

This scatter plot visualizes the relationship between Age (x-axis) and BloodPressure (y-axis, diastolic blood pressure), with points colored by Outcome (0 = non-diabetic, 1 = diabetic).

Key Observations
1. Relationship Between Age and Blood Pressure

There is a weak positive correlation between Age and BloodPressure.
While older individuals tend to show slightly higher blood pressure on average, the pattern is highly scattered and inconsistent.

2. Weak Class Separability

Compared to features such as Glucose or Insulin, this plot shows very weak separability between diabetic and non-diabetic groups.
Blue and orange points extensively overlap across almost the entire range.

3. Blood Pressure Distribution

Most data points from both classes fall within the 60–80 range.

Very low (<50) and very high (>90 or 100) blood pressure values appear in both classes.

No near-zero values are present, suggesting missing-value placeholders (often zeros) were removed or corrected prior to plotting.

4. Age Does Not Improve Separation

Even at older ages, both diabetic and non-diabetic points remain highly mixed.
Age alone does not create a meaningful boundary for distinguishing between the two outcomes.

Conclusion and Modeling Impact

Weak predictive power: BloodPressure alone, or even combined with Age, is not a strong predictor of diabetes in this dataset.

Low model weight: Machine learning models will likely assign low importance to this feature compared to strong metabolic predictors like Glucose and Insulin.

Interpretation: Diastolic blood pressure in this dataset appears to be only weakly associated with diabetes diagnosis.

