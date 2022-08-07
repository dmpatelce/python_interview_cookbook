# Pandas ##############

```python
import pandas as pd
```

### Read the CSV File and set as Dataframe
```python
df = pd.read_csv('weather_data.csv')
```

### Read the Dictionary to read the Dataframe
```python
weather_data = {
    'day': ['1/1/2017','1/2/2017','1/3/2017','1/4/2017','1/5/2017','1/6/2017'],
    'temperature': [32,35,28,24,32,31],
    'windspeed': [6,7,2,7,4,2],
    'event': ['Rain', 'Sunny', 'Snow','Snow','Rain', '']
}
# Note: Array must be all in same length. otherwise "ValueError: arrays must all be same length"
df = pd.DataFrame(weather_data) # same output as read_csv method
print(df)
```

### Print length of Rows and Columns
```python
df.shape # (6, 4)
rows, columns = df.shape
print("Rows: ", rows, "Columns:", columns)
```

### Print only some of the rows of the large CSV
```python
df.head() # Print first 5 rows
df.head(2) # Print only 2 initial rows

df.tail() # Print last 5 rows
df.tail(2) # Print last 2 bottom rows

df[2:5] # Print rows starting from 2 and ending with 5 (i.e. 2, 3, 4)
```

### Print columns
```python
df.columns # Print columns 
df.columns # Index(['day', 'temperature', 'windspeed', 'event'], dtype='object')
list(df.columns) # ['day', 'temperature', 'windspeed', 'event']
df.day
# 0    1/1/2017
# 1    1/2/2017
# 2    1/3/2017
# 3    1/4/2017
# 4    1/5/2017
# 5    1/6/2017
df['event']
# 0    Rain
# 1    Sunny
# 2    Snow
# 3    Snow
# 4    Rain
# 5     

# Print only some of the columns
df[['day', 'event']]
#    day        event
# 0  1/1/2017   Rain
# 1  1/2/2017   Sunny
# 2  1/3/2017   Snow
# 3  1/4/2017   Snow
# 4  1/5/2017   Rain
# 5  1/6/2017   
```

### Series 
A Pandas Series is like a column in a table. It is a one-dimensional array holding data of any type.
```python
type(df.event) # <class 'pandas.core.series.Series'>
```

### Operations
Reference : https://pandas.pydata.org/docs/reference/api/pandas.Series.html

```python
df['temperature'].max() # 35
df['temperature'].min() # 24
df[df['temperature']>32]

#       day     temperature     windspeed   event
#   1   1/2/2017        35      7           Sunny

df['day'][df['temperature'] == df['temperature'].max()] # Kinda doing SQL in pandas
# 1    1/2/2017
# Name: day, dtype: object

df[df['temperature'] == df['temperature'].max()] # Kinda doing SQL in pandas
        # day  temperature  windspeed  event
# 1  1/2/2017           35          7  Sunny

df.describe() # List all the statastics of the Numeric columns
#        temperature  windspeed
# count     6.000000   6.000000
# mean     30.333333   4.666667
# std       3.829708   2.338090
# min      24.000000   2.000000
# 25%      28.750000   2.500000
# 50%      31.500000   5.000000
# 75%      32.000000   6.750000
# max      35.000000   7.000000
```

### set_index: this is used to set the specific column as an index instead of the counter

```python
df.set_index('day')
#           temperature  windspeed  event
# day                                    
# 1/1/2017           32          6   Rain
# 1/2/2017           35          7  Sunny
# 1/3/2017           28          2   Snow
# 1/4/2017           24          7   Snow
# 1/5/2017           32          4   Rain
# 1/6/2017           31          2       

df.set_index('day', inplace=True) # inplace is used to overwrite the original element and replace it
df.index # Index(['1/1/2017', '1/2/2017', '1/3/2017', '1/4/2017', '1/5/2017', '1/6/2017'], dtype='object', name='day')
df.loc['1/2/2017'] # The loc operator is used to index a portion of the dataframe.
# temperature       35
# windspeed          7
# event          Sunny
# Name: 1/2/2017, dtype: object
df.reset_index(inplace=True) # reset the index and make it normal DataFrame with counter as index
df.set_index('event',inplace=True) # this is kind of building a hash map using event as a key
df.loc['Snow']

#           day	    temperature   windspeed
# event 
# Snow      1/3/2017    28          2
# Snow      1/4/2017    24          7
```
