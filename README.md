This project is an Exploratory Data Analysis (EDA) on the famous Pima Indians Diabetes dataset. It includes medical information for Pima women aged 21 and older, and its goal is to explore patterns associated with diabetes.

 link :https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database

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






