# Predicting Future Sales for DNSC 3288 Solo Final Project

### Basic Information

* **Person or organization developing model**: O'Neal Keegan, `onealkeegan@gwu.edu`
* **Model date**: December, 2025
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [DNSC-3288-Predict-Future-Sales.ipynb]
* (https://github.com/onealkeegan/DNSC-3288-Predict-Future-Sales/blob/main/DNSC_3288_Predict_Future_Sales.ipynb) 

### Intended Use
* **Primary intended uses**: This model's intended use is to predict next-month item sales for a retail planning Kaggle competition, allow student's to practice times-series forcasting 
* **Primary intended users**: Students in GWU DNSC 3288 class, future "Predict Future Sales" competitors
* **Out-of-scope use cases**: Predictions for markets outside the original Kaggle dataset ex. groceries

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: *Predict Future Sales* competition
* **How training data was divided into training and validation data**: all training besides month 33 for validation and month 34 for testing
* **Number of rows in training and validation data**:
  * Training rows: ~2.9M
  * Validation rows: ~214K

### Test Data
* **Source of test data**: sales_train.csv, items.csv, shops.csv, categories.csv from *Predict Future Sales* competition
* **Number of rows in test data**: 214,200
* **State any differences in columns between training and test data**: Test does not contain item_cnt (the target variable)

### Model details
* **Columns used as inputs in the final model**:
* Lag features (item_cnt_lag1to12, category_cnt_lag1to12, group_cnt_lag1to12)
* Price aggregates
* Count aggregates
* Age features
* Categorical identifiers (item_id, shop_id, category_id)
* Month, shop city, item groups
* **Column(s) used as target(s) in the final model**: "item_cnt"
* **Type of model**: LightGBM Regression
* **Software used to implement the model**: Python, LightGBM, NumPy, Pandas, Plotly, SHAP
* **Version of the modeling software**: lightgbm==4.6.0
* **Hyperparameters or other settings of your model**: 
```
params = {
    'objective': 'regression',
    'metric': 'rmse',
    'num_leaves': 30,
    'min_data_in_leaf':10,
    'feature_fraction':0.7,
    'learning_rate': 0.01,
    'num_rounds': 300,
    "early_stopping_round":30,
    'seed': 1,
    'verbosity':-1
}
```
### Quantitative Analysis

* Model was assessed primarily with RMSE

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.3456 | 0.7891  | 0.7687* |

Table 1. AUC values across data partitions. 

| Group | Validation AIR |
|-------|-----|
| Black vs. White | 0.8345 |
| Hispanic vs. White | 0.8765 |
| Asian vs. White | 1.098 |
| Female vs. Male | 1.245 |

### Ethical Consideration
* **Describe potential negative impacts of using your model:**: sales_train.csv, items.csv, shops.csv, categories.csv from *Predict Future Sales* competition
* **Describe potential uncertainties relating to the impacts of using your model:**: 214,200
* **Describe any unexpected or results**: Test does not contain item_cnt (the target variable)


