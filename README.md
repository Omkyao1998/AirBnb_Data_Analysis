# Airbnb Superhost Prediction (US Listings)

Can we tell which Airbnb hosts will become Superhosts from their behaviour and listing data? This project combines Airbnb listings from 31 US cities, cleans and engineers features, fills missing values with a regression model, and compares five classifiers.

## Business problem

Superhosts get better visibility and more bookings, and they make guests trust the platform. If Airbnb can spot hosts who are *close* to Superhost status, it can nudge them with tips (respond faster, accept more requests, keep reviews up). The same model also shows which host behaviours matter most.

## Data

- [Inside Airbnb](http://insideairbnb.com/) listing files for **31 US cities and regions** (New York, Los Angeles, San Francisco, Chicago, Austin, Seattle, Hawaii and more)
- **261,508 rows** combined, **256,887 unique listings** after removing duplicates
- Target: `host_is_superhost` (yes / no)
- Raw data is not included in this repo

## Approach

**Notebook 1 – `01_data_cleaning.ipynb`**
- Combine 31 city files into one table and keep the latest scrape of each listing
- Clean text fields (names, descriptions, neighbourhoods, amenities) and price
- Engineer host features: years as a host (binned), response-time score, verification score
- Convert yes/no columns to 0/1, one-hot encode room type, flag shared bathrooms and licensed listings
- Prepare listing text (stop-word removal, stemming, lemmatisation) for later text analysis

**Notebook 2 – `02_feature_engineering_and_models.ipynb`**
- Select host, review and availability features
- Fill missing `host_response_rate`, `host_acceptance_rate` and `host_years` using **Lasso regression** (instead of a simple mean)
- Train and compare Logistic Regression, Decision Tree, Naive Bayes, Random Forest and SVM (70/30 split)

## Results

| Model | Test accuracy |
|---|---|
| Logistic Regression | 0.67 |
| Naive Bayes | 0.33 |
| Decision Tree | 1.00* |
| Random Forest | 1.00* |

**\*Known issue – target leakage.** The feature list for the tree models still includes `host_is_superhost` / `host_is_superhost_int`, which is the target itself. That is why those models reach a perfect score. The fix is to drop both columns from the features and re-run; I'm treating the current numbers as not valid until then.

Lessons from this, which I now apply in every project:
- A perfect score is a red flag, not a result. Check the features first.
- Accuracy alone is not enough when classes are unbalanced. Report precision, recall and F1, and compare against a simple baseline (always predicting "not Superhost").

## Tech stack

Python · pandas · scikit-learn · NLTK · gensim · Google Colab

## How to run

```bash
git clone https://github.com/Omkyao1998/AirBnb_Data_Analysis.git
cd AirBnb_Data_Analysis
pip install -r requirements.txt
```

1. Download listing files from Inside Airbnb into a `data/` folder.
2. Run `01_data_cleaning.ipynb`, then `02_feature_engineering_and_models.ipynb`.
   The notebooks were written in Google Colab, so update the Google Drive paths at the top to your own folder.

## What I would improve next

- Remove the leaked target columns and re-run all models
- Use a `Pipeline` with scaling and stratified cross-validation
- Report precision, recall, F1 and ROC-AUC, plus feature importance
- Use the cleaned listing text (TF-IDF) as extra features

## Author

**Omkar Gokhale** — Data Engineer & BI Analyst · [GitHub](https://github.com/Omkyao1998)
