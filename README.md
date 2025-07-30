This project analyzes Airbnb listings data to predict whether a host is a "Superhost" based on various features such as host behavior, listing characteristics, and review metrics. 
It includes data cleaning, missing value imputation using Lasso regression, feature engineering, and the application of multiple machine learning models for classification.
Key Features:
Imputed missing values using Lasso Regression for numerical data (e.g., host_years, host_response_rate, host_acceptance_rate)
Applied Logistic Regression, Decision Tree, Naive Bayes, Random Forest, and Support Vector Machine (SVM) classifiers to predict host superhost status
Evaluated model performance using accuracy scores
Automated ETL pipelines, including missing value handling and feature transformation

Data Processing & Imputation
Features Used:
Key variables include host metrics (host_response_rate, host_acceptance_rate), listing details (number_of_reviews, price), review scores, and availability.
Missing Value Handling:
Lasso Regression was used to impute missing numerical values for host_years, host_acceptance_rate, and host_response_rate.
SimpleImputer (mean strategy) handled missing values in model features before training.

ETL Efficiency: Automated pipelines reduced manual preprocessing and improved model input quality.
Prediction Accuracy: Random Forest and SVM performed best, achieving high classification accuracy.
Business Value: This analysis can help Airbnb identify potential Superhosts, improving customer experience and platform trust.

