# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
### Date:26.08.2025

### Reg No:212223240182

### Name: VINOTH M P
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION

B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


data = pd.read_csv('/content/test.csv')

years = data['id'].tolist()
ram_values = data['ram'].tolist()

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, ram_values)]
n = len(years)

b = (n * sum(xy) - sum(ram_values) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(ram_values) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, ram_values)]
coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]
Y = [sum(ram_values), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"Polynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

data['Linear Trend'] = linear_trend
data['Polynomial Trend'] = poly_trend
data.set_index('id', inplace=True)

data['ram'].plot(kind='line', color='blue', marker='o', label="RAM")
data['Linear Trend'].plot(kind='line', color='black', linestyle='--', label="Linear Trend")
plt.title("Linear Trend Estimation (RAM vs ID)")
plt.legend()
plt.show()
data['ram'].plot(kind='line', color='blue', marker='o', label="RAM")
data['Polynomial Trend'].plot(kind='line', color='black', marker='o', label="Polynomial Trend")
plt.title("Polynomial Trend Estimation (RAM vs ID)")
plt.legend()
plt.show()

```
### OUTPUT

A - LINEAR TREND ESTIMATION

<img width="682" height="500" alt="image" src="https://github.com/user-attachments/assets/56c4ad72-3a50-4cfc-93ce-cacce71634f2" />


B- POLYNOMIAL TREND ESTIMATION

<img width="659" height="481" alt="image" src="https://github.com/user-attachments/assets/d8b4e255-e661-4be8-bc67-0aa4048ef07b" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
