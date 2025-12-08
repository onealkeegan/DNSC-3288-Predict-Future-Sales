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
* **Primary intended users**: (1) Students in GWU DNSC 3288 class (2) future "Predict Future Sales" competitors
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
['shop_id',
 'item_id',
 'date_block_num',
 'first_sale_day',
 'month',
 'year',
 'day_quality',
 'category_id',
 'item_name_first4',
 'item_name_first6',
 'item_name_first11',
 'group_id',
 'shop_cluster',
 'shop_type',
 'shop_city',
 'prev_days_on_sale',
 'item_age',
 'item_name_first4_age',
 'item_name_first6_age',
 'item_name_first11_age',
 'category_age',
 'group_age',
 'shop_age',
 'item_age_if_shop_sale',
 'item_age_without_shop_sale',
 'item_cnt_all_shops',
 'item_cnt_all_shops_median',
 'category_cnt',
 'category_cnt_median',
 'category_cnt_all_shops',
 'category_cnt_all_shops_median',
 'group_cnt',
 'group_cnt_all_shops',
 'shop_cnt',
 'city_cnt',
 'new_items_in_cat',
 'new_items_in_cat_all_shops',
 'item_cnt_lag1',
 'item_cnt_lag2',
 'item_cnt_lag3',
 'item_cnt_lag6',
 'item_cnt_lag12',
 'item_cnt_all_shops_lag1',
 'item_cnt_all_shops_lag2',
 'item_cnt_all_shops_lag3',
 'item_cnt_all_shops_lag6',
 'item_cnt_all_shops_lag12',
 'category_cnt_lag1',
 'category_cnt_lag2',
 'category_cnt_lag3',
 'category_cnt_lag6',
 'category_cnt_lag12',
 'category_cnt_all_shops_lag1',
 'category_cnt_all_shops_lag2',
 'category_cnt_all_shops_lag3',
 'category_cnt_all_shops_lag6',
 'category_cnt_all_shops_lag12',
 'group_cnt_lag1',
 'group_cnt_lag2',
 'group_cnt_lag3',
 'group_cnt_lag6',
 'group_cnt_lag12',
 'group_cnt_all_shops_lag1',
 'group_cnt_all_shops_lag2',
 'group_cnt_all_shops_lag3',
 'group_cnt_all_shops_lag6',
 'group_cnt_all_shops_lag12',
 'shop_cnt_lag1',
 'shop_cnt_lag2',
 'shop_cnt_lag3',
 'shop_cnt_lag6',
 'shop_cnt_lag12',
 'city_cnt_lag1',
 'city_cnt_lag2',
 'city_cnt_lag3',
 'city_cnt_lag6',
 'city_cnt_lag12',
 'new_items_in_cat_lag1',
 'new_items_in_cat_lag2',
 'new_items_in_cat_lag3',
 'new_items_in_cat_lag6',
 'new_items_in_cat_lag12',
 'new_items_in_cat_all_shops_lag1',
 'new_items_in_cat_all_shops_lag2',
 'new_items_in_cat_all_shops_lag3',
 'new_items_in_cat_all_shops_lag6',
 'new_items_in_cat_all_shops_lag12',
 'item_rm3',
 'item_rm6',
 'item_rm12',
 'category_rm3',
 'category_rm6',
 'category_rm12',
 'shop_rm3',
 'shop_rm6',
 'shop_rm12',
 'item_cnt_diff',
 'item_cnt_all_shops_diff',
 'category_cnt_diff',
 'category_cnt_all_shops_diff',
 'category_price_lag1',
 'block_price_lag1',
 'item_price_lag1',
 'item_price_lag2',
 'price_delta',
 'price_ratio',
 'item_cnt_sum_alltime',
 'item_cnt_sum_alltime_allshops',
 'relative_price_item_block_lag1',
 'item_cnt_per_day_alltime',
 'item_cnt_per_day_alltime_allshops',
 'same_name4catage_cnt_all_shops',
 'same_name4catage_cnt',
 'same_name6catage_cnt_all_shops',
 'same_name6catage_cnt',
 'same_name11catage_cnt_all_shops',
 'same_name11catage_cnt',
 'below_item_cnt_all_shops_lag1',
 'above_item_cnt_all_shops_lag1',
 'below_item_cnt_all_shops_lag2',
 'above_item_cnt_all_shops_lag2']
* **Column(s) used as target(s) in the final model**: "item_cnt"
* **Type of model**: LightGBM Regression
* **Software used to implement the model**: Python, LightGBM, NumPy, Pandas, Plotly, SHAP
* **Version of the modeling software**: lightgbm==4.6.0
* **Hyperparameters or other settings of your model**: 
```
params = {
    'objective': 'regression',
    'metric': 'rmse',
    'num_leaves': 120,
    'min_data_in_leaf': 50,
    'max_depth': 10,
    'feature_fraction': 0.8,
    'bagging_fraction': 0.8,
    'bagging_freq': 1,
    'learning_rate': 0.03,
    'seed': 42,
    'verbosity': -1
}
```
### Quantitative Analysis

* Model was assessed primarily with RMSE because RMSE uses the same units as the target variable, making it easier to understand the magnitude of the error.
* RMSE is also the evaluation metric for the competition.

| Train RMSE | Validation RMSE |
| ------ | ------- |
| 0.5639 | 0.5222  |

Table 1. RMSE Per Month

| Month | Training RMSE |
|-------|----------------|
| 2  | 0.630577 |
| 3  | 0.562119 |
| 4  | 0.533294 |
| 5  | 0.576405 |
| 6  | 0.554529 |
| 7  | 0.592284 |
| 8  | 0.575049 |
| 9  | 0.560159 |
| 10 | 0.563038 |
| 11 | 0.684111 |
| 12 | 0.588343 |
| 13 | 0.587203 |
| 14 | 0.569536 |
| 15 | 0.515059 |
| 16 | 0.527807 |
| 17 | 0.529246 |
| 18 | 0.523801 |
| 19 | 0.559758 |
| 20 | 0.526745 |
| 21 | 0.539508 |
| 22 | 0.558932 |
| 23 | 0.704694 |
| 24 | 0.597537 |
| 25 | 0.543416 |
| 26 | 0.529460 |
| 27 | 0.500136 |
| 28 | 0.501292 |
| 29 | 0.514481 |
| 30 | 0.506873 |
| 31 | 0.537613 |
| 32 | 0.540547 |


### Ethical Consideration
* **Describe potential negative impacts of using your model:**: Inaccurate predictions could lead to overstocking and supply chain inefficiences. Our model does not account for macroenvironment changes, so it may not be flexible to rapidly changing environments, and instead reinforce past demand biases rather than adapting to changes like a pandemic. 
* **Describe potential uncertainties relating to the impacts of using your model:**: The lack of real time  promotion data could cause the model's predictions to fail quickly outside of the training environment since promotions & deals have a large impact on inventory and sales. 
* **Describe any unexpected or results:**: The model occasionally produces extreme predictions on low-volume or newly introduced products, potentially causing misleading planning decisions. Clipping was applied to bound these predictions, but this may not show an accurate relationship in the real world. 
