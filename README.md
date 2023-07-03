# <p align="center"> The Journey into Time Series:<br> Beginning with Descriptive Analytics  </p>
### <p align="center"> Data Mastery Series - Episode 11: The Art of Forecasting (Part 2) </p>

---

Welcome to my GitHub repository. This section provides a code walkthrough and explanations for the descriptive analytics concepts we've explored in the context of time-series analysis.

**Data source:** 
https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/EP11.xlsx

Sample Dataset:
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/11.%20Dataset.png)

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
import plotly.subplots as sp
import plotly.io as pio
```

Our journey starts with the Frequency Distribution Tables.

**Frequency Distribution Table:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/12.FreqSummaryTable.png)

Python code for generating the Frequency Distribution Tables:
```python 
# Define the SKUs to iterate over
skus = ['A', 'B', 'C']

# Frequency analysis as DataFrames
frequency_dfs = []
for sku in skus:
    sku_df = pd.DataFrame(df[df['sku'] == sku]['value'].value_counts())
    sku_df.columns = [f"Frequency for SKU {sku}"]
    sku_df.sort_index(inplace=True)
    frequency_dfs.append(sku_df)

# Concatenate DataFrames
frequency_df = pd.concat(frequency_dfs, axis=1)
frequency_df.sort_index(inplace=True)

# Fill NaN values with 0
frequency_df.fillna(0, inplace=True)

# Print the frequency DataFrame
frequency_df
```

Next, we explore Heat Maps to get a more comprehensive understanding of the data.

**Heat Map:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/13.%20Heatmap.png)

Python code for generating the Heat Maps:
```python 
# Plotly

fig = go.Figure(data=go.Heatmap(z=frequency_df.values,
                               x=frequency_df.columns,
                               y=frequency_df.index,
                               colorscale='YlGnBu'))

fig.update_layout(title="Frequency Analysis by SKU",
                  xaxis=dict(title="SKU"),
                  yaxis=dict(title="Value"), 
                  coloraxis_colorbar=dict(title="Frequency"))

pio.show(fig)
```

Moving forward, we delve into Pie Charts.

**Pie Chart:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/14.Piechart.png)

Python code for generating the Pie Charts:
```python 
# Calculating the sum of values for each SKU
sku_sum = df_pivot.sum()

plt.figure(figsize=(4, 4))  # Adjust the figure size as desired

# Creating the pie chart
plt.pie(sku_sum, labels=sku_sum.index, autopct='%1.1f%%')
plt.title('Pie Chart: Sum of Value by SKU')
plt.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
```

Next, we create Bar Charts to compare data across different categories.

**Bar Chart:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/15.Barchart.png)

Python code for generating the Bar Charts:
```python 
# Extracting the data for the x-axis (sku) and y-axis (sum of value)
x = df_pivot.columns[1:].tolist()  # Exclude the 'date' column
y = df_pivot.sum().tolist()

plt.figure(figsize=(4, 4))  # Adjust the figure size as desired

# Creating the bar chart
plt.bar(x, y)
plt.xlabel('SKU')
plt.ylabel('Sum of Value')
plt.title('Bar Chart: Sum of Value by SKU')
plt.show()
```


And here's another variant of the bar chart:

**Bar Chart-2:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/16.Barchart2.png)

Python code for generating the Bar Chart-2:

```python 
skus = df['sku'].unique()

fig = sp.make_subplots(rows=len(skus), cols=1, shared_xaxes=True, subplot_titles=[f"Frequency analysis for SKU {sku}" for sku in skus], vertical_spacing=0.05)

for i, sku in enumerate(skus):
    frequencies = df[df['sku'] == sku]['value'].value_counts().sort_index()
    fig.add_trace(go.Bar(x=frequencies.index, y=frequencies.values), row=i+1, col=1)

fig.update_layout(height=800, width=500, title_text="Frequency Analysis by SKU")
fig.update_xaxes(title_text="Value", row=len(skus), col=1)
fig.update_yaxes(title_text="Frequency", row=len(skus), col=1)

pio.show(fig)
```

We then explore Histograms to understand the distribution of our data.

**Histogram:**
<br>
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/17.%20Histrogram.png)

Python code for generating the Histograms:
```python 
# Create a subplot for each SKU
fig = sp.make_subplots(rows=len(skus), cols=1, subplot_titles=[f"Histogram for SKU {sku}" for sku in skus], vertical_spacing=0.05, shared_xaxes=True)

# Iterate over each SKU
for i, sku in enumerate(skus):
    # Select the values for the SKU
    values = df_pivot[sku].values

    # Create histogram
    fig.add_trace(go.Histogram(x=values, nbinsx=15, opacity=0.5), row=i+1, col=1)

    fig.update_xaxes(title_text="Value", row=i+1, col=1)
    fig.update_yaxes(title_text="Frequency", row=i+1, col=1)

fig.update_layout(height=700, width=500, title_text="Histograms for SKUs", showlegend=False)

pio.show(fig)
```

Next, we generate a Kernel Density Estimation (KDE) to smooth out our histogram.

**Kernel Density Estimation:**
<br>
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/18.%20KDE.png)

Python code for generating the KDE:
```python 
# (Replace to Matplotlib version)
# Remove the 'date' column from df_pivot columns
skus = df_pivot.columns[1:]

# Create a subplot for each SKU
fig, axs = plt.subplots(len(skus), 1, figsize=(6, 8), sharex=True)

# Iterate over each SKU
for i, sku in enumerate(skus):
    # Select the values for the SKU
    values = df_pivot[sku].values

    # Create histogram with KDE plot
    sns.histplot(values, bins=15, kde=True, ax=axs[i])

    axs[i].set_title(f"Histogram with KDE for SKU {sku}")
    axs[i].set_xlabel("Value")
    axs[i].set_ylabel("Frequency")

plt.tight_layout()
plt.show()
```

And here's another example of using KDE:

**Kernel Density Estimation-2:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/19.%20KDE-2.png)

Python code for generating the KDE-2:
```python 
# Transpose the df_pivot DataFrame
df_pivot_transposed = df_pivot.transpose()

# Convert Timestamp objects to numerical values
df_pivot_transposed = df_pivot_transposed.apply(pd.to_numeric, errors='coerce')

# Handle missing values
df_pivot_transposed = df_pivot_transposed.dropna()

# Extract the column names from df_pivot_transposed for the x-axis
x_axis = df_pivot_transposed.columns

# Extract the SKU values from df_pivot_transposed for the legend labels
legend = df_pivot_transposed.index

# Create histogram with line histogram using plotly
hist_data = df_pivot_transposed.values.tolist()

# Create distplot with curve_type set to 'normal' and reduced bin_size
fig = ff.create_distplot(hist_data, legend, colors=['#A56CC1', '#63F5EF', '#FFA15A'],
                         bin_size=4, show_rug=False)

# Set the chart title and axis labels
fig.update_layout(title='Histogram with Line Histogram', xaxis_title='Value', yaxis_title='Frequency')

# Display the plot
fig.show()
```

Following that, we plot Box Plots to summarize the distribution of our data.

**Box Plot:**
<br>
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/20.%20Boxplot.png)

Python code for generating the Box Plots:
```python 
# Choose the x-axis column from the "df" dataset
x_axis = 'sku'

# Choose the y-axis column from the "df" dataset
y_axis = 'value'

# Create the box plot using seaborn
sns.boxplot(data=df, x=x_axis, y=y_axis)

# Set the chart title and axis labels
plt.title('Box Plot: {} vs {}'.format(y_axis, x_axis))
plt.xlabel(x_axis)
plt.ylabel(y_axis)

# Display the plot
plt.show()
```


Lastly, we generate Line Charts to examine trends over time.

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
*** 

"Thank you for your interest in this project! Please feel free to contribute or share your thoughts. Don't forget to leave a star ⭐ if this repository was useful for you. Looking forward to connecting with you! 🚀

<p align="center">
<a href="https://web.facebook.com/DonatoStory"><img src="https://img.shields.io/badge/Facebook-%231877F2.svg?&style=for-the-badge&logo=Facebook&logoColor=white"/></a>
<a href="https://medium.com/donato-story"><img src="https://img.shields.io/badge/Medium-%23000000.svg?&style=for-the-badge&logo=Medium&logoColor=white"/></a>
<a href="https://linkedin.com/in/nattapong-thanngam"><img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?&style=for-the-badge&logo=LinkedIn&logoColor=white"/></a>
</p>

Follow me and let's learn together! 🌟"

