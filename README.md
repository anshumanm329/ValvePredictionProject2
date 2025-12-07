# ValvePredictionProject2
Predicting percentage of valve opening, depending upon the liquid level and feedback
# Valve Position Prediction Project
This project is aimed at using the behaviour of a `PID regulator` based control system obtained from `Matlab`
to predict the opening level of the actuating mechanism (i.e. the valve) through various regressors such as `RandomForestRegressor` and `CatBoostRegressor`.
## 1. Problem definition
> How well can a valve's position be predicted using the data obtained from a Matlab simulation of a PID based control system
* ## 2. Data preparation
* In this part, we are going to import `training_data_from_matlab6.csv`.
* Check out what kind of format, the `Time` data is in and convert it into either int64 or `datetime(format = "seconds")`
* After that, we are to check for any other `string` type data using `pd.api.dtypes.is_string_dtype()` function. And convert all string type data to numeric, using`pd.to_numeric(downcast='float')`
* After converting all of the content of the dataframe except for *DateTime* we will check for missing data using `pd.isnull()`
* If found, then the missing data is to be replaced by zero.
* Once missing data is filled, we will be checking for values more than 100 in `Valve_positions` and values more than 1000 in `Liquid_levels`.
* This is errroneous data and it is to be replaced by the median values of the above mentioned labels.
* We will make a copy of the preprocessecd dataframe and label it as `df_for_modelling`
* In `df_for_modelling`, we will extract the year, month, date, hour, minute and seconds data from the DateTime column and then drop the datetime column as it can't be used for training a Regressor model.
* We are ready for modelling!
### 2.1. How to format the data
* We need to check what kind of format, the data under label `Time` are in and then convert them into either datetime.seconds or int64 format
* Convert `string` datatypes to float using `pd.to_numeric(downcast = 'float')`
* Eliminate any missing data by first generating `is_missing` boolean data for each column of the input data
* Then eliminate by checking through `isna().sum()` and `_is_missing.value_counts()` and then eliminating the missing values by replacing them with `medians`
* Eliminate erronious data. I.e. liquid levels above `1.0` in `input` and `liquid_level` columns and valve opening levels above `100` in `valve_positions` by replacing them with medians.
## 3. Modelling
* Use `train_test_split()` from `sklearn` to divide the dataset into training and validation datasets.
* Use `RandomForestRegressor` to train the model using the training dataset.
* Use `CatBoostRegressor` to train the model using the training dataset.
* Use `RandomizedSearchCV` to get the optimize the model using the best hyperparameters `RandomForestRegressor`
* Use `catboostcv` to obtain best hyperparameters for `CatBoostRegressor`
* Evaluate the optimized model on the validation datasets.
* Use test datasets to check the predictions of the model against true labels.

