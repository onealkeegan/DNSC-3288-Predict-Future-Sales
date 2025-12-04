# Predicting Future Sales for DNSC 3288 Solo Final Project

### Basic Information

* **Person or organization developing model**: O'Neal Keegan, `onealkeegan@gwu.edu`
* **Model date**: December, 2025
* **Model version**: 9.0
* **License**: MIT
* **Model implementation code**: [DNSC-3288-Predict-Future-Sales.ipynb]
* (https://github.com/onealkeegan/DNSC-3288-Predict-Future-Sales/blob/main/DNSC_3288_Predict_Future_Sales.ipynb) 

### Intended Use
* **Primary intended uses**: This model's intended use is to predict next-month item sales for a retail planning Kaggle competition, allow students to practice times-series forcasting 
* **Primary intended users**: Students in GWU DNSC 3288 class, future "Predict Future Sales" competitors
* **Out-of-scope use cases**: Predictions for markets outside the original Kaggle dataset ex. groceries

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | an Id that represents a (Shop, Item) tuple within the test set |
| **shop_id** | input | ID | unique identifier of a shop |
| **item_id** | input | ID | unique identifier of a product |
| **item_category_id** | ID | interval | unique identifier of item category |
| **item_cnt_day** | target | ratio | number of products sold |
| **item_price** | input | ratio | current price of an item|
| **date** | input | interval |  date in format dd/mm/yyyy |
| **date_block_num** | input | ratio |  a consecutive month number, used for convenience. January 2013 is 0, February 2013 is 1,..., October 2015 is 33 |
| **item_name** | input | nominal | name of item|
| **shop_name** | input | nominal | name of shop |
| **item_category_name**| intput | nominal | name of item category |

* **Source of training data**: sales_train.csv, items.csv, shops.csv, sample_submission.csv, item_categories.csv from *Predict Future Sales* competition
* **How training data was divided into training and validation data**: all training besides month 33 for validation and month 34 for testing
* **Number of rows in training and validation data**:
  * Training rows: 
  * Validation rows:

### Test Data
* **Source of test data**: test.csv from *Predict Future Sales* competition
* **Number of rows in test data**: 214k
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
* **Describe potential negative impacts of using your model:**: 
* **Describe potential uncertainties relating to the impacts of using your model:**: 
* **Describe any unexpected or results**:


