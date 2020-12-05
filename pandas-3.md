# Learning Data Analysis with Python - Pandas DataFrame and Basic Operations
> ⚠️ **Note** - _This post is a part of Learning data analysis with python series. If you haven't read the first post, some of the content won't make sense. Check it out <a href='https://bytetales.co/learning-data-analysis-with-python-introduction-to-pandas'>here</a>._


```python
d = {
    'col1' : pd.Series([1,2,3], index = ["row1", "row2", "row3"]),
    'col2' : pd.Series([4,5,6], index = ["row1", "row2", "row3"])
}

df = pd.DataFrame(d)
```

```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row1</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>row3</th>
      <td>3</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



As shown in above code, the keys of dict of Series becomes column names of the DataFrame and the index of the Series becomes the row name and all the data gets mapped by the row name i.e.,order of the index in the Series doesn't matter.

## DataFrame using ndarrays/lists

```python
d = {
    'one' : [1.,2.,3.],
    'two' : [4.,5.,6.]
}

df = pd.DataFrame(d)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>



As shown in the above code, when we use ndarrays/lists, if we don't pass the index then the `range(n)` becomes the index of the DataFrame.And while using the ndarray to create a DataFrame, the length of these arrays must be same and if we pass an explicit index then the length of this index must also be of same length as the length of the arrays.

## DataFrame using list of dictionaries

```python
d = [
    {'one': 1, 'two' : 2, 'three': 3},
    {'one': 10, 'two': 20, 'three': 30, 'four': 40}
]

df = pd.DataFrame(d)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>



We can also provide an explicit index in this method,too.

```python
df = pd.DataFrame(d, index=["first", "second"])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>first</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>second</th>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>



Although learning to create a DataFrame object using these methods is necessary but in real world, we won't be using these methods to create a DataFrame but we'll be using external data files to load data and manipulate that data. So, let's take a look how to load a csv file and create a DataFrame.In the previous post, we worked with the Nifty50 data to demonstrate how Series works and similarly in this post, we'll load Nifty50 2018 data, but in addition to just Close values of each date, in this dataset we have Open, High and Low value of Nifty50. First let's see what this dataset looks like and then we'll load it into a DataFrame.

![Nifty50 Data](https://res-console.cloudinary.com/bytetales/thumbnails/transform/v1/image/upload//v1599051299/bmlmdHlfNTA=/drilldown)

```python
df = pd.read_csv('NIFTY50_2018.csv')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>31 Dec 2018</td>
      <td>10913.20</td>
      <td>10923.55</td>
      <td>10853.20</td>
      <td>10862.55</td>
    </tr>
    <tr>
      <th>1</th>
      <td>28 Dec 2018</td>
      <td>10820.95</td>
      <td>10893.60</td>
      <td>10817.15</td>
      <td>10859.90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27 Dec 2018</td>
      <td>10817.90</td>
      <td>10834.20</td>
      <td>10764.45</td>
      <td>10779.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>26 Dec 2018</td>
      <td>10635.45</td>
      <td>10747.50</td>
      <td>10534.55</td>
      <td>10729.85</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24 Dec 2018</td>
      <td>10780.90</td>
      <td>10782.30</td>
      <td>10649.25</td>
      <td>10663.50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>241</th>
      <td>05 Jan 2018</td>
      <td>10534.25</td>
      <td>10566.10</td>
      <td>10520.10</td>
      <td>10558.85</td>
    </tr>
    <tr>
      <th>242</th>
      <td>04 Jan 2018</td>
      <td>10469.40</td>
      <td>10513.00</td>
      <td>10441.45</td>
      <td>10504.80</td>
    </tr>
    <tr>
      <th>243</th>
      <td>03 Jan 2018</td>
      <td>10482.65</td>
      <td>10503.60</td>
      <td>10429.55</td>
      <td>10443.20</td>
    </tr>
    <tr>
      <th>244</th>
      <td>02 Jan 2018</td>
      <td>10477.55</td>
      <td>10495.20</td>
      <td>10404.65</td>
      <td>10442.20</td>
    </tr>
    <tr>
      <th>245</th>
      <td>01 Jan 2018</td>
      <td>10531.70</td>
      <td>10537.85</td>
      <td>10423.10</td>
      <td>10435.55</td>
    </tr>
  </tbody>
</table>
<p>246 rows × 5 columns</p>
</div>



We have loaded the data and created a dataframe from it, but we may want to take the `Date` column as the index and as always, Pandas provide a simple way to do this and many more things that you may want to do with the data. we can make any column as the index column by providing the `index_col` parameter in the `read_csv` method. Let's see what our dataframe looks like after that.

```python
df = pd.read_csv('NIFTY50_2018.csv', index_col=0)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>31 Dec 2018</th>
      <td>10913.20</td>
      <td>10923.55</td>
      <td>10853.20</td>
      <td>10862.55</td>
    </tr>
    <tr>
      <th>28 Dec 2018</th>
      <td>10820.95</td>
      <td>10893.60</td>
      <td>10817.15</td>
      <td>10859.90</td>
    </tr>
    <tr>
      <th>27 Dec 2018</th>
      <td>10817.90</td>
      <td>10834.20</td>
      <td>10764.45</td>
      <td>10779.80</td>
    </tr>
    <tr>
      <th>26 Dec 2018</th>
      <td>10635.45</td>
      <td>10747.50</td>
      <td>10534.55</td>
      <td>10729.85</td>
    </tr>
    <tr>
      <th>24 Dec 2018</th>
      <td>10780.90</td>
      <td>10782.30</td>
      <td>10649.25</td>
      <td>10663.50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>05 Jan 2018</th>
      <td>10534.25</td>
      <td>10566.10</td>
      <td>10520.10</td>
      <td>10558.85</td>
    </tr>
    <tr>
      <th>04 Jan 2018</th>
      <td>10469.40</td>
      <td>10513.00</td>
      <td>10441.45</td>
      <td>10504.80</td>
    </tr>
    <tr>
      <th>03 Jan 2018</th>
      <td>10482.65</td>
      <td>10503.60</td>
      <td>10429.55</td>
      <td>10443.20</td>
    </tr>
    <tr>
      <th>02 Jan 2018</th>
      <td>10477.55</td>
      <td>10495.20</td>
      <td>10404.65</td>
      <td>10442.20</td>
    </tr>
    <tr>
      <th>01 Jan 2018</th>
      <td>10531.70</td>
      <td>10537.85</td>
      <td>10423.10</td>
      <td>10435.55</td>
    </tr>
  </tbody>
</table>
<p>246 rows × 4 columns</p>
</div>



There are many more parameters available in the `read_csv` method such as `usecols` using which we can deliberately ask the pandas to only load provided columns, `na_values` to provide explicit values that pandas should identify as null values and so on and so forth. Read more about all the parameters in pandas [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html).

Now, let's look at some of the basic operations that we can perform on the dataframe object in order to learn more about our data.

```python
# Shape (Number of rows and columns) of the DataFrame
df.shape
```




    (246, 4)



```python
# List of index
df.index
```




    Index(['31 Dec 2018', '28 Dec 2018', '27 Dec 2018', '26 Dec 2018',
           '24 Dec 2018', '21 Dec 2018', '20 Dec 2018', '19 Dec 2018',
           '18 Dec 2018', '17 Dec 2018',
           ...
           '12 Jan 2018', '11 Jan 2018', '10 Jan 2018', '09 Jan 2018',
           '08 Jan 2018', '05 Jan 2018', '04 Jan 2018', '03 Jan 2018',
           '02 Jan 2018', '01 Jan 2018'],
          dtype='object', name='Date', length=246)



```python
# List of column names
df.columns
```




    Index(['Open', 'High', 'Low', 'Close'], dtype='object')



```python
# Check if a DataFrame is empty or not
df.empty
```




    False



It's very crucial to know data types of all the columns because sometimes due to corrupt data or missing data, pandas may identify numeric data as 'object' data-type which isn't desired as numeric operations on the 'object' type of data is costlier in terms of time than on `float64` or `int64` i.e numeric datatypes.

```python
# Datatypes of all the columns
df.dtypes
```




    Open     float64
    High     float64
    Low      float64
    Close    float64
    dtype: object



We can use iloc and loc to index and get the particular data from our dataframe.

```python
# Indexing using implicit index
df.iloc[0]
```




    Open     10913.20
    High     10923.55
    Low      10853.20
    Close    10862.55
    Name: 31 Dec 2018, dtype: float64



```python
# Indexing using explicit index
df.loc["01 Jan 2018"]
```




    Open     10531.70
    High     10537.85
    Low      10423.10
    Close    10435.55
    Name: 01 Jan 2018, dtype: float64



We can also use both row and column to index and get specific cell from our dataframe.

```python
# Indexing using both the axes(rows and columns)
df.loc["01 Jan 2018", "High"]
```




    10537.85



We can also perform all the math operations on a dataframe object same as we did on series.

```python
# Add 10 to all the values
df.add(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>31 Dec 2018</th>
      <td>10923.20</td>
      <td>10933.55</td>
      <td>10863.20</td>
      <td>10872.55</td>
    </tr>
    <tr>
      <th>28 Dec 2018</th>
      <td>10830.95</td>
      <td>10903.60</td>
      <td>10827.15</td>
      <td>10869.90</td>
    </tr>
    <tr>
      <th>27 Dec 2018</th>
      <td>10827.90</td>
      <td>10844.20</td>
      <td>10774.45</td>
      <td>10789.80</td>
    </tr>
    <tr>
      <th>26 Dec 2018</th>
      <td>10645.45</td>
      <td>10757.50</td>
      <td>10544.55</td>
      <td>10739.85</td>
    </tr>
    <tr>
      <th>24 Dec 2018</th>
      <td>10790.90</td>
      <td>10792.30</td>
      <td>10659.25</td>
      <td>10673.50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>05 Jan 2018</th>
      <td>10544.25</td>
      <td>10576.10</td>
      <td>10530.10</td>
      <td>10568.85</td>
    </tr>
    <tr>
      <th>04 Jan 2018</th>
      <td>10479.40</td>
      <td>10523.00</td>
      <td>10451.45</td>
      <td>10514.80</td>
    </tr>
    <tr>
      <th>03 Jan 2018</th>
      <td>10492.65</td>
      <td>10513.60</td>
      <td>10439.55</td>
      <td>10453.20</td>
    </tr>
    <tr>
      <th>02 Jan 2018</th>
      <td>10487.55</td>
      <td>10505.20</td>
      <td>10414.65</td>
      <td>10452.20</td>
    </tr>
    <tr>
      <th>01 Jan 2018</th>
      <td>10541.70</td>
      <td>10547.85</td>
      <td>10433.10</td>
      <td>10445.55</td>
    </tr>
  </tbody>
</table>
<p>246 rows × 4 columns</p>
</div>



We can also aggregate the data using the `agg` method. For instance, we can get the maximum and minimum values from all the columns in our data using this method as show below.

```python
df.agg(["max", "min"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>max</th>
      <td>11751.8</td>
      <td>11760.2</td>
      <td>11710.5</td>
      <td>11738.50</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9968.8</td>
      <td>10027.7</td>
      <td>9951.9</td>
      <td>9998.05</td>
    </tr>
  </tbody>
</table>
</div>



However, pandas provide a more convenient method to get a lot more than just minimum and maximum values across all the columns in our data. And that method is `describe`. As the name suggests, it describes our dataframe by applying mathematical and statistical operations across all the columns.

```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>246.000000</td>
      <td>246.000000</td>
      <td>246.000000</td>
      <td>246.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>10758.260366</td>
      <td>10801.753252</td>
      <td>10695.351423</td>
      <td>10749.392276</td>
    </tr>
    <tr>
      <th>std</th>
      <td>388.216617</td>
      <td>379.159873</td>
      <td>387.680138</td>
      <td>382.632569</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9968.800000</td>
      <td>10027.700000</td>
      <td>9951.900000</td>
      <td>9998.050000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>10515.125000</td>
      <td>10558.650000</td>
      <td>10442.687500</td>
      <td>10498.912500</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>10704.100000</td>
      <td>10749.850000</td>
      <td>10638.100000</td>
      <td>10693.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>10943.100000</td>
      <td>10988.075000</td>
      <td>10878.262500</td>
      <td>10950.850000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>11751.800000</td>
      <td>11760.200000</td>
      <td>11710.500000</td>
      <td>11738.500000</td>
    </tr>
  </tbody>
</table>
</div>



And to get the name, data types and number of non-null values in each columns, pandas provide `info` method.

```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 246 entries, 31 Dec 2018 to 01 Jan 2018
    Data columns (total 4 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   Open    246 non-null    float64
     1   High    246 non-null    float64
     2   Low     246 non-null    float64
     3   Close   246 non-null    float64
    dtypes: float64(4)
    memory usage: 19.6+ KB


We are working with a small data with less than 300 rows and thus, we can work with all the rows but when we have tens or hundreds of thousand rows in our data, it's very difficult to work with such huge number of data. In statistics, 'sampling' is a technique that solves this problem. Sampling means to choose a small amount of data from the whole dataset such that the sampling dataset contains somewhat similar features in terms of diversity as that of the whole dataset. Now, it's almost impossible to manually select such peculiar rows but as always, pandas comes to our rescue with the `sample` method.

```python
df.sample(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18 Jul 2018</th>
      <td>11060.20</td>
      <td>11076.20</td>
      <td>10956.30</td>
      <td>10980.45</td>
    </tr>
    <tr>
      <th>29 Aug 2018</th>
      <td>11744.95</td>
      <td>11753.20</td>
      <td>11678.85</td>
      <td>11691.90</td>
    </tr>
    <tr>
      <th>25 Oct 2018</th>
      <td>10135.05</td>
      <td>10166.60</td>
      <td>10079.30</td>
      <td>10124.90</td>
    </tr>
    <tr>
      <th>06 Aug 2018</th>
      <td>11401.50</td>
      <td>11427.65</td>
      <td>11370.60</td>
      <td>11387.10</td>
    </tr>
    <tr>
      <th>14 Feb 2018</th>
      <td>10585.75</td>
      <td>10590.55</td>
      <td>10456.65</td>
      <td>10500.90</td>
    </tr>
  </tbody>
</table>
</div>



But, executing this method produces different results everytime and that may be unacceptable in some cases. But that can be solved by providing `random_state` parameter in the `sample` method to reproduce same result everytime.

As shown above, we can perform many operations on the DataFrame object to get information of the DataFrame and from the DataFrame. These are just basic operations that we can perform on the DataFrame object, there are many more interesting methods and operations that we can perform on the DataFrame object such as `pivot` , `merge` , `join` and many more. Also, in this given dataset, we have time as the index of our DataFrame i.e this is the TimeSeries dataset and pandas also provide many methods to manipulate the TimeSeries data such as `rolling_window`.

That will be all for this post. In the next post we'll look at some of these methods and we'll perform 5 analysis tasks using these methods. Till then, you can take a look at the [pandas documentation](https://pandas.pydata.org/pandas-docs/stable/index.html) and find more information about DataFrame objects and the methods that can be applied on the DataFrame object.

**Thank you for reading**
