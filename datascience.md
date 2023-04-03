# Table of Contents
- [Main](README.md)
- [Webscraping](webscraping.md)
- [Data Science](datascience.md)

[pandas](#pandas)
1. [create](#create)
1. [output](#output)
1. [read](#read)
1. [update](#update)

[numpy](#numpy)

[plt](#plt)


# pandas

- import
``` python
import pandas as pd
```
### create
- dataframe
- main structure for holding data in a table
``` python
df = pd.read_csv('data.csv') # read from csv
df = pd.DataFrame.from_dict(dict) # read from dict (keys are col names)

# or read from sqlite3
import sqlite3
con = sqlite3.connect("ssdfd.sqlite")
df = pd.read_sql_query("SELECT * FROM tablename", con)
```
### output

- plotting
```
df.plot.line('TIME', "SIZE") # line
df['colname'].hist() # histogram
plt.scatter(x=df['col1'], y=df['col2'], alpha=0.1) # density plot
```
setting title, xlabel with axes
```
ax = df['colname'].hist()
ax.set_xlabel("xlabel")
ax.set_title("title")
```

- get dict
``` python
df.to_dict('index')
# {'row1': {'col1': 1, 'col2': 0.5}, 'row2': {'col1': 2, 'col2': 0.75}}
```

- get numpy array (if all numbers)
- otherwise numpy array will have some objects and stuff
``` python
a = df.to_numpy()
```

- get column as list
``` python
a['colname'].tolist()
```


### read

- metadata
``` python
df.columns # array of col names (can set these)
df.index # array of row names (can set these)
df.dtypes # array of data types
```

- access
``` python
df['colname'] # one col
df[['colname1', 'colname2']] # multiple cols
```

- conditional access
``` python
df[df['longitude'] == -119.7]
df[(df['longitude'] == -119.7) & (df['longitude'] == -119.7)]
```

- specific access
``` python
df.iloc[14] # get row
df.iloc[14,1] # get row, col
df.iloc[22:25] # multiple rows
```

### update

- adding data
``` python
df['New Column'] = df['latitude'] + df['longitude']
df['new col'] = df['longitude'].apply(lambda x : 1 if x==-122.05 else 0)
```

- sort rows by a columns values
```
df = df.sort_values(by=['TIME'])
```

# plt

- import
``` python
import matplotlib.pyplot as plt
```

- plotting
- `plot` or `scatter`
``` python
plt.plot(alphas, num_occurances, label="num occurances")
plt.plot(alphas, mean_returns, label="mean returns")
plt.plot(alphas, total_returns, label="total returns")
plt.plot(alphas, variance_returns, label="variance returns")
plt.legend()
plt.title("metrics vs alpha")
plt.xlabel("alpha")
plt.ylabel("metric")
```


# numpy
- uses numpy `import numpy as np`
```
a = np.array([2,3])
```
