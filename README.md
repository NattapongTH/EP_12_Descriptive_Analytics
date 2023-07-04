# <p align="center"> The Journey into Time Series:<br> Unveiling Descriptive Analytics  </p>
### <p align="center"> Data Mastery Series - Episode 12: The Art of Forecasting (Part 3) </p>

---

Welcome to my GitHub repository. This section provides a code of my blog (link Web:xxx)



Before we begin, let's set up our environment:

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

To wrap up previous chapter, following is like of dataset,sample dataset figure and line chart.

**Data source:** 
https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/EP11.xlsx

**Sample Dataset:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/11.%20Dataset.png)

**Line Chart:**
<br>
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/21.%20Line%20Chart.png)

Python code for generating the Line Charts:
```python 
fig = go.Figure()

for sku in df['sku'].unique():
    filtered_df = df[df['sku'] == sku]
    fig.add_trace(go.Scatter(x=filtered_df['date'], y=filtered_df['value'], name=sku))

fig.update_layout(title="Line Chart: Value by SKU",
                  xaxis=dict(title="Date"),
                  yaxis=dict(title="Value"))

pio.show(fig)
```

This chapter will focus core facets of descriptive analytics are 'Measures of Centrality', 'Measures of Variation', 'Measures of Localization', and 'Measures of Symmetry',
<br>

**1. Measures of Centrality:**

These statistical tools illustrate Centrality measures describe the 'center' of a dataset. Common measures include the mean (average), median (middle value), and mode (most common value).

```python 
code
```

output:
- For SKU A: Mean =  43.80072463768116 , Median =  44.0 , Mode =  38
- For SKU B: Mean =  41.97826086956522 , Median =  42.0 , Mode =  44
- For SKU C: Mean =  23.282608695652176 , Median =  24.0 , Mode =  21

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_1.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_2.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/1_3.png)
<br>

**2. Measures of Variation**
These statistical tools illustrate the dispersion and distribution of a dataset. Recognizing the degree of data dispersion is vital for interpreting the stability or volatility of the subject under examination.

2.1 Range:

```python 
code
```

output:
- Range of SKU A: 68 - 20 = 48
- Range of SKU B: 62 - 23 = 39
- Range of SKU C: 41 - 6 = 35

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_1.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_2.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/2_3.png)
<br>

2.2 Variance:

```python 
code
```

output:
- Variance of SKU A: 150.27650856389988
- Variance of SKU B: 71.27225296442687
- Variance of SKU C: 63.73075098814228

2.3 Standard Deviation:

```python 
code
```

output:
- Standard Deviation of SKU A: 12.258731931317362
- Standard Deviation of SKU B: 8.442289557011586
- Standard Deviation of SKU C: 7.983154200448735

2.4 Coefficient of Variation:

```python 
code
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
code
```

output:
- Skewness of SKU A: -0.0045463589746413575, Kurtosis of SKU A: -1.061281248417483

- Skewness of SKU B: 0.04283073151454455, Kurtosis of SKU B: -0.589672638621972

- Skewness of SKU C: -0.042340305446899616, Kurtosis of SKU C: -0.59944736404992



*Special Note: Powerful Python Libraries For EDA*

**1. .describe()**
These measures help us understand the symmetry and structure of our data distribution.

```python 
code
```

```python 
code
```

```python 
code
```

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/3_1.png)
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

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/5.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/6.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/6.1.png)
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

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/7.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/8.png)
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

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/9.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/10.png)
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

<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/11.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/12.png)
<br>
![alt](https://github.com/NattapongTH/EP_12_Descriptive_Analytics/blob/main/Photo/13.png)
<br>

Note: Python Libraries always have update and sometime the import function will be change. if you want to use it, please reconfirm by read their document.

"Thank you for your interest in this project! Please feel free to contribute or share your thoughts. Don't forget to leave a star ⭐ if this repository was useful for you. Looking forward to connecting with you! 🚀

<p align="center">
<a href="https://web.facebook.com/DonatoStory"><img src="https://img.shields.io/badge/Facebook-%231877F2.svg?&style=for-the-badge&logo=Facebook&logoColor=white"/></a>
<a href="https://medium.com/donato-story"><img src="https://img.shields.io/badge/Medium-%23000000.svg?&style=for-the-badge&logo=Medium&logoColor=white"/></a>
<a href="https://linkedin.com/in/nattapong-thanngam"><img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?&style=for-the-badge&logo=LinkedIn&logoColor=white"/></a>
</p>

Follow me and let's learn together! 🌟"



