Exploratory Data Analysis – Shopify Stock Dataset
1. Project Title
Exploratory Data Analysis (EDA) on Shopify Stock Data

2. Objective
The objective of this task is to perform Exploratory Data Analysis (EDA) on the Shopify stock dataset. The dataset contains historical stock market information such as opening price, highest price, lowest price, closing price, adjusted closing price, and trading volume.

The analysis includes data loading, data inspection, data cleaning, feature creation, statistical analysis, and data visualization.

3. Technologies Used
Python
Pandas
Matplotlib
Google Colab
4. Dataset
The dataset used in this task is SHOP.csv, which contains Shopify stock trading information.

Original Columns
Column	Description
date	Trading date
open	Opening stock price
high	Highest stock price
low	Lowest stock price
close	Closing stock price
adj_close	Adjusted closing price
volume	Number of shares traded
The dataset contains 2,469 rows and 7 columns.

5. Import Required Libraries
Code
import pandas as pd
import matplotlib.pyplot as plt
Description
Pandas is used for data loading, cleaning, manipulation, and statistical analysis. Matplotlib is used for creating graphs and visualizations.

6. Load the Dataset
Code
df = pd.read_csv("/content/SHOP.csv")
Description
The read_csv() function loads the SHOP.csv dataset into a Pandas DataFrame named df.

7. Display First Five Records
Code
print(df.head())
Output
                        date   open   high    low  close  adj_close     volume
0  2015-05-21 00:00:00-04:00  2.800  2.874  2.411  2.568      2.568  123039000
1  2015-05-22 00:00:00-04:00  2.607  3.110  2.600  2.831      2.831   28412000
2  2015-05-26 00:00:00-04:00  2.980  3.034  2.908  2.965      2.965    8202000
3  2015-05-27 00:00:00-04:00  3.067  3.081  2.700  2.750      2.750      7976000
4  2015-05-28 00:00:00-04:00  2.755  2.774  2.648  2.745      2.745    4000000
8. Check Dataset Shape
Code
print(df.shape)
Output
(2469, 7)
Result
The dataset contains:

Rows: 2469
Columns: 7
9. Check Dataset Information
Code
print(df.info())
Output
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2469 entries, 0 to 2468
Data columns (total 7 columns):

date         2469 non-null   object
open         2469 non-null   float64
high         2469 non-null   float64
low          2469 non-null   float64
close        2469 non-null   float64
adj_close    2469 non-null   float64
volume       2469 non-null   int64
Result
The dataset has 7 columns. Five columns are floating-point values, one is integer, and the date column is initially stored as an object.

10. Check Missing Values
Code
print(df.isnull().sum())
Output
date         0
open         0
high         0
low          0
close        0
adj_close    0
volume       0
dtype: int64
Result
There are no missing values in the dataset.

11. Remove Duplicate Records
Code
df = df.drop_duplicates()
Description
The drop_duplicates() function removes duplicate rows from the dataset.

12. Convert Date Column
Code
df["date"] = pd.to_datetime(
    df["date"],
    format="mixed",
    errors="coerce"
)
Description
The date column is converted into a datetime format so that it can be sorted and used for time-based analysis.

Note: The notebook produced a Pandas FutureWarning about mixed time zones during this conversion.

13. Sort Data by Date
Code
df = df.sort_values("date")
Description
The records are arranged in chronological order based on the date.

14. Set Date as Index
Code
df = df.set_index("date")
Description
The date column is set as the DataFrame index, which is useful for time-series analysis.

15. Remove Missing Values
Code
df = df.dropna()
Description
Any rows containing missing values are removed.

After cleaning, the dataset contains 2,469 records and 6 data columns, with the date used as the index.

16. Create New Features
16.1 Daily Price Change
Code
df["Daily_Price_'Change"] = df["close"] - df["open"]
Description
This calculates the difference between the closing price and opening price.

16.2 Daily Return Percentage
Code
df["Daily_Return_%"] = ((df["close"] - df["open"]) / df["open"]) * 100
Description
This calculates the daily stock return as a percentage.

16.3 Price Range
Code
df["Price_Range"] = df["high"] - df["low"]
Description
This calculates the difference between the highest and lowest price of the day.

17. Display Processed Data
Code
df.head()
Output
The first five records contain the original stock columns along with the newly created:

Daily_Price_'Change
Daily_Return_%
Price_Range
For example, the first record has a daily price change of approximately -0.232, daily return of approximately -8.286%, and price range of 0.463.

18. Descriptive Statistics
Code
print(df.describe())
Output
              open         high          low        close    adj_close
count  2469.000000  2469.000000  2469.000000  2469.000000  2469.000000
mean     48.464345    49.505495    47.347795    48.456613    48.456613
std      43.633916    44.470235    42.642546    43.573362    43.573362
min       1.939000     1.985000     1.848000     1.933000     1.933000
25%      10.479000    10.635000    10.275000    10.450000    10.450000
50%      35.640999    36.879002    34.655998    35.874001    35.874001
75%      76.080002    77.169998    74.589996    75.800003    75.800003
max     171.800003   176.291794   168.509506   169.059998   169.059998
The analysis also includes volume, daily price change, daily return percentage, and price range statistics.

19. Calculate Mean Return
Code
print("Mean Return:",
      df["Daily_Return_%"].mean())
Output
Mean Return: 0.08640631099421993
Result
The mean daily return is approximately 0.0864%.

20. Calculate Return Variance
Code
print("Return Variance:",
      df["Daily_Return_%"].var())
Output
Return Variance: 9.733081984179565
21. Calculate Return Standard Deviation
Code
print("Return Standard Deviation:",
      df["Daily_Return_%"].std())
Output
Return Standard Deviation: 3.1197887723657773
Result
The standard deviation of daily returns is approximately 3.12%.

22. Data Visualization
22.1 Shopify Trading Volume Trend
Code
plt.figure(figsize=(12,5))
plt.plot(df.index, df["volume"])
plt.title("Shopify Trading Volume Trend")
plt.xlabel("Date")
plt.ylabel("Volume")
plt.xticks(rotation=45)
plt.show()
Output
image
Trading Volume Trend Graph

Description
This line graph shows the variation in Shopify trading volume over time.

23. Daily Return Distribution
Code
plt.figure(figsize=(12,5))
plt.hist(df["Daily_Return_%"], bins=30)
plt.title("Shopify Daily Return Distribution")
plt.xlabel("Daily Return (%)")
plt.ylabel("Frequency")
plt.show()
Output
image
Daily Return Distribution Histogram

Description
The histogram shows the distribution of daily stock returns.

24. Shopify Stock Price Trend
Code
plt.figure(figsize=(12, 5))
plt.plot(df.index, df["Price_Range"])
plt.title("Shopify Stock Price Trend")
plt.xlabel("date")
plt.ylabel("Price_Range")
plt.xticks(rotation=45)
plt.show()
Output
image
Shopify Stock Price Trend Graph

Description
This line graph represents the variation in the daily price range of Shopify stock.

25. Key Findings
From the EDA performed:

The dataset contains 2,469 records and 7 original columns.

There are no missing values in the original dataset.

Duplicate records were removed.

The date column was converted and used as the index.

Three new features were created:

Daily Price Change
Daily Return %
Price Range
The mean daily return is approximately 0.0864%.

The variance of daily return is approximately 9.7331.

The standard deviation of daily return is approximately 3.1198%.

Trading volume, daily return distribution, and price range were visualized using Matplotlib.

26. Conclusion
The Exploratory Data Analysis helped in understanding the structure, quality, statistical characteristics, and trends in the Shopify stock dataset. The data was inspected and cleaned before calculating additional features such as daily price change, daily return percentage, and price range. Statistical measures and visualizations were then used to understand stock behaviour and trading activity.

27. Project File
EDA_TASK_3(2).ipynb
SHOP.csv
README.md
