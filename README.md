# <p align="center">The Journey into Time Series:<br> Unveiling Descriptive Analytics </p>
## <p align="center"> Data Mastery Series - Episode 12: The Art of Forecasting (Part 3) </p>

---

Welcome to my GitHub repository for the 12th episode of the Data Mastery Series. 
This repository contains all the code used in my corresponding blog post (link: [Web:xxx]()).

To begin, we need to set up our Python environment with the necessary libraries:


```python 
import numpy as np
import pandas as pd

import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.figure_factory as ff
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import plotly.io as pio
```

You can get the data we will be using from this source. Below, you will find a sample of the dataset, a figure of the sample dataset, and a line chart representing it.

**Data source:** 
https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/EP11.xlsx

**Sample Dataset:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/11.%20Dataset.png)

**Line Chart:**
<br>
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/21.%20Line%20Chart.png)


In this episode, we delve into four core facets of descriptive analytics: 'Measures of Centrality', 'Measures of Variation', 'Measures of Localization', and 'Measures of Symmetry'. Let's take a closer look at each.
<br>

**1. Measures of Centrality:**

These statistical tools illustrate Centrality measures describe the 'center' of a dataset. Common measures include the mean (average), median (middle value), and mode (most common value).

```python 
# Filter data for each SKU
df_A = df[df['sku'] == 'A']
df_B = df[df['sku'] == 'B']
df_C = df[df['sku'] == 'C']

# Measures of Centrality
mean_A = df_A['value'].mean()
median_A = df_A['value'].median()
mode_A = df_A['value'].mode()

mean_B = df_B['value'].mean()
median_B = df_B['value'].median()
mode_B = df_B['value'].mode()

mean_C = df_C['value'].mean()
median_C = df_C['value'].median()
mode_C = df_C['value'].mode()

print("For SKU A: Mean = ", mean_A, ", Median = ", median_A, ", Mode = ", mode_A[0])
print("For SKU B: Mean = ", mean_B, ", Median = ", median_B, ", Mode = ", mode_B[0])
print("For SKU C: Mean = ", mean_C, ", Median = ", median_C, ", Mode = ", mode_C[0])
```

output:
- For SKU A: Mean =  43.80072463768116 , Median =  44.0 , Mode =  38
- For SKU B: Mean =  41.97826086956522 , Median =  42.0 , Mode =  44
- For SKU C: Mean =  23.282608695652176 , Median =  24.0 , Mode =  21

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_1.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_2.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_3.png)
<br>

**2. Measures of Variation**
These statistical tools illustrate the dispersion and distribution of a dataset. Recognizing the degree of data dispersion is vital for interpreting the stability or volatility of the subject under examination.

2.1 Range:

```python 
# Calculating Range for SKU A, B and C
range_A = df[df['sku']=='A']['value'].max() - df[df['sku']=='A']['value'].min()
range_B = df[df['sku']=='B']['value'].max() - df[df['sku']=='B']['value'].min()
range_C = df[df['sku']=='C']['value'].max() - df[df['sku']=='C']['value'].min()

# Printing the range
print(f"Range of SKU A: {df[df['sku'] == 'A']['value'].max()} - {df[df['sku'] == 'A']['value'].min()} = {range_A}")
print(f"Range of SKU B: {df[df['sku'] == 'B']['value'].max()} - {df[df['sku'] == 'B']['value'].min()} = {range_B}")
print(f"Range of SKU C: {df[df['sku'] == 'C']['value'].max()} - {df[df['sku'] == 'C']['value'].min()} = {range_C}")
```

output:
- Range of SKU A: 68 - 20 = 48
- Range of SKU B: 62 - 23 = 39
- Range of SKU C: 41 - 6 = 35

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_1.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_2.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_3.png)
<br>

2.2 Variance:

```python 
# Calculating Variance for SKU A, B and C
var_A = df[df['sku']=='A']['value'].var()
var_B = df[df['sku']=='B']['value'].var()
var_C = df[df['sku']=='C']['value'].var()

# Printing the variance
print(f"Variance of SKU A: {var_A}")
print(f"Variance of SKU B: {var_B}")
print(f"Variance of SKU C: {var_C}\n")
```

output:
- Variance of SKU A: 150.27650856389988
- Variance of SKU B: 71.27225296442687
- Variance of SKU C: 63.73075098814228

2.3 Standard Deviation:

```python 
# Calculating Standard Deviation for SKU A, B and C
std_A = df[df['sku']=='A']['value'].std()
std_B = df[df['sku']=='B']['value'].std()
std_C = df[df['sku']=='C']['value'].std()

# Printing the standard deviation
print(f"Standard Deviation of SKU A: {std_A}")
print(f"Standard Deviation of SKU B: {std_B}")
print(f"Standard Deviation of SKU C: {std_C}\n")
```

output:
- Standard Deviation of SKU A: 12.258731931317362
- Standard Deviation of SKU B: 8.442289557011586
- Standard Deviation of SKU C: 7.983154200448735

2.4 Coefficient of Variation:

```python 
# Calculating Coefficient of Variation for SKU A, B and C
cv_A = (std_A / df[df['sku']=='A']['value'].mean()) * 100
cv_B = (std_B / df[df['sku']=='B']['value'].mean()) * 100
cv_C = (std_C / df[df['sku']=='C']['value'].mean()) * 100

# Printing the coefficient of variation
print(f"Coefficient of Variation of SKU A: {cv_A} %")
print(f"Coefficient of Variation of SKU B: {cv_B} %")
print(f"Coefficient of Variation of SKU C: {cv_C} %")
```

output:
- Coefficient of Variation of SKU A: 27.987509413877014 %
- Coefficient of Variation of SKU B: 20.11109889293283 %
- Coefficient of Variation of SKU C: 34.2880572568293 %


**3. Measures of Localization**
These measures give us more granular insight about the distribution of data within the dataset. (see topic .describe())

**4. Measures of Symmetry**
These measures help us understand the symmetry and structure of our data distribution.

```python 
from scipy.stats import skew, kurtosis

skus = ['A', 'B', 'C']

for sku in skus:
    data = df[df['sku'] == sku]['value']

    # Calculate skewness
    skewness = skew(data)
    print(f'Skewness of SKU {sku}: {skewness}')

    # Calculate kurtosis
    kurt = kurtosis(data)
    print(f'Kurtosis of SKU {sku}: {kurt}\n')
```

output:
- Skewness of SKU A: -0.0045463589746413575, Kurtosis of SKU A: -1.061281248417483

- Skewness of SKU B: 0.04283073151454455, Kurtosis of SKU B: -0.589672638621972

- Skewness of SKU C: -0.042340305446899616, Kurtosis of SKU C: -0.59944736404992



*Special Note: Powerful Python Libraries For EDA*

**1. .describe()**
This function gives us a summary of the statistical measures of our data distribution.

```python 
df.groupby('sku')['value'].describe().T
```

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/4.1.png)
<br>

```python 
perc = [.10, .20, .30, .40, .50, .60, .70, .80, .90]  # list of percentiles
include =['object', 'float', 'int']  # list of data types

df.groupby('sku')['value'].describe(percentiles=perc, include=include)
```

<<<<<<< HEAD
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/4.2.png)
<br>

```python 
df.groupby('sku')['value'].describe(percentiles=perc, include=include).T
```
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/4.3.png)
<br>

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/3_1.png)
=======
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/3_1.png)
>>>>>>> 2f32ef6837c6a56a8c0db7fa762bb5055036f6d2
<br>


**2. YData Profiling (Previously Pandas Profiling):**

```python 
code
```

```python 
code
```

```python 
code
```

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/5.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/6.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/6.1.png)
<br>

**3. D-Tale:**

```python 
code
```

```python 
code
```

```python 
code
```

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/7.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/8.png)
<br>

**4. SweetViz:**

```python 
code
```

```python 
code
```

```python 
code
```

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/9.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/10.png)
<br>

**5. DataPrep:**

```python 
code
```

```python 
code
```

```python 
code
```

<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/11.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/12.png)
<br> ![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/13.png)
<br>

Note: Please note that Python libraries are updated frequently, and as such, the import functions may change over time. If you plan to use these libraries, please ensure you read their documentation to stay up to date with any changes.
---

Thank you for your interest in this project! Feel free to contribute, share your thoughts, or ask any questions you might have. If you found this repository useful, don't forget to give it a star ⭐. I look forward to connecting with you! 🚀

<p align="center">
<a href="https://web.facebook.com/DonatoStory"><img src="https://img.shields.io/badge/Facebook-%231877F2.svg?&style=for-the-badge&logo=Facebook&logoColor=white"/></a>
<a href="https://medium.com/donato-story"><img src="https://img.shields.io/badge/Medium-%23000000.svg?&style=for-the-badge&logo=Medium&logoColor=white"/></a>
<a href="https://linkedin.com/in/nattapong-thanngam"><img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?&style=for-the-badge&logo=LinkedIn&logoColor=white"/></a>
</p>

Follow me and let's learn together! 🌟"



