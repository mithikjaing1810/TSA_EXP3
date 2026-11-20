# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
### Date: 06-11-2026
### Reg no : 212224240087
### Dataset : Nvidia_stock price

## AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
## ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
## PROGRAM:


```

### Import packages
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

### Load NVIDIA dataset
df = pd.read_csv('NVIDIA_STOCK(5).csv', skiprows=2)

### Rename columns
df.columns = ['Date', 'Adj Close', 'Close',
              'High', 'Low', 'Open', 'Volume']

### Convert data types
df['Date'] = pd.to_datetime(df['Date'])
df['Volume'] = pd.to_numeric(df['Volume'], errors='coerce')

### Sort data by date
df = df.dropna(subset=['Date', 'Volume'])
df = df.sort_values('Date').reset_index(drop=True)

### Assign Volume to data array
data = df['Volume'].values
N = len(data)

### Compute ACF
lags = range(35)
autocorr_values = []

### Calculate mean and variance
mean_data = np.mean(data)
variance_data = np.var(data)

### Calculate autocorrelation for each lag
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) *
            (data[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

### Plot ACF graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)

plt.title('Autocorrelation of NVIDIA Stock Volume')

plt.xlabel('Lag')

plt.ylabel('Autocorrelation')

plt.grid(True)

plt.show()

```

## OUTPUT:
<img width="846" height="547" alt="image" src="https://github.com/user-attachments/assets/63f5f47e-7c92-4a6e-b8cb-74358f3413a8" />


## RESULT:
   Thus we have successfully implemented the auto correlation function in python.
