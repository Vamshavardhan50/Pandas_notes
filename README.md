# 🐼 Pandas Notes

## 📌 Introduction

Pandas is a powerful Python library for data analysis and manipulation. It provides data structures like Series and DataFrame which are ideal for handling structured data.

## 🔧 Installation

```bash
pip install pandas
```

## 📚 Importing Pandas

```python
import pandas as pd
```

## 📊 Pandas Data Structures

### Series

A one-dimensional labeled array.

```python
s = pd.Series([10, 20, 30])
print(s)
# Output:
# 0    10
# 1    20
# 2    30
# dtype: int64
```

### DataFrame

A two-dimensional labeled data structure.

```python
data = {'Name': ['Alice', 'Bob'], 'Age': [25, 30]}
df = pd.DataFrame(data)
print(df)
# Output:
#     Name  Age
# 0  Alice   25
# 1    Bob   30
```

## 🔍 Reading Data

```python
df = pd.read_csv('data.csv')
```

## 🧭 Exploring Data

```python
print(df.head())       # First 5 rows
print(df.info())       # Summary of dataframe
print(df.describe())   # Statistical summary
print(df.columns)      # Column names
print(df.shape)        # (rows, columns)
```

## 🎯 Selecting Data

```python
print(df['Name'])         # Single column
print(df[['Name', 'Age']]) # Multiple columns
print(df.iloc[0])         # First row by position
print(df.loc[0])          # First row by label
```

## ✂️ Filtering Data

```python
print(df[df['Age'] > 25])
```

## 🔄 Modifying Data

```python
df['Age'] = df['Age'] + 1
```

## ➕ Adding/Removing Columns

```python
df['Gender'] = ['F', 'M']
df.drop('Gender', axis=1, inplace=True)
```

## 🔁 Iterating Through Rows

```python
for index, row in df.iterrows():
    print(row['Name'], row['Age'])
```

## 🧼 Handling Missing Data

```python
df.dropna()           # Drop rows with missing values
df.fillna(0)          # Fill missing values with 0
```

## 📊 Grouping and Aggregation

```python
print(df.groupby('Age').count())
```

## 🔗 Merging/Joining DataFrames

```python
df1 = pd.DataFrame({'id': [1, 2], 'name': ['Alice', 'Bob']})
df2 = pd.DataFrame({'id': [1, 2], 'age': [25, 30]})
merged = pd.merge(df1, df2, on='id')
print(merged)
# Output:
#    id   name  age
# 0   1  Alice   25
# 1   2    Bob   30
```

## 📌 Pivot Tables

```python
data = {'Name': ['Alice', 'Bob', 'Alice'], 'Subject': ['Math', 'Math', 'English'], 'Score': [90, 80, 85]}
df = pd.DataFrame(data)
pivot = pd.pivot_table(df, values='Score', index='Name', columns='Subject')
print(pivot)
# Output:
# Subject  English  Math
# Name                  
# Alice         85     90
# Bob           NaN    80
```

## 🗓️ Date/Time Handling

```python
dates = pd.to_datetime(['2023-01-01', '2023-02-01'])
df = pd.DataFrame({'Date': dates, 'Value': [100, 200]})
print(df)

print(df['Date'].dt.month)
# Output:
# 0    1
# 1    2
# Name: Date, dtype: int64
```

## 📆 Time Series Resampling

```python
df = pd.DataFrame({
    'Date': pd.date_range(start='2023-01-01', periods=6, freq='D'),
    'Sales': [100, 120, 130, 90, 150, 110]
})
df.set_index('Date', inplace=True)
weekly = df.resample('W').sum()
print(weekly)
# Output: Weekly sum of sales
```

## 📶 MultiIndexing

```python
arrays = [
    ['A', 'A', 'B', 'B'],
    [1, 2, 1, 2]
]
index = pd.MultiIndex.from_arrays(arrays, names=('Group', 'Subgroup'))
data = pd.DataFrame({'Value': [10, 20, 30, 40]}, index=index)
print(data)
# Output:
#               Value
# Group Subgroup      
# A     1            10
#       2            20
# B     1            30
#       2            40
```

## 📈 Data Visualization with Pandas

```python
df = pd.DataFrame({
    'Month': ['Jan', 'Feb', 'Mar'],
    'Sales': [200, 250, 300]
})
df.plot(x='Month', y='Sales', kind='bar')
import matplotlib.pyplot as plt
plt.show()
```

## 📁 Reading from Excel/JSON/SQL

```python
# Excel
pd.read_excel('data.xlsx')

# JSON
pd.read_json('data.json')

# SQL (requires sqlalchemy)
import sqlite3
conn = sqlite3.connect('database.db')
pd.read_sql_query("SELECT * FROM tablename", conn)
```

## 🚀 Performance Tips

```python
# Use 'category' dtype for low-cardinality strings

df['Category'] = df['Category'].astype('category')
print(df['Category'].memory_usage(deep=True))
```

## 📤 Exporting Data

```python
df.to_csv('output.csv', index=False)
```

## 📚 References

* [Pandas Official Documentation](https://pandas.pydata.org/docs/)
