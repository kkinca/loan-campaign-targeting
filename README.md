# loan-campaign-targeting

A decision tree modeling project designed to identify which bank customers are most likely to accept a personal loan offer.

## Project Overview

This project focuses on improving marketing campaign performance for a bank by predicting which liability customers are most likely to convert to personal loan borrowers.

The goal is to move beyond broad, low-efficiency outreach and instead build a targeted campaign strategy based on interpretable machine learning. The project combines exploratory data analysis, decision tree modeling, pruning, and business recommendations to support more precise customer targeting.

## Business Problem

AllLife Bank wants to increase personal loan conversion among existing customers while preserving strong deposit relationships.

The business objectives were to:
- predict which customers are likely to accept a personal loan
- understand the key drivers of conversion
- identify the most promising customer segments for future campaigns
- improve conversion above the baseline rate of 9.6%

A strong solution needed to be both accurate and interpretable so the marketing team could use it in real campaign decisions.

## Dataset

The dataset contains information on **5,000 bank customers**, including:
- demographic features
- financial characteristics
- account relationships
- digital usage behavior
- prior response to a personal loan offer

### Target Variable
- `Personal_Loan`
  - `1` = accepted
  - `0` = rejected

### Key Predictors
- Age
- Experience
- Family
- Education
- Income
- CCAvg
- Mortgage
- Securities Account
- CD Account
- Online Banking
- Credit Card

The baseline personal loan acceptance rate in the dataset was **9.6%**.

## Exploratory Data Analysis

EDA showed several important business patterns:

- loan acceptance is relatively rare, making this a class-imbalanced problem
- higher-income customers were much more likely to accept the loan
- heavier credit-card spenders also converted at much higher rates
- CD Account ownership was the strongest categorical predictor
- education level showed moderate lift
- online banking usage offered only limited additional signal

### Key EDA Insights
- Customers earning over 100K showed much higher loan adoption
- Higher monthly card spend was strongly associated with conversion
- Customers with a CD Account converted at about 46%, versus about 7% for non-CD customers
- Income and CCAvg emerged as the strongest numeric predictors

## Data Preprocessing

The preprocessing workflow included:
- removal of non-predictive fields such as ID
- duplicate value checks
- confirmation of zero missing values
- documentation of outliers without removal
- stratified 70/30 train-test split
- categorical encoding where needed

Because the model used decision trees, no feature scaling was required.

## Modeling Approach

The project used **decision tree classification** to predict loan acceptance.

Three model stages were compared:
1. **Baseline Decision Tree**
2. **Pre-Pruned Decision Tree**
3. **Post-Pruned Decision Tree (Final Model)**

The objective was not only to improve performance, but also to simplify the model so the strongest signals remained interpretable and actionable.

## Baseline Model

The baseline full-depth tree performed well on training data but showed signs of overfitting.

### Baseline Performance
- **Train Accuracy:** 99%
- **Test Accuracy:** 88%
- **Precision:** 0.81
- **Recall:** 0.78
- **F1 Score:** 0.79

The baseline model relied on too many minor variables, including features that did not generalize well.

## Model Improvement Through Pruning

To improve generalization and interpretability, both pre-pruning and post-pruning were applied.

### Pre-Pruning
- `max_depth = 5`
- `min_samples_leaf = 25`
- `min_samples_split = 30`

### Post-Pruning
- `max_depth = 7`
- `min_samples_leaf = 20`
- `min_samples_split = 25`
- `ccp_alpha = 0.015`

Pruning simplified the model and removed weaker, unstable predictors.

## Final Model Performance

The **post-pruned decision tree** was selected as the final model.

### Final Test Results
- **Accuracy:** 0.90
- **Precision:** 0.84
- **Recall:** 0.81
- **F1 Score:** 0.82
- **AUC:** 0.93

This final model delivered stronger generalization while remaining easy to explain and operationalize.

## Top Drivers of Loan Adoption

The strongest final predictors were:
1. Income
2. CCAvg
3. CD_Account
4. Education
5. Online Banking

A key project insight was that pruning removed spurious features and sharpened the model’s focus on financially logical drivers of conversion.

## Final Model Rules

Examples of interpretable targeting rules from the final model:

1. If **Income >= 115K** and **CCAvg >= 2.5**, the customer is likely to accept the loan.
2. If **CD_Account = 1**, the customer has a high probability of conversion.
3. If **Income < 60K** and **CCAvg < 1**, the customer is unlikely to convert.
4. Graduate and advanced education levels provide additional lift over undergraduate customers.

These rules make the model highly actionable for campaign planning.

## Business Recommendations

### Primary Target Segment
- Income > 100K
- CCAvg > 2K/month
- CD_Account = 1
- Online Banking = 1

### Secondary Target Segment
- Graduate or advanced education
- Mid-income customers (60K-100K)
- CCAvg between 1K and 2K/month

### Low-Priority Segment
- Income < 50K
- CCAvg < 1K/month

### Suggested Targeting Channels
- personalized email and app notifications for online users
- relationship manager outreach for high-value CD customers
- bundled offers such as CD renewal plus loan incentives

## Business Impact

This project shows how interpretable machine learning can improve campaign efficiency and customer targeting.

Potential business value includes:
- more efficient allocation of marketing spend
- higher conversion versus broad outreach
- better identification of high-propensity customer segments
- clearer decision rules for campaign execution
- easier communication between analytics and marketing teams

The analysis suggested that targeting the top-propensity decile could potentially lift conversion to approximately 20% to 25%, versus the baseline rate of 9.6%.

## Risk and Governance Considerations

The project also identified practical guardrails for responsible deployment:
- avoid ZIP-level targeting to reduce geographic bias
- monitor data drift regularly
- keep targeting rules simple enough for marketing execution
- review the model periodically for performance and compliance

## Tools and Techniques

- Python
- Decision Trees
- Classification Modeling
- Exploratory Data Analysis (EDA)
- Model Pruning
- Feature Importance Analysis
- Campaign Targeting Strategy
- Business Analytics
- Jupyter Notebooks

## Repository Contents

Suggested files for this repo:
- `README.md`
- `loan_campaign_targeting_notebook.ipynb`
- `Loan_Campaign_Targeting_Presentation.pdf`

## Key Takeaway

This project demonstrates how interpretable machine learning can bridge analytics and business action. By combining decision trees with clear segmentation rules, the model supports smarter campaign targeting, stronger conversion potential, and more practical decision-making for marketing teams.
