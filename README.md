# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 

### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```
Developed by: Sai Eswar Kandukuri
Reg No: 212221240020
```
#### Import the packages
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.ar_model import AutoReg
from sklearn.metrics import mean_squared_error
```
#### Read the Airline Passengers dataset from a CSV file
```
data = pd.read_csv("/content/airline.csv")
```
#### Display the shape and the first 50 rows of the dataset
```
print("Shape of the dataset:", data.shape)
print("First 50 rows of the dataset:")
print(data.head(50))
```
#### Plot the first 50 values of the 'International' column
```
plt.plot(data['International '].head(50))
plt.title('First 50 values of the "International" column')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.show()
```
#### Perform rolling average transformation with a window size of 5
```
rolling_mean_5 = data['International '].rolling(window=5).mean()
```
#### Display the first 10 values of the rolling mean
```
print("First 10 values of the rolling mean with window size 5:")
print(rolling_mean_5.head(10))
```
#### Perform rolling average transformation with a window size of 10
```
rolling_mean_10 = data['International '].rolling(window=10).mean()
```
#### Plot the original data and fitted value (rolling mean with window size 10)
```
plt.plot(data['International '], label='Original Data')
plt.plot(rolling_mean_10, label='Rolling Mean (window=10)')
plt.title('Original Data and Fitted Value (Rolling Mean)')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.legend()
plt.show()
```
#### Fit an AutoRegressive (AR) model with 13 lags
```
lag_order = 13
model = AutoReg(data['International '], lags=lag_order)
model_fit = model.fit()
```
#### Plot Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF)
```
plot_acf(data['International '])
plt.title('Autocorrelation Function (ACF)')
plt.show()

plot_pacf(data['International '])
plt.title('Partial Autocorrelation Function (PACF)')
plt.show()
```
#### Make predictions using the AR model
```
predictions = model_fit.predict(start=lag_order, end=len(data)-1)
```
#### Compare the predictions with the original data
```
mse = mean_squared_error(data['International '][lag_order:], predictions)
print('Mean Squared Error (MSE):', mse)
```
#### Plot the original data and predictions
```
plt.plot(data['International '][lag_order:], label='Original Data')
plt.plot(predictions, label='Predictions')
plt.title('AR Model Predictions vs Original Data')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.legend()
plt.show()
```

### OUTPUT:

# Plot the original data and fitted value
![image](https://github.com/Vivekreddy8360/TSA_EXP8/assets/94525701/5f971aea-be3c-425c-bcb9-95cd27cb2888)

# Plot Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF)
![image](https://github.com/Vivekreddy8360/TSA_EXP8/assets/94525701/ee9aff85-0bac-47df-a947-9e0c6c4846ad)

![image](https://github.com/Vivekreddy8360/TSA_EXP8/assets/94525701/2a57d8fd-e564-4bf4-a92b-c4bd759151be)

# Plot the original data and predictions
![image](https://github.com/Vivekreddy8360/TSA_EXP8/assets/94525701/b29540db-745b-47d9-a151-9de1f739b656)
### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
