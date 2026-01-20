# Pandas Cheat Sheet

## Table of Contents

0. [Imports](#imports)
1. [Creating DataFrames](#creating-dataframes)
2. [Creating Series](#creating-series)
3. [Inspecting Data](#inspecting-data)
4. [Selecting Data](#selecting-data)
5. [Filtering](#filtering)
6. [Data Manipulation](#data-manipulation)
7. [Grouping & Aggregation](#grouping--aggregation)
8. [Sorting](#sorting)
9. [Merging & Joining](#merging--joining)
10. [Statistics](#statistics)
11. [I/O](#io)

## Imports
```python
import pandas as pd
import numpy as np
```

## Creating DataFrames

```python
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})
df = pd.read_csv('file.csv')
df = pd.DataFrame(np.random.rand(5, 3), columns=['A', 'B', 'C'])
```
## Creating Series

```python
series = pd.Series([1,2,3,4,5])
series = pd.Series({"Madrid": 12, "Paris": 10})
index = series.index 
values = series.values

```

## Inspecting Data

```python
df.head()              # First 5 rows
df.tail()              # Last 5 rows
df.info()              # Data types and memory
df.describe()          # Summary statistics
df.shape               # (rows, columns)
df.columns             # Column names
df.dtypes              # Data types

series.isna()          # Booleans indicating NaN values
```

## Selecting Data

```python
df['A']                # Select column
df[['A', 'B']]         # Select multiple columns
df.loc[0]              # Select row by label
df.iloc[0]             # Select row by index
df.loc[0, 'A']         # Select by label
df.iloc[0, 0]          # Select by position
```

## Filtering

```python
df[df['A'] > 2]                    # Boolean indexing
df[(df['A'] > 1) & (df['B'] < 6)]  # Multiple conditions
```

## Data Manipulation

```python
df['C'] = df['A'] + df['B']   # New column
df.drop('A', axis=1)          # Drop column
df.drop(0, axis=0)            # Drop row
df.rename(columns={'A': 'X'}) # Rename columns
df.fillna(0, inplace = True)  # Fill missing values
df.dropna()                   # Remove missing values

```

## Grouping & Aggregation

```python
df.groupby('A').sum()  # Group and sum
df.groupby('A')['B'].mean()  # Group specific column
df.pivot_table(values='B', index='A', aggfunc='sum')

```

## Sorting

```python
df.sort_values('A')    # Sort by column
df.sort_values(['A', 'B'])  # Sort by multiple columns
df.sort_index()        # Sort by index
```

## Merging & Joining

```python
pd.concat([df1, df2])  # Concatenate
pd.merge(df1, df2, on='key')  # Inner join
df1.join(df2)          # Join on index

```

## Statistics

```python
df.mean()              # Mean
df.median()            # Median
df.std()               # Standard deviation
df.corr()              # Correlation matrix
df.sum()               # Sum
df.count()             # Count non-null values
```

# I/O

```python
# Read
df.read_csv('file.csv', index=False)
df.read_excel('file.xlsx')

# Write
df.to_csv('file.csv', index=False)
df.to_excel('file.xlsx')
df.to_json('file.json')
df.to_sql('table', connection)
```
