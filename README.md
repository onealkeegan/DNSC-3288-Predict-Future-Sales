# Predicting Future Sales for DNSC 3288 Solo Final Project

### Basic Information

* **Person or organization developing model**: O'Neal Keegan, `onealkeegan@gwu.edu`
* **Model date**: December, 2025
* **Model version**: 9.0
* **License**: MIT
* **Model implementation code**: [DNSC-3288-Predict-Future-Sales.ipynb]
* (https://www.kaggle.com/code/onealkeegan/dnsc3288-predict-future-sales)

### Intended Use
* **Primary intended uses**: (1) This model's intended use is to predict next-month item sales for a retail planning Kaggle competition (2) Allow students to practice times-series forcasting 
* **Primary intended users**: Students in GWU DNSC 3288 class, future "Predict Future Sales" competitors
* **Out-of-scope use cases**: Predictions for markets outside the original Kaggle dataset ex. groceries

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | an ID that represents a (Shop, Item) tuple within the test set |
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
  * Training rows: 7,869,484
  * Validation rows: 221,760

### Test Data
* **Source of test data**: test.csv from *Predict Future Sales* competition
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

| Train RMSE | Validation RMSE |
| ------ | ------- |
| 0.6035 | 0.5517  |

Table 1. RMSE Per Month

| Month | Training RMSE |
|-------|-----|
| 2  | 0.667765 |
| 3  | 0.603433 |
| 4  | 0.566605 |
| 5  | 0.609390 |
| 6  | 0.583677 |
| 7  | 0.628294 |
| 8  | 0.615719 |
| 9  | 0.597084 |
| 10 | 0.607769 |
| 11 | 0.738983 |
| 12 | 0.628255 |
| 13 | 0.632644 |
| 14 | 0.609606 |
| 15 | 0.552822 |
| 16 | 0.559833 |
| 17 | 0.560788 |
| 18 | 0.555500 |
| 19 | 0.600944 |
| 20 | 0.572158 |
| 21 | 0.579527 |
| 22 | 0.600553 |
| 23 | 0.765158 |
| 24 | 0.638652 |
| 25 | 0.581953 |
| 26 | 0.571159 |
| 27 | 0.539051 |
| 28 | 0.537635 |
| 29 | 0.548998 |
| 30 | 0.536134 |
| 31 | 0.573818 |
| 32 | 0.587106 |


### Ethical Consideration
* **Describe potential negative impacts of using your model:**: Inaccurate predictions could lead to overstocking and supply chain inefficiences. Our model does not account for seasonality changes or macroenvironment changes, so it may not be flexible to rapidly changing environments, and instead reinforce past demand biases rather than adapting to changes like a pandemic or holiday season. 
* **Describe potential uncertainties relating to the impacts of using your model:**: The lack of real time  promotion data could cause the model's predictions to degrade quickly outside of the training environment since promotions & deals have a large impact on inventory and sales. 
* **Describe any unexpected or results:**: The model occasionally produces extreme predictions on low-volume or newly introduced products, potentially causing misleading planning decisions. Clipping was applied to bound these predictions, but this may not show an accurate relationship in the real world. 
