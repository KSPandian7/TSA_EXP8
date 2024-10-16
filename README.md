### DEVELOPED BY : KULASEAKARAPANDIAN K
### REGISTER NO : 212222240052
### Date:

# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING

### AIM:
To implement a Moving Average Model and Exponential Smoothing using Python for time series analysis of electricity consumption data.

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
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the Ethereum dataset from a CSV file
file_path = 'path/to/your/ethereum_data.csv'  # Replace with the correct file path
data = pd.read_csv(file_path)

# Convert 'dateTime' to datetime and set it as the index
data['dateTime'] = pd.to_datetime(data['dateTime'])
data.set_index('dateTime', inplace=True)

# Focus on the 'close' prices
close_data = data['close']

# Display the shape and the first 20 rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Plot Transform Dataset (Original Close Prices)
plt.figure(figsize=(12, 6))
plt.plot(close_data, label='Original Close Prices', color='blue')
plt.title('Transform Dataset (Original Close Prices)')
plt.xlabel('DateTime')
plt.ylabel('Close Price')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 5
rolling_mean_5 = close_data.rolling(window=5).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(close_data, label='Original Close Prices', color='blue')
plt.plot(rolling_mean_5, label='Moving Average (window=5)', color='orange')
plt.title('Moving Average of Close Prices')
plt.xlabel('DateTime')
plt.ylabel('Close Price')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(close_data, trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 5 periods (adjust as needed)
future_steps = 5
predictions = model_fit.predict(start=len(close_data), end=len(close_data) + future_steps - 1)

# Create a future index for the predicted dates
future_dates = pd.date_range(start=close_data.index[-1] + pd.Timedelta(minutes=5), periods=future_steps, freq='5T')

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(close_data, label='Original Close Prices', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Close Prices')
plt.xlabel('DateTime')
plt.ylabel('Close Price')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```
### OUTPUT:

#### Moving Average
![image](https://github.com/user-attachments/assets/acc2c577-40e3-4892-90f4-c29d65b4c619)

#### Plot Transform Dataset
![image](https://github.com/user-attachments/assets/56069192-e0d2-4dbd-bb31-810567f2c184)

#### Exponential Smoothing
![image](https://github.com/user-attachments/assets/4c2286d4-bc21-4316-a22d-8da50e06150d)



### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
