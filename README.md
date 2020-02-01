# PandasFrequentlyUsedFunctions
### Breif summary, details see jupyter file
## 1. Create data Frame
### 1.1 input dict
    pd.DataFrame
    df.values
    df[['col1','col2']]
### 1.2 input csv/txt
| Parameters  | meaning |
| ------------- | ------------- |
| header  | default 1st row is header; set header=None, all are data, no header  |
| index_col  | default 1st column is index; set index_col=-1, no column index  |
| sep/delimiter  | default read_csv is ",", read_table is "\t"  |
| encoding  | -  |
## 2. Manipulate Data
| axis | meaning |
| ------ | ------ |
| axis=0  | row |
| axis=1  | column |
### 2.1 index & slice
    df[['col1','col2']]
    df[0:2]
    df[df['col3']>3]
    df[df['col3'>3]
    df[(df['col3']>3) & (df['col2'] > 4)]
#### 2.1.1 loc, iloc difference 
| axis | meaning   |
|------|------|
|   loc  | gets rows (or columns) with particular labels from the index|
|   iloc  | gets rows (or columns) at particular positions in the index(so it only takes integers)|
iloc works based on interger position
loc works based on labels
    df.iloc[0]  always returns the 1st row
    df.iloc[-5:] always returns the last 5 rows
    df.iloc[:,2] always returns the 3rd colum
    df.loc['a'] returns the row with name(label) "a"
    df.lov["b":, "date"]
### 2.2 Change data
#### 2.2.1 use value to change
#### 2.2.2 use list to change
#### 2.2.3 use Series to change
### 2.3 reindex
    df.reindex([1,2,4,5])
    df.reindex(columns=reIndexCols)
### 2.4 drop
    df.drop('Ohio')                   # drop by row
    df.drop(['one', 'two'], axis=1)   # drop by column
### 2.5 functions
#### 2.5.1 using numpy
    np.max(df)
    np.man(df, axis=1)
    np.abs(df)
#### 2.5.2 using functions for row or column
    f = lambda x: x.max() - x.min()
    df.apply(f)      # apply row by row, returns results as columns
    df.apply(f, axis=1) # return results as row
### 2.6 sort
#### 2.6.1 sort based on index/columns
    df.sort_index()
    df.sort_index(1, ascending=False)
#### 2.6.2 sort based on values of multiple columns
    df.sort_values(by=['two','one'], ascending=False)
### 2.7 aggregate and statistics
#### 2.7.1 sum, mean, max
    df.sum()  # return results as columns
    df.sum(axis=1) # retusn results as row
### 2.8 deal mising value
    df.dropna()  # drop row with any null
    df.dropna(how="all", axis=0,inplace=False) # drop row with all value of null
    df.fillna({1:"fill_null_1",2:"fill_null_2"}) # fill 1st column, 2nd column with specified values
    df.fillna(method="ffill")    
 ### 2.9 Pandas tricks 
 (refer:https://gdcoder.com/be-a-more-efficient-data-scientist-by-using-these-pandas-tricks/)
#### 2.9.1 fix messy dataframe column names
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_').str.replace('(', '').str.replace(')', '')

eg:
s = "Sales (Dollars)'
result: sales_dollars
#### 2.9.2 Remove Outliers
train.loc[train[col_name] < np.percentile(train[col_name],95)]
train.loc[train[col_name] > np.percentile(train[col_name],5)]
#### 2.9.3 Skip first n rows
df = pd.read_csv('file_name.csv',skiprows=10, header=None)
#### 2.9.4 Left merge with indicator
l = pd.DataFrame({"id": [1,2,3,4,5], "value": [10,20,30,40,50]})
r = pd.DataFrame({"id":[6,2,3,4,7], "value": [100,200, 300, 400, 5]})
pd.merge(l, r, how="outer", on="id", suffixes=("_left","_right"),indicator=True)
#### 2.9.5 Compress & Save Pandas Dataframe
df.to_csv("dataset.csv", index=False)
df.to_csv("dataset.gz", compression="gzip", index=False)
df = pd.read_csv("dataset.gz")

