# Predictive Pricing for IKEA Storage Furniture Using Machine Learning

This project leverages machine learning models to predict whether a piece of IKEA storage furniture falls into a **high** or **low** price category based on product features such as volume, color options, designer, and online availability. The goal was to develop models that not only classify price tiers with high accuracy, but also generate business insights for product design, inventory management, and pricing strategy.

---

## Objective

To accurately classify IKEA storage furniture into high or low price categories using supervised machine learning, while identifying which product attributes most influence price. The predictive model enables IKEA managers to:

- **Optimize pricing strategies** based on product features and perceived value
- **Improve inventory planning** by matching supply with local purchasing power
- **Design products more effectively** based on attributes associated with premium pricing

---

## Data Overview

- **Source**: Kaggle – IKEA Saudi Arabia Furniture Dataset (April 2020)  
  [Link to dataset](https://www.kaggle.com/datasets/ahmedkallam/ikea-sa-furniture-web-scraping)
- **Initial Rows**: 3,964
- **Final Dataset Used**: 773 rows (after cleaning and filtering for storage furniture)
- **Final Features**:
  - `Sellable_Online` (Yes/No)
  - `Other_Colors_Available` (Yes/No)
  - `Designer`
  - `Volume_Category` (Small, Medium, Large, Extra Large)
  - `Price_Category_High` (Target variable: 1 = high price, 0 = low price)

---

## Data Preprocessing

- **Filtered to storage furniture only** (e.g., bookcases, wardrobes, cabinets)
- **Dropped irrelevant features** (e.g., product links, descriptions, IDs)
- **Created new `Volume` feature** from width, height, and depth, then binned into 4 quartile-based categories
- **Transformed `Price` into binary target variable** using median split
- **One-hot encoded** categorical features (e.g., designer names)
- **Handled class imbalance** using SMOTE (Synthetic Minority Over-sampling Technique) where appropriate

---

## Models Implemented

We developed and iteratively refined the following models:

### Decision Tree Classifier

| Model Variant           | Train Acc | Test Acc | High Price Precision | High Price Recall | Notes |
|-------------------------|-----------|----------|------------------------|-------------------|-------|
| Benchmark (raw data)    | 80.88%    | 80.92%   | 86%                   | 74%               | No preprocessing |
| Cleaned & Filtered Data | 89.16%    | 85.16%   | 91%                   | 78%               | Major performance gain |
| + Feature Selection     | 83.82%    | 83.23%   | 93%                   | 71%               | Precision-focused |
| + SMOTE                 | 84.50%    | 81.94%   | 90%                   | 72%               | Balanced class recall |
| + Ensemble (Voting)     | 87.70%    | 83.23%   | 87%                   | 78%               | Balanced precision & recall |

### Random Forest Classifier

| Model Variant           | Train Acc | Test Acc | High Price Precision | High Price Recall | Notes |
|-------------------------|-----------|----------|------------------------|-------------------|-------|
| Baseline                | 80.58%    | 81.73%   | 83%                   | 79%               | Raw data |
| Cleaned Data            | 89.16%    | 83.23%   | 87%                   | 78%               | High performance |
| + SMOTE                 | 88.98%    | 84.50%   | 83%                   | 84%               | Best balanced model |
| + Hyperparameter Tuning| 88.99%    | 83.87%   | 88%                   | 78%               | Best precision model |

---

## Feature Importance (Random Forest)

Top features contributing to "High Price" classification:
1. **Volume Category (Extra Large)** – 31.76%
2. **Volume Category (Large)** – 15.00%
3. **Other Colors Available** – 9.15%
4. **Designer: Francis Cayouette** – 4.24%

This analysis reveals that **physical size, aesthetic options, and design pedigree** significantly drive premium pricing.

---

## Evaluation Metrics

All models were evaluated using:
- **Accuracy**
- **Precision and Recall (per class)**
- **F1-Score**
- **Stratified Accuracy** (used due to near-balanced binary target distribution)
- **Confusion Matrices** to inspect misclassifications

---

## Key Insights

- **Model Performance**: SMOTE-augmented Random Forest provided the most **balanced performance** with 84.5% accuracy, 84% precision, and 84% recall across classes.
- **Pricing Drivers**: Larger volumes, more color options, and certain designers significantly increase perceived value and therefore price.
- **Model Tuning**: Hyperparameter optimization improved precision for high-price classes but often traded off some recall.

---

## Business Implications

- **Strategic Design**: IKEA can invest in large, customizable storage products with popular designers to justify higher prices.
- **Localized Inventory**: Price classification helps align product mix with local consumer purchasing power and demand.
- **Marketing**: Highlight designers like Francis Cayouette and color variety in campaigns to enhance value perception.
- **Forecasting**: Accurate price category classification supports better margin and revenue projections.

---

## Next Steps and Improvements

- Expand dataset to include additional variables such as material, brand collaborations, or region-specific pricing.
- Compare model results with real-world IKEA pricing and margin data for validation.
- Apply similar methodology to other product categories (e.g., Bedroom or Living Room furniture) for scalable pricing insights.

---

## Author

**Sorasak Joshi**  
Master's in Business Analytics, University of California, Irvine  
sorasakj@uci.edu  
[LinkedIn Profile](https://www.linkedin.com/in/sorasakjoshi)

---

> This project was completed as part of BANA 273: Machine Learning Analytics under Professor Mingdi Xin. It demonstrates the value of domain-specific data preprocessing and feature engineering in real-world pricing strategy applications.
