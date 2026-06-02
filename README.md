# Marketing-Mix-Modelling---Data-Science-Project
# Marketing Mix Modeling (MMM): Measuring Advertising Impact with Adstock, Saturation & Ridge Regression to predict future sales performance.

## Overview

This project implements a Marketing Mix Modeling (MMM) framework to quantify the impact of multiple advertising channels on sales performance. The model captures real-world marketing dynamics such as advertising carryover effects (Adstock), diminishing returns (Saturation), seasonality, promotional activities, and competitor influence.

The objective is to answer key business questions:

* Which marketing channels drive the most sales?
* How much does each channel contribute to revenue growth?
* At what point do marketing investments experience diminishing returns?
* How accurately can future sales be predicted using marketing spend data?

## Project Objective

The primary objective of this project was to build an interpretable Marketing Mix Modeling (MMM) framework capable of accurately predicting weekly sales while quantifying the impact of different marketing channels.

Specific goals included:

* Achieve a sales forecasting error below **4% MAPE**.
* Model advertising carryover effects using **Adstock** transformations.
* Capture **diminishing returns** through saturation curves.
* Measure the influence of individual marketing channels on sales performance.
* Compare multiple machine learning algorithms and select the most suitable model for MMM.
* Generate response curves to support marketing budget allocation decisions.

Using a combination of domain-specific feature engineering and machine learning, the final Ridge Regression model achieved:

* **R² Score:** 94.04%
* **MAPE:** 3.86%
* **RMSE:** 101,889
* **Average Weekly Sales:** 2.34 Million

The project demonstrates how marketing analytics can be combined with machine learning to support data-driven budget allocation and campaign planning decisions.
---
## Business Problem

Organizations invest heavily across multiple advertising channels such as Google Ads, Instagram, TV, YouTube, Influencer Marketing, OTT Platforms, and Print Media. However, understanding the true impact of each channel is challenging because:

* Advertising effects persist over time.
* Marketing channels often influence each other.
* Returns diminish as spending increases.
* External factors such as competitors affect sales performance.
* Seasonal demand patterns create additional complexity.

Marketing Mix Modeling addresses these challenges by estimating the relationship between marketing investments and business outcomes while accounting for carryover effects, saturation, seasonality, and competitive pressure.
Throgh Marketing Mix Modeling we can experiment where the next ruppee must be invested and its impact on sales before actually investing
---

## Dataset

The dataset contains weekly observations from January 2022 to December 2025.

### Target Variable

* Sales

### Marketing Channels

* Instagram Ads
* Google Ads
* TV Advertising
* YouTube Advertising
* Newspaper Advertising
* Influencer Marketing
* OTT Advertising

### Additional Features

* Competitor Spend
* Sales Promotion Campaigns
* Holiday Indicators
* Seasonal Features (Week Sin/Cos)

---

## Data Preparation

### Missing Value Handling

* Rows with missing sales values were removed.
* Missing marketing spend values were replaced with 0, representing periods when campaigns were inactive.
* Missing competitor spend values were imputed using mean imputation.

### Seasonality Engineering

To capture yearly seasonal patterns, raw date information was transformed into cyclical features:

* Week Sin
* Week Cos

This preserves the periodic nature of calendar data while avoiding artificial discontinuities.

---

## Marketing Mix Transformations

### 1. Adstock Transformation

Advertising rarely impacts customers immediately and then disappears. Marketing effects often carry forward into future periods.

An Adstock transformation with a decay factor of 0.5 was applied to all marketing channels to capture this carryover effect.

### 2. Saturation Transformation

Marketing effectiveness typically follows diminishing returns. Doubling spend does not necessarily double sales.

To model this behavior, a nonlinear saturation transformation was applied:

```python
np.log1p(adstock_value) ** 4
```

This transformation allows the model to capture realistic marketing response patterns where incremental gains decrease as spend increases.

---

## Modeling Pipeline

### Feature Encoding

* One-Hot Encoding for sales promotion categories.

### Feature Scaling

* StandardScaler applied to numerical features.

### Train-Test Split

A chronological split was used to preserve the time-series structure:

* Training Set: First 80%
* Test Set: Last 20%

No random shuffling was performed.

---
## Models Evaluated

| Model                      |   R² Score |      MAPE |
| -------------------------- | ---------: | --------: |
| Ridge Regression           | **94.04%** | **3.86%** |
| Multiple Linear Regression |     93.46% |     3.91% |
| XGBoost                    |     86.21% |     5.36% |
| SVR                        |     67.00% |     8.88% |
| Random Forest              |     59.76% |    10.44% |

### Why Ridge Regression?

Ridge Regression delivered the strongest overall performance while maintaining interpretability, which is critical for Marketing Mix Modeling.

Benefits include:

* Handles multicollinearity between channels.
* Produces stable coefficient estimates.
* Maintains explainability for business stakeholders.
* Achieved the highest predictive accuracy among all tested models.
Among all evaluated models, Ridge Regression provided the best combination of predictive performance, stability, and business interpretability.

---

## Key Findings

### Google Ads Emerged as the Strongest Channel

Response curve analysis indicates that Google Ads generated the highest modeled sales impact, making it the most influential channel in the marketing mix.

### Instagram Ads Closely Followed

Instagram demonstrated strong incremental sales contribution and showed a response pattern similar to Google Ads.

### Diminishing Returns Were Clearly Observed

Response curves revealed that additional marketing spend produces progressively smaller gains at higher investment levels, highlighting the importance of budget optimization.

### Competitor Activity Negatively Influenced Sales

The model identified a negative relationship between competitor advertising spend and sales performance, indicating competitive pressure within the market.

---

## Response Curve Analysis

Response curves were generated for major advertising channels to visualize the relationship between marketing investment and incremental sales.

These curves help answer questions such as:

* How much additional revenue is generated by increasing spend?
* Which channels saturate more quickly?
* Where should incremental budget be allocated?

The analysis showed that Google Ads and Instagram Ads offer the strongest sales response before reaching saturation.

---

## Technologies Used

* Python
* NumPy
* Pandas
* Matplotlib
* Scikit-Learn
* Google Colab

---
## Future Improvements
* Budget optimization framework
* Bayesian Marketing Mix Modeling
* Confidence intervals for channel contributions
* Interactive dashboard for scenario analysis
<img width="1580" height="2790" alt="image" src="https://github.com/user-attachments/assets/86d4177b-b1e5-4b1d-9b7b-169b9bff2716" />
<img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/ff980b14-fec5-42d7-8e9f-2f9927317f1c" />
<img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/f2f1181b-5249-4aa8-816b-b4fd18f1c74b" />


---

## Author

Nafees Sayyed

Data Science/ML Enthusiast focused on applying machine learning techniques to solve real-world business problems through interpretable and data-driven solutions.
