# Q1: How to apply a function to each element in a DataFrame?
Ans:

```python
    df['NewColumn'] = df['OldColumn'].apply(lambda x: your_function(x))
```
For e.g.:
```python
# Applying a function to each element
df['Salary'] = df['Salary'].apply(lambda x: x + 1000)
print(df)
```

# Q2: What is difference between pivot and pivot_table?
Ans: `pivot` and `pivot_table` are both methods in pandas that are used for reshaping or transforming data in a DataFrame, but they are used in slightly different scenarios:

1. **pivot:**
   - The `pivot` method is used for reshaping data based on the values in a single column.
   - It takes three arguments: the index (rows), the columns, and the values to fill the DataFrame.
   - It is suitable when you have a simple DataFrame and want to pivot it based on the values in a single column.

   **Example:**
```python
   df = pd.DataFrame({'Date': ['2022-01-01', '2022-01-01', '2022-01-02'],
                      'Category': ['A', 'B', 'A'],
                      'Value': [10, 15, 20]})
   
   pivoted_df = df.pivot(index='Date', columns='Category', values='Value')
```

2. **pivot_table:**
   - The `pivot_table` method is more versatile and is used for creating a spreadsheet-style pivot table.
   - It can handle multiple index and column values and can also aggregate data using various aggregation functions (default is mean).
   - It is suitable when you need to perform aggregation (e.g., sum, mean) on the values based on multiple columns.

   **Example:**
   
```python
   df = pd.DataFrame({'Date': ['2022-01-01', '2022-01-01', '2022-01-02'],
                      'Category': ['A', 'B', 'A'],
                      'Value': [10, 15, 20]})
   
   pivot_table_df = df.pivot_table(index='Date', columns='Category', values='Value', aggfunc='sum')
```

In summary, if you have a simple scenario where you just want to reshape your data based on values in a single column, you can use `pivot`. If you need more flexibility, such as handling multiple index and column values and performing aggregations, then `pivot_table` is the more appropriate choice.

# Q3: **How to convert a column to datetime format?**

Ans:
   
 ```python
    df['DateColumn'] = pd.to_datetime(df['DateColumn'])
```
# Q4: **How to apply a function element-wise to a DataFrame?**
    
```python
    df = df.applymap(lambda x: your_function(x))
```

# Q5: **How to select specific rows and columns in a DataFrame?**
    
```python
    selected_data = df.loc[df['Column1'] > 25, ['Column1', 'Column2']]
```

# Q6: **How to melt a DataFrame?**
    
```python
    melted_df = pd.melt(df, id_vars=['Column1'], value_vars=['Column2', 'Column3'])
```

# Q7: **How to create a new column based on conditions from multiple columns?**
    
```python
    df['NewColumn'] = np.where((df['Column1'] > 25) & (df['Column2'] == 'Value'), 'Yes', 'No')
 ```

The given code snippet creates a new column (`NewColumn`) in a DataFrame (`df`) based on conditions from multiple columns (`Column1` and `Column2`). The new column is assigned the value 'Yes' if both conditions are met; otherwise, it is assigned the value 'No'. Here are a couple of examples to illustrate its usage:

### Example 1:

```python
import pandas as pd
import numpy as np

# Create a sample DataFrame
data = {'Column1': [30, 20, 35, 18],
        'Column2': ['Value', 'Other', 'Value', 'Value']}
df = pd.DataFrame(data)

# Apply the condition to create the new column
df['NewColumn'] = np.where((df['Column1'] > 25) & (df['Column2'] == 'Value'), 'Yes', 'No')

# Display the resulting DataFrame
print(df)
```

Output:
```
   Column1 Column2 NewColumn
0       30   Value       Yes
1       20   Other        No
2       35   Value       Yes
3       18   Value        No
```
# Q8: Tell me the difference between the map, apply, and applymap in pandas.
Ans: In pandas, `map`, `apply`, and `applymap` are methods used for transforming data in different ways. Here's a brief explanation of each:

1. **`map`:**
   - **Usage:** Used for element-wise transformations on a Series.
   - **Functionality:** It applies a function to each element of the Series.
   - **Applicability:** Typically used for simple transformations that can be applied element-wise.

   **Example:**
   ```python
   # Using map to replace values in a Series
   df['column'] = df['column'].map({'old_value': 'new_value'})
   ```

2. **`apply`:**
   - **Usage:** Used for element-wise or along-the-axis transformations on a Series or DataFrame.
   - **Functionality:** It applies a function along the axis of the DataFrame or Series.
   - **Applicability:** More versatile than `map` and can handle more complex transformations. Can be used on both Series and DataFrames.

   **Example:**
   ```python
   # Using apply to apply a function along a column
   df['new_column'] = df['column'].apply(lambda x: x * 2)
   ```

3. **`applymap`:**
   - **Usage:** Used for element-wise transformations on a DataFrame.
   - **Functionality:** It applies a function to each element of the DataFrame.
   - **Applicability:** Designed specifically for DataFrames and is used when you want to apply a function element-wise to every element in the entire DataFrame.

   **Example:**
   ```python
   # Using applymap to apply a function to every element in a DataFrame
   df = df.applymap(lambda x: x ** 2)
   ```

In summary:
- **`map`** is for Series and is used for simple, element-wise transformations.
- **`apply`** is versatile and can be used for both Series and DataFrames, allowing for more complex transformations along an axis.
- **`applymap`** is for DataFrames and is used for element-wise transformations on every element in the entire DataFrame.

It's important to note that all these methods return new objects and do not modify the original data in place, unless specified.



