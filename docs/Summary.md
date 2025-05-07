# Smart Factory Sensor Data Summary
---

## ETL Process

Using vscode plugins to get a general feel of the data. The data consists of weather conditions of multiple zones where presumably the sensors are fitted. The dataset also has outdoor conditions which may serve as a constant for all the zones.

### Loading Process

Used `pandas.read_csv()` to load the data into a `pandas.Dataframe`. After loading the data missing data checks were made. All the columns had missing data. Since there were no categorical data no encoding was done.

There were mainly 2 types of data.
- DateTime
- Float

Used forward filling to fill for missing timestamps and mean data to fill for the rest of the measurements.

During verification checks for any missing cells that may have overlooked, it was discovered that the following were still the same

|**Column** | **Missing cells** |
|---|---|
|equipment_energy_consumption | 844 |
|lighting_energy             |  809 |
|zone1_temperature         |    867 |
|zone1_humidity          |      801 |
|zone2_temperature     |        853 |

Used the same vscode plugin to further inspect the dataset. There were many string data describing missing data present. Examples

- "?????"
- "err"
- "na"

Created a column converter function to make those specific columns strictly numerical.

### Feature Engineering

Created a few features to further granulize the data to make it easier to find trends within the data

### Data Description

Used the `Dataframe.info()` and `Dataframe.describe()` to check the metadata of the columns. Discovered that there are negative values for energy consumption and humidity features which are not possible. Assuming the readings are correct, proceeded with absolute values of the features.

## EDA

Used visual graphs to visualize the datasets and discovered that there was heavy utilization of energy during midday 2/16 to midday 5/16. Feature correlation indicated that the energy consumtion was highly dependent on hour of day and inversly dependent on zone8 humidity

## Models

Used the following regression models

- Linear Regressor
- K nearest neighbout
- Decision Tree Regressor
- Random Forest Regressor

Created model pipleines to handle the data and used `SelectKBest` for feature selection. Found 15 to be the most optimized `k` value.

### Evaluation

Found Random forest to be the best model among all

|Model|RMSE |R² |
| --- | --- | --- |
|      RandomForest|  162.769622|  0.073747|
|      DecisionTree|  165.966089|  0.037010 |
|  LinearRegression|  167.876149|  0.014717 |
|               KNN|  171.314964| -0.026062 |


