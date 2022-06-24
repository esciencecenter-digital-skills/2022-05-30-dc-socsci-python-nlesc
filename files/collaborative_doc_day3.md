![](https://i.imgur.com/iywjz8s.png)

# Collaborative Document

2022-06-01 Data Carpentry with Python (day 3)

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

## 👮Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.

## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, type `/hand` in the chat window.

To get help, type `/help` in the chat window.

You can ask questions in the document or chat window and helpers will try to help you.

## 🖥 Workshop information

:computer:[Workshop website](https://esciencecenter-digital-skills.github.io/2022-05-30-dc-socsci-python-nlesc/)

🛠 [Setup](https://esciencecenter-digital-skills.github.io/2022-05-30-dc-socsci-python-nlesc/#setup)

:arrow_down: Download [pandas-data.zip](https://github.com/esciencecenter-digital-skills/2022-05-30-dc-socsci-python-nlesc/raw/main/files/pandas-data.zip)


## 🗓️ Agenda
| Time | Topic |
|--:|:---|
| 9:00 | Welcome, recap of day 2 |
| 9:15 | Reading data from a file using Pandas |
| 10:15 | Coffee break |
| 10:30 | Extracting row and columns |
| 11:30 | Coffee break |
| 11:45	| Data Aggregation using Pandas |
| 12:45 | Day 3 wrap-up |
| 13:00| END |

## 🔧 Exercises

### Exercise: head and tail
1. As well as the `head()` method there is a `tail()` method. What do you think it does? Try it.
2. (Optional) Both methods accept a single numeric parameter. What do you think it does? Try it.

### Exercise: Print all columns
1. When we asked for the column names and their data types, the output was abridged, i.e. we didn’t get the values for all of the columns. Can you write a small piece of code which will print all of the values on separate lines. Paste your code in the collaborative document.
2. (optional): Using if statements, write a piece of code that prints 'big dataset' if the number of columns is larger than 10, and 'small dataset' if the number of columns is smaller.
3. (even more optional): Write a function that returns whether a dataset has more than 10 columns. (it should return a boolean value)

### Exercise: Pandas columns
What happens if you:
1. List the columns you want out of order from the way they appear in the file?
2. Put the same column name in twice?
3. Put in a non-existing column name? (a.k.a Typo)

### Exercise: aggregation
In breakout rooms. Discuss the answers in your group and write the answers in the collaborative document.
1. Read in the SAFI_results.csv dataset.
2. Get a list of the different E26_affect_conflicts values.
3. Groupby E26_affect_conflicts and describe the results.
4. How many of the respondents never had any conflicts?
5. (optional) Using groupby find out whether farms that use water ('E01_water_use') have more plots ('D_plots_count') than farms that do not use water.

## 🧠 Collaborative Notes

On day 2 we have learned how to:
* Work in the Jupyter environment
* Create variables and assign values to them
* Check the type of a variable (integer, string, boolean, list)
* Perform simple arithmetic operations
* Specify parameters when using built-in functions
* Get help for functions
* Conditionally execute a section of code (`if` statement)
* Execute a section of code on a list of items (`for` loop)
* Create and use simple functions
* Use functions written by others by importing libraries into your code

### Concept recap
Variables:
```python=
a = 3  # integer
b = "hello world"  # string
c = True  # boolean
d = [1, 2, 3, 4]  # list
```

Function (call):
```python=5
print(a)  # built-in function to print
# 3
```

Methods:
```python=7
b.split(" ")
# ['hello', 'world']
```

Control structure:
```python=9
if condition:
    # code if condition is True

for i in iterable:
    # code to repeat for each of `i`
```

Function (definition):
```python=14
def function_name(arg1, arg2):
    """
    What does the function do (this is a docstring)
    """
    # body of function
    return variable
```

List vs Tuple:
```python=
a = [1, 2, 3, 4]  # list: mutable
b = (1, 2, 3, 4)  # tuple: immutable
```

### Working with Pandas

- Reading data stored in CSV files (other file formats can be read as well)
- Slicing and subsetting data in Dataframes (=tables)
- Dealing with missing data
- Inserting and deleting columns from data structures
- Aggregating data using data grouping facilities using the split-apply-combine paradigm
- Joining of datasets (after they have been loaded into Dataframes)
- Creating simple plots

```python=
import pandas as pd
```

We will look at `Series` and `DataFrame`.
- `Series`: like column, or vector in other languages
- `DataFrame`: like a table, 2D array

*Tip:* to figure out current working directory
- from Python
```python
import os
os.getcwd()
# /path/to/working/directory
```
- inside a Jupyter cell, type `!pwd`

#### Load Data
We read a tab separated file, and save the result in a variable `df`.
```python=2
df = pd.read_csv("SN7577.tab", sep="\t")
```

*Tip:* You can find all supported options in the docstring of `read_csv`: `help(pd.read_csv)`

You can inspect the dataframe by executing the following:
```python
df
# print out of the dataframe
```
The output can be limited to fewer rows by calling `df.head()`, or `df.tail()`.  Both take a numeric argument which specifies the number of rows to include.

### Exploring the dataframe
```python=3
len(df)  #length/number of rows
# 1286
df.shape  # number of rows and columns
# (1286, 202)
df.size  # number of cells (row x columns)
# 259772
```
*Note:* unlike `.head()` or `.tail()`, `.shape` and `.size` are attributes, not functions.  You can inspect them either by looking at the completion menu shown in Jupyter when you press `tab`, or by looking at their type: `type(df.shape)`.

```python=9
df.columns
# Index(['Q1', 'Q2', 'Q3', 'Q4', 'Q5ai', 'Q5aii', 'Q5aiii', 'Q5aiv', 'Q5av',
#        'Q5avi',
#        ...
#        'numhhd', 'numkid', 'numkid2', 'numkid31', 'numkid32', 'numkid33',
#        'numkid34', 'numkid35', 'numkid36', 'wts'],
#       dtype='object', length=202)
df.dtypes
# Q1            int64
# Q2            int64
# Q3            int64
# Q4            int64
# Q5ai          int64
#              ...
# numkid33      int64
# numkid34      int64
# numkid35      int64
# numkid36      int64
# wts         float64
# Length: 202, dtype: object
```

*Note:* When printing long output, Pandas abridges the output to fit in the screen.  To inspect all of the values, we can resort to plain Python

```python=
for col in df.columns
    print(col)
# Q1
# Q2
# ...
```

### Selecting columns & rows
Read first 3 columns:
```python=
df_few_cols = pd.read_csv("SN7577.tab", sep='\t', usecols= [0,1,2])
```
or, by name:
```python=2
df_few_cols = pd.read_csv("SN7577.tab", sep='\t', usecols= ["Q1", "Q2", "Q3"])
```
Selecting a column from a dataframe:
```python=3
df["Q1"]
df.Q1  # supported, but not recommended as might not work sometimes
```
Select multiple columns:
```python=5
df[["Q1", "Q2", "Q3"]]
```
Selecting rows:
```python=6
df[0:10]  # select first 10 rows
```
*Note:* using just the number will not work
```python
df[0]  # gives `KeyError`
```
This is because Pandas is looking for a column called `0`

### Indexing by position
```python=
df.iloc[[0, 1, 2]]  # first 3 rows
```
You can also select columns by providing a second argument:
```python=2
df.iloc[1:10, [0, 1, 2]]  # select rows 2-10, and columns 1-3
```
*Note:* note that the row and column numbers are 0-indexed, (counting starts at 0)

Indexing by name:
```python=3
df.loc[[0, 1, 2], ["Q1", "Q2", "Q3"]]  # select first 3 rows, and columns
```
*Tip:* The indexer method (`.iloc[]` or `.loc[]`) accepts:
- slices: `0:4` (0-3)
- lists: `[0, 1, 2, 3]` or `["Q1", "Q2", "Q3"]`
- name: for single column or rows, just the name, say, `0` or ``"Q"``

Some other column manipulation
```python=4
df[["Q2", "Q1"]]  # reorder columns
df[["Q1", "Q1"]]  # repeat columns
df["nonexistent"]  # raises `KeyError`
```

### Filtering rows
Filter all rows where Q1 is equal to 1
```python=
mask = df["Q1"] == 1
df[mask]  # rows where Q1 is 1
df[df["Q1"] == 1]  # equivalent as above
```

Combining multiple conditions:
```python=4
mask = (df["Q1"] == 1) & (df["Q2"] == -1)
df[mask]
```
*Note:* the `&` operator is overloaded in Pandas to do boolean operation between array elements.  In normal Python, the ampersand is a bitwise operator, the two should not to be confused.

To select specific columns after applying our mask, we can do:
```python=6
df[mask][["Q1", "Q2"]]  # select first two columns after filtering
```

### Summarising data
```python=
df_SAFI = pd.read_csv("SAFI_results.csv")
df_SAFI.describe()  # summary of numeric columns
df_SAFI.describe().T  # transposes the output, useful if you have lots of columns
```

*Tip:* `df.info()` gives you a summary of data types

```python=4
df_SAFI.min().T
```
Some text columns are included here, because text can be sorted (alphabetically)

```python=5
df_SAFI.count()
```
Note some columns have a different count, because they have missing values, and missing values are not included in summary statistics.

```python=6
df_SAFI["B_no_membrs"].describe()
```
We can also call `.describe()` on individual columns.
```python=7
print(df_SAFI['B_no_membrs'].min())
print(df_SAFI['B_no_membrs'].max())
print(df_SAFI['B_no_membrs'].mean())
print(df_SAFI['B_no_membrs'].std())
print(df_SAFI['B_no_membrs'].count())
print(df_SAFI['B_no_membrs'].sum())
# 2
# 19
# 7.190839694656488
# 3.1722704895263734
# 131
# 942
```
Similar for other summary statistics methods.

### Dealing with missing values
We can count missing values in a column with:
```python=
df_SAFI.isnull().sum()
```
We can also do this for individual columns:
```python=2
df_SAFI['E19_period_use'].isnull().sum()
df_SAFI['E19_period_use'].describe()
```
In this column, missing value means the land wasn't irrigated, so we can fill the missing values with 0.
```python=4
df_SAFI['E19_period_use'].fillna(0, inplace=True)
```
*Note:* `inplace=True` overwrites the existing dataframe, this is usually not considered to be good practice

If not using `inplace`, we can save the new filled column into the original dataframe as:
```python=
df_SAFI['E19_period_use_noNA'] = df_SAFI['E19_period_use'].fillna(0)
df_SAFI['E19_period_use'].isnull.sum()
# 39
df_SAFI['E19_period_use_noNA'].isnull.sum()
# 0
```

Similarly, we can also replace existing values:
```python=6
import numpy as np  # need numpy for np.NaN
df_SAFI["E19_period_use_withNA"] = df_SAFI['E19_period_use_noNA'].replace(0, np.NaN)
```
We can see the columns we manipulated like this:
```python=8
df_SAFI[[col for col in df_SAFI.columns if col.startswith("E19")]].describe()
```

|	E19_period_use |	E19_period_use_noNA |	E19_period_use_withNA
|------|----|---
| count |	92.000000 |	131.000000 |	92.000000
| mean |	12.043478 |	8.458015 |	12.043478
| std |	8.583031 |	9.062399 |	8.583031
| min |	1.000000 |	0.000000 |	1.000000
| 25% |	4.000000 |	0.000000 |	4.000000
| 50% |	10.000000 |	5.000000 |	10.000000
| 75% |	20.000000 |	15.500000 |	20.000000
| max |	45.000000 |	45.000000 |	45.000000

*Note:* we are indexing by creating a filtered list of columns that start with `"E19"`:
```python
[col for col in df_SAFI.columns if col.startswith("E19")]  # list comprehension
# ['E19_period_use', 'E19_period_use_noNA', 'E19_period_use_withNA']
```

### Categorical variables
```python=
df_SAFI.dtypes[:20]  # look at the data types of the first 20 columns
```
Let's look at `"C01_respondent_roof_type"`
```python=2
pd.unique(df_SAFI['C01_respondent_roof_type'])
# array(['grass', 'mabatisloping', 'mabatipitched'], dtype=object)
```
We can group by the roofing type:
```python=4
grouped_data = df_SAFI.groupby('C01_respondent_roof_type')
grouped_data.describe()
```
We can inspect a specific column:
```python=6
grouped_data["A11_years_farm"].describe()
```
| 	| count| 	mean| 	std| 	min| 	25% |	50%| 	75%| 	max
| --|--|--|--|--|--|--|--|--|
| **C01_respondent_roof_type**
|grass| 	73.0| 	14.986301| 	11.635068| 	1.0 |	6.0| 	12.0| 	20.00| 	60.0
| mabatipitched |	10.0 |	21.300000 |	11.916841| 	9.0 |	17.0 |	20.0 |	20.75 |	53.0
| mabatisloping| 	48.0 |	15.979167| 	9.315943 |	2.0 |	10.0 |	16.0 |	20.25 |	50.0

We can also group by multiple columns:
```python=7
grouped_data2 = df_SAFI.groupby(['C01_respondent_roof_type', 'C02_respondent_wall_type'])
grouped_data2["A11_years_farm"].describe()
```
| 	| | 	count | 	mean | 	std | 	min | 	25% |	50% | 	75%  |	max
| --|--|--|--|--|--|--|--|--|--|
| **C01_respondent_roof_type** |	**C02_respondent_wall_type**
| grass | 	burntbricks | 	22.0 |	16.772727 |	9.159600 |	5.0 |	11.25 |	15.0 |	20.75 |	41.0
||muddaub |	42.0 |	13.904762| 	13.110803 |	1.0 |	4.25 |	11.0 |	20.00 |	60.0
||sunbricks| 	9.0| 	15.666667 |	10.087121 |	6.0 |	10.00 |	12.0| 	17.00 |	35.0
|mabatipitched| 	burntbricks| 	6.0 |	18.000000 |	4.857983 |	9.0 |	17.00 |	20.0 |	20.75 |	22.0
||muddaub |	3.0 |	28.333333 |	21.733231 |	12.0 |	16.00 |	20.0 |	36.50 |	53.0
||sunbricks |	1.0 |	20.000000 |	NaN |	20.0 |	20.00 |	20.0 |	20.00 	|20.0
|mabatisloping |	burntbricks |	39.0 	|14.666667 |	8.285477 |	2.0 |	9.00 |	15.0 |	20.00 |	40.0
||cement |	1.0 |	10.000000 |	NaN 	|10.0 |	10.00 |	10.0 |	10.00 |	10.0
||muddaub |	1.0 |	22.000000 |	NaN |	22.0 	|22.00 |	22.0 |	22.00 |	22.0
||sunbricks| 	7.0 |	23.285714 	|12.632159 	|10.0 	|18.00 |	22.0 |	22.50 |	50.0


## Questions

* Recommendations for sites/books for more exercises for Python for this particular purpose?


## 📚 Resources

* [Dataset: Audit of Political Engagement 11, 2013](https://beta.ukdataservice.ac.uk/datacatalogue/studies/study?id=7577&type=data%20catalogue#!/details)
* [Data science with Python tutorial](https://www.geeksforgeeks.org/data-science-tutorial/)
* [Pandas documentation](https://pandas.pydata.org/docs)
* [Python documentation](https://docs.python.org/3/index.htmlw)