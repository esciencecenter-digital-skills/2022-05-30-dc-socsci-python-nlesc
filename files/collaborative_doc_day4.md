![](https://i.imgur.com/iywjz8s.png)

# Collaborative Document

2022-06-02 Data Carpentry with Python (day 4)

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
| 9:00 | Welcome, recap of day 3 |
| 9:15 | Joining Pandas Dataframes |
| 10:15 | Coffee break |
| 10:30 | Data visualisation using Matplotlib |
| 11:30 | Coffee break |
| 11:45	| Data visualisation using Matplotlib |
| 12:45 | Workshop wrap-up & [post-workshop survey](https://carpentries.typeform.com/to/UgVdRQ?slug=2022-05-30-dc-socsci-python-nlesc) |
| 13:00 | END

## 🔧 Exercises

### Exercise: Practice with data

1. Using the `SN7577i_aa.csv` and `SN7577i_bb.csv` files, create a Dataframe which is the result of an outer join using the `Id` column to join on.
2. What do you notice about the column names in the new Dataframe?
3. How would you re-write the code so that all the columns which are common to both files are joined in the resulting Dataframe?

### Exercise: Plotting with Pandas
1. Make a histogram of the number of buildings in the compound (`buildings_in_compound`). Determine the appropriate number of bins, then include the `bins` argument in your function to improve the chart.
2. Make a scatter plot of `years_farm` vs `years_liv` and color the points by `buildings_in_compound`.
3. (Optional) Make a bar plot of the mean number of rooms per wall type (use columns `rooms` and `respondent_wall_type`). Hint: check out the function `plot.bar`, and recall how to use `groupby` to apply statistics to grouped data.

Barbara (Instructor):
```python=
df.hist("buildings_in_compound")
```
![](https://i.imgur.com/aBErYl0.png)

The bin boundaries are fractional, so we can inspect:
```python=
df.buildings_in_compound.describe()
```
|count|    131.000000
|--|--|
|mean|       2.068702
|std |       1.241530
|min |       1.000000
|25% |       1.000000
|50% |       2.000000
|75% |       3.000000
|max |       8.000000

Name: buildings_in_compound, dtype: float64
And then pick the correct number of bins:
```python=
df.hist("buildings_in_compound", bins=8)
```
![](https://i.imgur.com/RraBWsy.png)

Scatter plot:
```python=
df.plot.scatter(x="years_farm", y="years_liv", c="buildings_in_compound", colormap="cool", sharex=False)
```
![](https://i.imgur.com/B7YTQMG.png)

Group by:
```python=
rooms_mean = df.groupby("respondent_wall_type").mean()["rooms"]
rooms_mean.plot.bar()
```
![](https://i.imgur.com/jTteLXQ.png)

### Exercise: Customize your plot

Revisit your favorite plot we’ve made so far, or make one with your own data then:
- add axes labels
- add a title
- save it in two different formats

## 🧠 Collaborative Notes

### Recap of day 3
- Introduced a new library Pandas
  ```python=
  import pandas as pd
  ```
- Learned to load datasets from a file
  ```python=2
  df = pd.read_csv(...)
  ```
- Accessing columns in a dataframe
  ```python=3
  df["A"] # single column
  df.A
  df[["A", "B"]]  # multiple columns
  ```
- Accessing rows
  ```python=6
  df[0:5]  # rows from 1, to 5
  df.iloc[0]
  df.iloc[[0, 1, 2]]
  df.iloc[0, 1]
  df.loc[0:5, ["A", "B"]]
  ```
- Filters/masks
  ```python=11
  mask = df["A"] == -1  # condition
  df[mask]
  df[df["A"] == -1] # equivalent
  mask = (df["A"] == -1) & (df["B"] == 1)
  df[mask]
  ```
- Missing values
  ```python=16
  import numpy as np
  df.isnull()  # cells with missing values
  df.fillna(0)  # replace NA with 0
  df.replace(0, np.nan)  # replace 0 with NA
  ```
- overview of a dataframe
  ```python=20
  df.describe()  # overview of numerical data
  df.groupby("A").describe() # categorical values
  ```
 merge_on_2 = pd.merge(df_aa, df_bb, how ="outer" , on = "Id" )


### Joining Pandas dataframes
- appending rows
- appending columns
- more complex join: merging both rows & columns

#### Appending rows
We want to merge rows where, say, we have different set of measurements for the same experiment.  First let's read the files:
```python=
df_a = pd.read_csv("SN7577i_a.csv")
df_b = pd.read_csv("SN7577i_b.csv")
```
You may inspect with `df.head()`:

Let's merge the rows:
```python=3
df_merge_rows = pd.concat([df_a, df_b], ignore_index=True)
```
But you will note, the indices are repeated (for a & b).  We can resolve this by using the option

Let's look at the case where the number of columns do not match:
```python=
df_aa = pd.read_csv("SN7577i_aa.csv")  # Q1, Q2, Q3
df_bb = pd.read_csv("SN7577i_bb.csv")  # Q1, Q2, Q4
```

If we concatenate them:
```python=3
df_merge_row = pd.concat([df_aa, df_bb], ignore_index=True)
```
| | 	Id |	Q1| 	Q2 |	Q3| 	Q4
|--|--|--|--|--|--|
|0 |	1| 	1| 	-1 |	1.0 |	NaN
|1 |	2| 	3| 	-1| 	1.0| 	NaN
|2 |	3| 	10 |	3 |	2.0 |	NaN |
|...
|10 |	1277 |	10 |	10| 	NaN| 	6.0
11 |	1278 |	2 |	-1 |	NaN |	4.0
12 |	1279 |	2 |	-1 |	NaN 	| 5.0

- Columns missing from one dataframe are filled with NaNs
- Column data types are coerced to fit right type (float) that can store both types (NaN and integer), NaNs can only be represented as floats

*Tip:* If you want to keep the data type as integer, you may convert the column type to Pandas specifi integer type:
```python=4
df_merge_row.astype("Int64")
```


#### Appending columns from a different dataframe
```python=
df_c = pd.read_csv("SN7577i_c.csv")
df_d = pd.read_csv("SN7577i_d.csv")
```

Merge the columns:
```python=
df_merge_cols = pd.concat([df_c, df_d], axis="columns")
```
| |  	Id| 	maritl| 	numhhd| 	Id| 	Q1| 	Q2|
|--|--|--|--|--|--|--|
| 0| 	1| 	6| 	3| 	1| 	1| 	-1|
| 1 |	2| 	4 |	3| 	2| 	3| 	-1
|2 |	3 |	6 |	2 |	3 |	10| 	3

*Note:* common columns are repeated, this can be avoided by selecting only the columns that you want. When repeated columns are present, accessing by label will return both columns:
```python=
df_merge_cols["Id"]
```
|| 	Id| 	Id|
|--|--|--|
|0 |	1 |	1
|1 |	2 |	2

#### Joining data
![](https://i.imgur.com/EZLGgPL.png)


##### Inner join
```python=
df_merged_inner = pd.merge(df_c, df_d, how="inner")
```
||  	Id |	maritl| 	numhhd| 	Q1| 	Q2|
|--|--|--|--|--|--|
|0 	|1 |	6 |	3 |	1 |	-1
|1 	|2 |	4 |	3 |	3 |	-1
|2 	|3 |	6| 	2 |	10| 	3
|3 |	4 |	4 |	1 |	9 	| -1

- must have at least one column in common
- only rows where the values in the common column match will be retained
- under the hood Pandas finds the common column, and merges based on that
- it is good practice to explicitly specify the column to use

```python=2
pd.merge(df_c, df_d, how="inner", on="Id")
```

##### Outer join
```python=3
pd.merge(df_c[0:3], df_d[5:10], how="outer", on="Id")
```
|| 	Id| 	maritl| 	numhhd| 	Q1| 	Q2|
|--|--|--|--|--|--|
| 0| 	1| 	6.0| 	3.0 |	NaN 	|NaN
| 1| 	2| 	4.0 |	3.0 |	NaN| 	NaN
|2| 	3| 	6.0 |	2.0 |	NaN| 	NaN
|3| 	6| 	NaN |	NaN |	1.0| 	-1.0
|4| 	7 |	NaN |	NaN |	1.0 |	-1.0
|5| 	8 |	NaN |	NaN |	1.0 |	-1.0

- union of the values of all rows for the common column

Let's try to merge dataframes with more than one common column:
```python=4
df_c_q = pd.concat([df_c, df_d["Q1"]], axis=1)  # dataframe with >1 common column
pd.merge(df_c_q, df_d, on="Id")
```
|| 	Id| 	maritl| 	numhhd| 	Q1_x| 	Q1_y| 	Q2|
|--|--|--|--|--|--|--|
|0 |	1| 	6| 	3| 	1 |	1 |	-1
| 1 |	2| 	4 |	3 |	3 |	3 |	-1
|2| 	3| 	6| 	2 |	10| 	10| 	3

- the common column not being used in the merge (not in `on=...`) gets renamed to `_x` and `_y`, and the values are retained

We can also merge on multiple columns:
```python=6
pd.merge(df_c_q, df_d, on=["Id", "Q1"])
```
|| 	Id| 	maritl| 	numhhd| 	Q1| 	Q2
|--|--|--|--|--|--|
|0| 	1| 	6 |	3 |	1| 	-1
|1 |	2| 	4 |	3| 	3| 	-1

### Plotting with Pandas and Matplotlib
Let's work with the SAFI dataset, and get a histogram:
```python=
df = pd.read_csv("SAFI_full_shortname.csv")
df["years_liv"].hist()  # histogram
```
![](https://i.imgur.com/20wDa09.png)

Let's customise a bit, specify the number of bins:
```python=3
df["years_liv"].hist(bins=20)
```
![](https://i.imgur.com/MO3lepI.png)

Let's group by:
```python=4
df.hist(column="years_liv", by="village")
df["years_liv"].hist(by=df["village"])  # alternate
```
![](https://i.imgur.com/kiZn7D2.png)
*Note:* the second method is less preferable because it's easier to make a mistake, and pass an incorrect `by=...`.

Change the layout and figure size:
```python=6
df.hist(column="years_liv", by="village", layout=(1,3), figsize=(10, 5))
```
![](https://i.imgur.com/hGllUho.png)

#### Scatter plots
```python=
df.plot.scatter(x="gps_Latitude", y="gps_Longitude")
```
![](https://i.imgur.com/iaT2nwv.png)

Adding more information (see: [resources](#resources) for more colormaps)
```python=2
df.plot.scatter(x="gps_Latitude", y="gps_Longitude", c="gps_Altitude", colormap="viridis")
```
![](https://i.imgur.com/eQowUky.png)

*Note:* to get ticks show up properly, see this [SO answer](https://stackoverflow.com/questions/66444722/scatter-plot-x-axis-tick-labels-not-showing-up)

#### Boxplot and other plot types
The default pandas style isn't very readable:
```python=
df.boxplot(by ='village',column=['buildings_in_compound'])
```
![](https://i.imgur.com/cIs1mUh.png)

Using `seaborn`, we can get much cleaner plots:
```python=
import seaborn as sns
sns.boxplot(data=df, x="respondent_wall_type", y="buildings_in_compound")
```
![](https://i.imgur.com/vrRNQ5z.png)

```python=
sns.violinplot(data=df, x="respondent_wall_type", y="buildings_in_compound")
```
![](https://i.imgur.com/AOJIAFs.png)

```python=
sns.lmplot(data=df, x='years_farm', y='years_liv',hue='village')
```
![](https://i.imgur.com/Gp2QCXy.png)

### Using matplotlib directly
Let's get the data we want to plot
```python=
parents_from_area = df[(df.parents_liv=="yes") | (df.sp_parents_liv=="yes")] # either parents live in area
parents_not_area = df[(df.parents_liv=="no") & (df.sp_parents_liv=="no")]  # none of the parents live in the area
```
Build the plot gradually:
```python=
import matplotlib.pyplot as plt

plt.title("Time devoted to farming")
plt.ylabel("Years farming in area")
plt.xlabel("Years lived in area")

# scatter plot from two different datasets
plt.scatter(x=parents_from_area["years_liv"], y=parents_from_area["years_farm"],
            label="one or both parents from area")
plt.scatter(x=parents_not_area["years_liv"], y=parents_not_area["years_farm"],
            label="neither parents from area")

plt.legend() # include legend
plt.show() # not necessay when using Jupyter
```
![](https://i.imgur.com/CFamgAP.png)

To save a plot to a file, you can save to a file by adding `plt.savefig(..)` before you all `plt.show()`:
```python
plt.savefig("farming_parents.png", dpi=150)
```

## 📚 Resources
- Pandas user guide: [Merge, join, concatenate and compare](https://pandas.pydata.org/docs/user_guide/merging.html)
- Matplotlib [color maps](https://matplotlib.org/stable/gallery/color/colormap_reference.html)
- Seaborn [API docs](https://seaborn.pydata.org/api.html)
- [Post-workshop survey](https://carpentries.typeform.com/to/UgVdRQ?slug=2022-05-30-dc-socsci-python-nlesc&typeform-source=esciencecenter-digital-skills.github.io)
