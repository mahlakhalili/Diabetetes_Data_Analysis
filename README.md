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

📊Glucose , Density Plot (KDE)

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

📊Insulin , Dual Density Plot (KDE by Outcome)

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

📊Glucose , Density Plot by Outcome

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

📊BMI , Density Plot by Outcome

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

📊Outcome , Bar Plot (Target Variable Distribution)

<img width="557" height="448" alt="Screenshot 2025-12-01 135624" src="https://github.com/user-attachments/assets/6a4f9981-9b5b-4763-9ff1-7f671e14bd3b" />

This bar plot shows the distribution of the Outcome variable in the Pima Indians Diabetes dataset. This visualization is crucial for understanding the presence of class imbalance in the data.

Key Observations

Outcome = 0 (Non-Diabetic): ~500 samples

Outcome = 1 (Diabetic): ~268 samples

Total observations: ~768

This means that the non-diabetic class has almost twice as many samples as the diabetic class.

📊Analysis of Average Glucose by Outcome

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

📊Analysis of Average BMI by Outcome

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

📊Analysis of Average Insulin by Outcome

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

📊Scatter Plot Analysis: Glucose vs. BMI by Outcome

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

📊Scatter plot , Glucose vs Age colored by Outcome

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

📊Scatter Plot: BMI vs Age (Colored by Outcome)

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

📊Scatter Plot: Insulin vs Glucose (Colored by Outcome)

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

📊Scatter Plot: BloodPressure vs Age (Colored by Outcome)

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

📊Analysis of Mean Glucose Level by Diabetes Outcome

<img width="675" height="425" alt="Screenshot 2025-12-01 211233" src="https://github.com/user-attachments/assets/d8a4afc0-9221-4dd9-8be3-ac56fdced606" />

This is a simple bar plot that compares the mean value of the Glucose feature across the two categories of the target variable Outcome, providing clear and quantitative insights.

1. Nature of the Chart & Key Variables

Feature analyzed: Mean Glucose level

Grouping: Based on the target variable (Outcome):

Outcome 0: Non-diabetic patients

Outcome 1: Diabetic patients

Y-axis: Mean Glucose value

2. Key Observations (Quantitative Results)

Mean Glucose for Outcome 0 (Non-Diabetic): 110.6

Mean Glucose for Outcome 1 (Diabetic): 142.3

Difference: A clear and significant gap of 31.7 units between the two groups

This difference highlights a strong relationship between glucose levels and diabetes diagnosis.

3. Conclusion & Relevance for Modeling

Strong predictive indicator:
The chart quantitatively confirms that Glucose is the strongest discriminative feature in this dataset.

Aligned with earlier EDA:
This observation is consistent with the Glucose KDE plot, where the diabetic group showed a noticeable shift toward higher values.

Modeling importance:
Machine learning models are expected to assign high importance to this feature, given the strong difference in group means.

📊Analysis of Class Distribution (Outcome Counts)

<img width="699" height="432" alt="Screenshot 2025-12-01 220047" src="https://github.com/user-attachments/assets/77e60d8b-dbab-4e43-9773-5ba781eb3480" />

This is a simple bar plot that shows the count of each target class (Outcome), clearly highlighting the class imbalance in the dataset.

1. Nature of the Chart & Feature

Feature analyzed: Outcome (target variable, diabetes diagnosis)

Meaning of values:

Non-Diabetic (0): Patients without diabetes

Diabetic (1): Patients with diabetes

Y-axis: Count of observations in each class

2. Key Observations & Class Distribution

Non-Diabetic (Class 0): 500 patients

Diabetic (Class 1): 268 patients

Total observations: 
500
+
268
=
768
500+268=768

Class imbalance:

Majority Class: Non-Diabetic (0)

Minority Class: Diabetic (1)

Ratio ≈ 500:268 (~65% to 35%) indicates a moderate imbalance in class distribution

3. Conclusion & Modeling Implications

Models trained on this dataset should consider class imbalance to avoid bias toward the majority class.

Techniques such as resampling (oversampling/undersampling) or class-weight adjustments may help improve predictive performance for the minority class.

📊Analysis of Average BMI by Diabetes Outcome

<img width="666" height="427" alt="Screenshot 2025-12-01 221440" src="https://github.com/user-attachments/assets/37cf206d-1b39-4ac9-93c1-668b7377fe04" />

This chart is a bar plot that compares the average BMI (Body Mass Index) across the target variable Outcome (diabetes diagnosis).

1. Nature of the Chart & Feature

Feature analyzed: Average BMI for each group

Grouping by Outcome:

Outcome 0: Non-diabetic patients

Outcome 1: Diabetic patients

Y-axis: Average BMI

2. Key Observations & Numerical Insights

Average BMI for Outcome 0 (Non-diabetic): ≈ 30.5

Average BMI for Outcome 1 (Diabetic): ≈ 35

Significant difference: There is a noticeable difference of ~4.5 units in average BMI between the two groups

3. Conclusion & Modeling Implications

Confirms Obesity as a Risk Factor:

Diabetic individuals in this dataset have, on average, a higher BMI

Medically, this corresponds to Class I and II obesity

Modeling:

BMI can be an important feature in diabetes prediction models, as it provides a clear quantitative distinction between diabetic and non-diabetic patients

📊Analysis of Average Insulin by Diabetes Outcome

This chart is a bar plot that compares the average Insulin level across the target variable Outcome (diabetes diagnosis).

1. Nature of the Chart & Feature

Feature analyzed: Average Insulin (serum insulin level)

Grouping by Outcome:

Non-Diabetic (Outcome 0): Patients without diabetes

Diabetic (Outcome 1): Patients with diabetes

Y-axis: Average Insulin level

2. Key Observations & Numerical Insights

Average Insulin for Non-Diabetic (Outcome 0): ≈ 125

Average Insulin for Diabetic (Outcome 1): ≈ 185

Significant difference: There is a clear difference of ~60 units in average insulin levels between the two groups

3. Conclusion & Modeling Implications

Confirms Insulin as a Strong Predictor:

Diabetic patients in this dataset have significantly higher insulin levels

This aligns with insulin resistance in type 2 diabetes

Consistency with EDA:

The result is consistent with the Insulin density plot, which shows the diabetic group distribution shifted toward higher values

Modeling:

Insulin is a powerful predictive feature and would likely receive a high weight in diabetes prediction models

📊Analysis of Average Blood Pressure by Diabetes Outcome

<img width="657" height="452" alt="Screenshot 2025-12-01 222340" src="https://github.com/user-attachments/assets/b750a2f7-e264-4ac7-85bd-31ae119e9bcb" />

This chart is a bar plot that compares the average diastolic Blood Pressure (BP) across the target variable Outcome (diabetes diagnosis).

1. Nature of the Chart & Feature

Feature analyzed: Average Blood Pressure (diastolic)

Grouping by Outcome:

Non-Diabetic: Patients without diabetes

Diabetic: Patients with diabetes

Y-axis: Average Blood Pressure

2. Key Observations & Numerical Insights

Average BP for Non-Diabetic: ≈ 70

Average BP for Diabetic: ≈ 72.5

Minimal difference: The difference between the two groups is very small (~2–3 units)

3. Conclusion & Modeling Implications

Weak Separability:

Diastolic Blood Pressure alone has poor discriminative power between diabetic and non-diabetic patients

The average difference is negligible

Least predictive importance:

Compared to features like Glucose (mean difference ≈ 31.7) or Insulin (mean difference ≈ 60), Blood Pressure contributes the least to diabetes prediction in this dataset

📊Analysis of Average Age by Diabetes Outcome

This chart is a bar plot that compares the average Age across the target variable Outcome (diabetes diagnosis).

1. Nature of the Chart & Feature

Feature analyzed: Average Age

Grouping by Outcome:

Non-Diabetic: Patients without diabetes

Diabetic: Patients with diabetes

Y-axis: Average Age

2. Key Observations & Numerical Insights

Average Age for Non-Diabetic: ≈ 31 years

Average Age for Diabetic: ≈ 37 years

Significant difference: There is a noticeable difference (~6 years) in average age between the two groups

3. Conclusion & Modeling Implications

Age as a risk factor:

This chart confirms that higher age is an important risk factor for diabetes in this dataset, as the diabetic group has a clearly higher average age

Moderate separability:

Although the difference in average age is not as large as features like Glucose or Insulin, it still provides useful information about diabetes risk

📊Pie Chart Analysis of Target Variable (Outcome)

<img width="745" height="558" alt="Screenshot 2025-12-01 230238" src="https://github.com/user-attachments/assets/a149009f-bf52-4063-a4ed-5d730a5e7e2c" />

This chart is a pie chart showing the relative distribution (percentage) of the target variable Outcome (diabetes diagnosis) in the dataset. It visually highlights class imbalance.

1. Nature of the Chart & Feature

Feature analyzed: Outcome (target variable, diabetes diagnosis)

Meaning of values:

Non-Diabetic (0): Patients without diabetes (blue segment)

Diabetic (1): Patients with diabetes (orange segment)

Metric: Percentage of total observations

2. Key Observations & Percentages

Non-Diabetic (class 0): 65.1% of the dataset

Diabetic (class 1): 34.9% of the dataset

3. Conclusion & Modeling Implications

Class Imbalance:

The chart confirms that the dataset has a moderate class imbalance, with the "Diabetic" class (34.9%) being the minority class.

This is important for modeling, as some algorithms may require adjustment (e.g., class weighting, resampling) to handle the imbalance effectively.

📊Pair Plot Analysis of Key Features

<img width="729" height="618" alt="Screenshot 2025-12-01 230621" src="https://github.com/user-attachments/assets/bfe19b81-e367-4ab8-9d32-c5d6bff0c139" />

This chart is a Pair Plot that shows univariate distributions (on the diagonal) and bivariate relationships (off-diagonal) among four key features: Glucose, BMI, Insulin, and Age, separated by the target variable Outcome (class 0: blue, class 1: orange).

It provides a compact overview of these four features with class separation.

1. 🔬 Univariate Distributions (Diagonal)

The diagonal of the pair plot shows KDE distributions of each feature for each class:

Glucose:

Diabetic distribution (orange) clearly shifted toward higher values.

Non-diabetic peak (blue) around 100, diabetic peak around 120–130.

Strongest univariate separability among all features.

BMI:

Diabetic distribution shifted toward higher BMI (orange peak slightly above blue peak).

Orange distribution has a heavier right tail (very high BMI).

Insulin:

Diabetic distribution clearly shifted to higher insulin levels (orange peak ~150–170 vs. blue peak ~70–90).

Provides very good univariate separation.

Age:

Diabetic distribution shifted toward older ages.

Mean age of the diabetic group is higher.

2. 📉 Bivariate Relationships (Off-Diagonal)

Off-diagonal plots show scatter plots, highlighting correlations and combined separability:

Glucose vs. Insulin (Row 1, Column 3):

Strongest positive correlation and best combined separability.

Diabetic points (orange) concentrated at high glucose and high insulin.

Glucose vs. BMI (Row 1, Column 2):

Positive correlation observed.

Diabetic points mostly in the upper-right (high glucose and high BMI).

Glucose vs. Age (Row 1, Column 4):

With increasing age, density of diabetic points increases, especially at high glucose levels.

BMI vs. Insulin (Row 2, Column 3):

Positive correlation.

Higher BMI tends to correspond to higher insulin levels.

Provides relatively good separability.

BMI vs. Age (Row 2, Column 4):

Weak correlation.

Separability is lower, but diabetic points are denser in the high BMI and high age region.

3. 💡 Overall Conclusions for Modeling

Strongest predictors: Glucose and Insulin, individually and combined, provide the best information for diabetes prediction.

Combined risk factors: BMI and Age are important risk factors that improve model predictive power when combined with Glucose.

High overlap region: In all scatter plots, the central region (e.g., Glucose 100–140) shows considerable class overlap, indicating that strong decision boundaries are needed for this region.

📊Correlation Heatmap Analysis

<img width="865" height="703" alt="Screenshot 2025-12-01 231200" src="https://github.com/user-attachments/assets/c63975a8-49a6-42bf-a6c4-41c935125e81" />

This chart is a Correlation Heatmap showing the strength and direction of linear relationships between each pair of features in the dataset. This analysis is crucial for understanding data structure and feature selection.

1. Chart Nature and Color Scale

Color scale: Represents the Pearson Correlation Coefficient, ranging from -1.0 (perfect negative correlation) to 1.0 (perfect positive correlation).

Dark red (close to 1): Strong positive correlation (as one increases, the other also increases).

Dark blue (close to -1): Strong negative correlation (as one increases, the other decreases).

White/light (close to 0): Weak or no linear correlation.

Key conclusion:

Glucose (0.50), Insulin (0.35), and BMI (0.31) are the strongest predictors of diabetes (Outcome) and should have the most weight in a machine learning model.

 Feature-to-Feature Correlation :

This section helps identify multicollinearity that may harm modeling:

Glucose & Insulin (0.63): Strong positive correlation. Medically logical as higher glucose usually triggers higher insulin production.

BMI & SkinThickness (0.69): Very strong positive correlation. Logical, since skin thickness generally increases with BMI. In modeling, one may need to remove or combine these features (e.g., PCA) to avoid multicollinearity.

Pregnancies & Age (0.55): Strong positive correlation. Older women generally have more pregnancies.

BMI & BloodPressure (0.31): Moderate positive correlation, indicating a link between obesity and blood pressure.

📝 Summary of Findings

Feature prioritization: Glucose is the strongest predictor, followed by Insulin and BMI.

Multicollinearity: BMI/SkinThickness and Glucose/Insulin show strong internal correlations that should be considered during modeling.

Consistency: These findings quantitatively confirm our earlier analyses from scatter plots and mean comparisons.

📊BMI Distribution Box Plot Analysis Based on Outcome

<img width="829" height="582" alt="Screenshot 2025-12-01 231454" src="https://github.com/user-attachments/assets/97d9cab6-46d4-4d4a-8eef-f0385e47e258" />

This chart is a Box Plot comparing the distribution of BMI (Body Mass Index) across the target variable Outcome.

1. Chart Nature and Features

Feature analyzed: BMI (Body Mass Index)

Grouping by Outcome:

0 (left – teal/blue): Non-Diabetic

1 (right – yellow): Diabetic

Key elements of a box plot:

Median (middle line): The central value of the distribution.

Box (Interquartile Range – IQR): The range between the 25th percentile (Q1) and 75th percentile (Q3).

Whiskers (lines outside the box): Represent the typical range of data.

Outliers (individual points): Values outside the typical range.

Statistical Conclusions and Modeling Implications

Risk factor confirmation: The chart clearly shows that higher BMI is a significant risk factor for diabetes. The center and quartiles for the diabetic group are shifted upward.

Moderate separability: Although the difference in medians (~4 units) is notable, the high IQR overlap indicates that BMI is a useful predictor but not as strong as features like Glucose.

📊Glucose Distribution Box Plot Analysis Based on Outcome

<img width="800" height="582" alt="Screenshot 2025-12-01 231943" src="https://github.com/user-attachments/assets/c7e80204-76dc-49f0-b723-e75fcb7566cb" />

This chart is a Box Plot comparing the distribution of Glucose (blood sugar) across the target variable Outcome.

1. Chart Nature and Features

Feature analyzed: Glucose (Blood Sugar)

Grouping by Outcome:

0 (left – teal/blue): Non-Diabetic

1 (right – yellow): Diabetic

Statistical Conclusions and Modeling Implications

Strongest univariate separator: Glucose is undeniably the most powerful single feature to distinguish between classes.

Minimal IQR overlap: Provides excellent separability for modeling. A simple threshold on Glucose can give a highly accurate preliminary prediction.

📊Insulin Distribution Box Plot Analysis Based on Outcome

<img width="757" height="583" alt="Screenshot 2025-12-01 232603" src="https://github.com/user-attachments/assets/c2f16c08-693d-4e0e-aaee-161333b4359a" />


This chart is a Box Plot comparing the distribution of Insulin (serum insulin levels) across the target variable Outcome.

1. Chart Nature and Features

Feature analyzed: Insulin (Serum Insulin Levels)

Grouping by Outcome:

0 (left – teal/blue): Non-Diabetic

1 (right – yellow): Diabetic

Box Plot Elements:

Median (Q2): Middle value of the distribution

Interquartile Range (IQR, Q1–Q3): Middle 50% of the data

Whiskers: Typical range of data

Outliers: Extreme values outside the whiskers

Statistical Conclusions and Modeling Implications :

High predictive power: Insulin is a very strong predictor for diabetes.

Median gap: The large difference between medians (~65 units) shows a clear shift toward higher insulin levels in diabetic patients, consistent with insulin resistance.

IQR overlap: Although there is slight overlap in the boxes (~135–160), the central tendency of the two groups is clearly distinct, making it an excellent feature for modeling.

📊Blood Pressure Distribution Box Plot Analysis Based on Outcome

<img width="765" height="495" alt="Screenshot 2025-12-01 233102" src="https://github.com/user-attachments/assets/67062042-2eaf-46b8-802c-b9c7e6715e2c" />

This chart is a Box Plot comparing the distribution of Blood Pressure (Diastolic BP) across the target variable Outcome.

1. Chart Nature and Features

Feature analyzed: Blood Pressure (Diastolic)

Grouping by Outcome:

0 (left – teal/blue): Non-Diabetic (Healthy)

1 (right – yellow): Diabetic

Box Plot Elements:

Median (Q2): Middle value of the distribution

Interquartile Range (IQR, Q1–Q3): Middle 50% of the data

Whiskers: Typical range of data

Outliers: Extreme values outside the whiskers

Statistical Conclusions and Modeling Implications :

Weak predictive power: Compared to Glucose and Insulin, Blood Pressure is a weak feature for discriminating diabetes.

Supports weak correlation: The small median difference, high IQR overlap, and low Pearson correlation with Outcome (0.18) confirm that this feature alone is not very informative.

📊Age Distribution Box Plot Analysis Based on Outcome

<img width="754" height="498" alt="Screenshot 2025-12-01 233419" src="https://github.com/user-attachments/assets/4b7964f3-0e24-4aa3-8932-cb6fd4e4aef9" />

This chart is a Box Plot comparing the distribution of Age across the target variable Outcome.

1. Chart Nature and Features

Feature analyzed: Age

Grouping by Outcome:

0 (left – teal/blue): Non-Diabetic (Healthy)

1 (right – yellow): Diabetic

Box Plot Elements:

Median (Q2): Middle value of the distribution

Interquartile Range (IQR, Q1–Q3): Middle 50% of the data

Whiskers: Typical range of data

Outliers: Extreme values outside the whiskers

Statistical Conclusions and Modeling Implications :

Age as a risk factor: Age is an important risk factor since the median and overall distribution for diabetics clearly shifts toward older ages.

Moderate discriminative power: Despite the IQR overlap, the separation in medians indicates that age provides useful information for diabetes risk prediction.

📊Comprehensive EDA Analysis for Diabetes Dataset


<img width="742" height="495" alt="Screenshot 2025-12-01 234032" src="https://github.com/user-attachments/assets/a57f8841-ed0a-4246-b78f-615935ae39f5" />

<img width="771" height="492" alt="Screenshot 2025-12-01 234047" src="https://github.com/user-attachments/assets/ea7bdf66-b213-465e-ab2c-f1a326e7ce8b" />

<img width="769" height="493" alt="Screenshot 2025-12-01 234102" src="https://github.com/user-attachments/assets/66508330-981a-44b6-b17b-04a83f461152" />

<img width="750" height="498" alt="Screenshot 2025-12-01 234118" src="https://github.com/user-attachments/assets/19ff80a1-1b15-42c8-aa8b-8797d5d9923f" />

1️⃣ Target Variable Distribution & Class Imbalance

Class 0 (Non-Diabetic): 500 observations (65.1%)

Class 1 (Diabetic): 268 observations (34.9%)

Conclusion: The dataset exhibits a moderate class imbalance.

2️⃣ High Predictive Power Features
a. Glucose

Correlation with Outcome: 0.50 (strongest predictor)

Mean:

Non-Diabetic: 110.6

Diabetic: 142.3

Distribution (Density / Box / Violin Plot): The diabetic distribution clearly shifts to higher values. Minimal IQR overlap exists (Class 0 box up to 125, Class 1 starts at 120), indicating excellent discriminative power.

b. Insulin

Correlation with Outcome: 0.35 (strong positive)

Mean:

Non-Diabetic: ~125

Diabetic: ~185

Distribution: Diabetic distribution shifts noticeably to higher insulin levels (median ~175 vs 110 for Non-Diabetic). Strong predictor.

c. BMI

Correlation with Outcome: 0.31 (moderate positive)

Mean:

Non-Diabetic: ~30.8

Diabetic: ~35.2

Distribution: Diabetic distribution shifts to higher BMI values (median ~34 vs 30 for Non-Diabetic). Moderate-to-strong predictor.

3️⃣ Important Risk Factor
Age

Correlation with Outcome: 0.24 (moderate)

Mean:

Non-Diabetic: ~31

Diabetic: ~37

Distribution (Box / Violin Plot): Median age for diabetics (~36) is clearly higher than non-diabetics (~27).

Combined relationships (Glucose vs Age): Diabetic points (orange) are denser in high-glucose and older-age regions, especially above 40 years.

4️⃣ Weak Discrimination & High Overlap
Blood Pressure

Correlation with Outcome: 0.18 (weak)

Mean:

Non-Diabetic: ~70

Diabetic: ~72–73

Distribution (Box / Scatter Plot): Wide IQR overlap and no clear separation in scatter plots (Blood Pressure vs Age) indicate weak predictive power.

5️⃣ Feature-to-Feature Relationships

Heatmap & Pair Plot findings:

Glucose & Insulin: Strongest internal correlation (0.63)

BMI & SkinThickness: Strong correlation (0.69)

Pregnancies & Age: Strong correlation (0.55)

Bivariate relationships: Scatter plot of Insulin vs Glucose shows the best combined discrimination; diabetic points cluster in high-glucose and high-insulin regions.

✅ Summary:

Top predictors: Glucose > Insulin > BMI

Important risk factor: Age

Weak predictor: Blood Pressure

Feature interactions: Glucose-Insulin and BMI-SkinThickness correlations should be considered to avoid multicollinearity in modeling.

📊Joint Plot Analysis (Glucose vs BMI)

<img width="708" height="668" alt="Screenshot 2025-12-01 234708" src="https://github.com/user-attachments/assets/959d7944-9b02-451b-a028-17ff2d3240de" />

<img width="732" height="649" alt="Screenshot 2025-12-01 234725" src="https://github.com/user-attachments/assets/efcbb724-0b03-401a-8886-5201207c24c5" />

This Joint Plot shows the relationship between Glucose and BMI across the dataset, while also displaying the marginal distributions for each variable.

Main Scatter Plot:

A weak positive correlation is observed between Glucose and BMI.

The densest region of the data (dark blue areas) lies roughly within Glucose 100–140 and BMI 25–35.

Glucose Distribution (X-axis Marginal):

The Glucose distribution is approximately normal, with a peak around 100–125.

BMI Distribution (Y-axis Marginal):

The BMI distribution is also approximately normal, with a peak around 30–35.

📊Joint Plot Analysis (Glucose vs Age)

<img width="716" height="662" alt="Screenshot 2025-12-01 235047" src="https://github.com/user-attachments/assets/38280340-ec82-44e2-b533-b5ecc061de32" />

<img width="700" height="655" alt="Screenshot 2025-12-01 235100" src="https://github.com/user-attachments/assets/747d7dc5-bf65-4c9a-89fa-a73e3fa33d1b" />

This plot shows how glucose levels change with age and the overall distribution of these two features in the dataset.

1️⃣ Combined Distribution (Joint Plot)
The plot, displayed as a combination of a scatter plot and a density plot, illustrates the overall data distribution.

Density Plot (Data Concentration):

The highest density (darkest area) is observed in the age range 20–30 years and glucose range 75–125.

This indicates that most individuals in the dataset are young and have normal glucose levels.

As age and glucose increase, data density decreases.

Scatter Plot:

Shows that data points are generally scattered across the full range of age and glucose.

In the lower age range (20–30 years), data points are very concentrated.

📊Joint Plot Analysis (Glucose vs Insulin)

<img width="734" height="665" alt="Screenshot 2025-12-01 235749" src="https://github.com/user-attachments/assets/4af9cc8c-3270-4b3d-8d0e-ff03980d34d9" />

<img width="747" height="668" alt="Screenshot 2025-12-01 235804" src="https://github.com/user-attachments/assets/951d3f2c-d02f-4688-a8b5-7f0fe46218dc" />

This analysis is based on distribution plots, means, and combined scatter/Joint Plots. Insulin and Glucose are two of the most important predictive features for diabetes.

1️⃣ Combined Distribution (Joint Plot) and Internal Correlation

Hexbin / Density Plot:

There is a strong positive correlation between Glucose and Insulin across the dataset.

The highest data density (darkest regions) occurs at Glucose 90–130 and Insulin 75–150.

This pattern aligns with biological behavior, where increased glucose triggers higher insulin secretion.

Correlation Coefficient (Heatmap):

Pearson correlation between Glucose and Insulin is 0.63, the strongest feature-to-feature correlation in this dataset.

2️⃣ Predictive Power by Outcome

Scatter Plot – Insulin vs Glucose by Outcome:

This plot provides the best separability among all 2D feature combinations.

High Separability Region:

Diabetic individuals (Outcome=1, orange) cluster in high Glucose (>140) and high Insulin (>150) regions.

Low Separability Region:

Non-diabetic individuals (Outcome=0, blue) are concentrated in low Glucose (<120) and low Insulin (<100) regions.

Overlap Region:

Significant overlap occurs in the mid-range: Glucose 100–140, Insulin 50–150.

 Key Takeaways :

High Predictive Power: The combination of Glucose and Insulin creates a very strong decision boundary, as diabetic patients are mainly clustered in the high-value region for both features.

Strong Correlation: The strongest internal correlation in the dataset (0.63) is between Glucose and Insulin.

📊Joint Plot Analysis ( Blood Pressure vs Age)

This analysis is based on Joint Plots, density plots, scatter plots, and correlation metrics.

1️⃣ Combined Distribution (Joint Plot) and Internal Correlation

Joint Plots show both bivariate and univariate distributions of Blood Pressure and Age across the dataset.

Density Plot:

The highest data density (darkest area) is observed at Age 20–30 and Blood Pressure 60–75.

There is a weak to moderate positive correlation between Age and Blood Pressure.

Correlation Coefficient (Heatmap):

Pearson correlation between Blood Pressure and Age is 0.34.

2️⃣ Predictive Power by Outcome

Scatter Plot – Blood Pressure vs Age by Outcome:

This plot shows the relationship between these two features separated by diabetes diagnosis (Outcome).

Separability:

Weak separability: Diabetic individuals (Outcome=1, orange) and non-diabetic individuals (Outcome=0, blue) are heavily mixed throughout the plot.

Diabetic density: Although diabetic points slightly cluster at higher Blood Pressure (>80) and older Age (>40), this region is not clearly separable, as many non-diabetic points also exist there.

Key Takeaways :

Weak Predictive Power: Blood Pressure alone, or even combined with Age, provides poor separation between diabetic and non-diabetic individuals.

Moderate Correlation: Age and Blood Pressure have a moderate internal correlation (0.34).

📊Joint Plot Analysis (BMI vs Age)

<img width="728" height="655" alt="Screenshot 2025-12-02 000644" src="https://github.com/user-attachments/assets/11d2d20f-fd7d-4324-8518-68e65f7d55e0" />

<img width="733" height="666" alt="Screenshot 2025-12-02 000317" src="https://github.com/user-attachments/assets/e37961d6-e16b-4563-8691-d3c09a917615" />

This analysis is based on Joint Plots, density plots, scatter plots, and correlation metrics.

1️⃣ Combined Distribution (Joint Plot) and Internal Correlation

Joint Plots display both bivariate and univariate distributions of BMI and Age across the dataset.

Density Plot:

The highest data density (darkest area) is observed at Age 20–30 and BMI 25–35.

There is a weak to very weak linear correlation between Age and BMI.

Correlation Coefficient (Heatmap):

Pearson correlation between BMI and Age is only 0.04, indicating almost no linear relationship between these two features in the overall dataset.

2️⃣ Predictive Power by Outcome

Scatter Plot – BMI vs Age by Outcome:

This plot (also visible in the Pair Plot) shows the relationship between BMI and Age separated by diabetes diagnosis (Outcome).

Separability:

Better separability is observed in the high BMI (>35) and older Age (>40) region.

Diabetic density: At higher ages, diabetic points (Outcome=1, orange) tend to cluster towards higher BMI values.

Overlap: There is heavy overlap between diabetic and non-diabetic points in the younger age (20–35) and medium BMI (25–35) region, indicating that this combination of features is not useful for separation in that range.

 Key Takeaways :

Very Weak Linear Correlation: Overall, BMI and Age have a very weak linear correlation (0.04) across the dataset.

Combined Risk Area: Despite the weak correlation, high BMI combined with older Age marks a region where the density of diabetic patients increases, highlighting a potential combined risk factor.

📊Analysis of BMI Distribution Based on Outcome

<img width="685" height="501" alt="Screenshot 2025-12-02 001147" src="https://github.com/user-attachments/assets/93aef273-38a4-41f5-b70a-c17c21a51aee" />

1️⃣ Box Plot Distribution Analysis

Non-Diabetic Class (Outcome 0):

Most individuals (IQR) fall within BMI 25–35.

This range corresponds to overweight to Class 1 obesity.

Diabetic Class (Outcome 1):

Most individuals (IQR) fall within BMI 31–39.

This distribution is shifted towards Class 2 obesity.

 Key Summary for BMI :

Discriminative Power: BMI is a moderately strong predictor of diabetes with a correlation of 0.31 with Outcome, indicating a clear link between obesity and diabetes in this dataset.

Noticeable Difference: Diabetic individuals have higher BMI on average, and their distribution clearly shifts toward higher obesity ranges.

Overlap: There is significant overlap between the two groups’ boxes (especially in BMI 30–35), which means BMI alone cannot fully separate diabetic from non-diabetic individuals.

🏁 Final Conclusions and Future Directions
1️⃣ Key Findings

Exploratory Data Analysis (EDA) clearly showed that the discriminative power between diabetic and non-diabetic classes heavily depends on two critical features:

Glucose:

The strongest single feature with the highest correlation (0.50) with the target variable (Outcome).

Mean Glucose in diabetic individuals (142.3) is significantly higher than in non-diabetics (110.6).

Insulin:

The second most powerful feature.

In combination with Glucose, it provides the best bivariate separation between classes.

BMI (Body Mass Index):

The third most important factor with a strong correlation (0.31).

Diabetic individuals clearly have a higher BMI distribution (mean 35.2 vs 30.8).

2️⃣ Modeling Impact

Feature Prioritization:
Based on the analysis, Glucose, Insulin, and BMI will be considered the core features in the structure of future Machine Learning models.

Handling Class Imbalance:
The dataset shows a moderate class imbalance (65.1% non-diabetic vs 34.9% diabetic).
Therefore, in the next steps, class imbalance techniques such as SMOTE or class weighting will be applied to prevent model bias toward the majority class.

Thank you for your attention to this analysis. All modeling steps and code will be available in the corresponding directories.

