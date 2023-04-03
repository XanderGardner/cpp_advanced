# Table of Contents
- [Main](#README.md)
- [Webscraping](#webscraping.md)

[Data Structures Built-in](#data-structures-built-in)
1. [list](#list)
1. [tuple](#tuple)
1. [set](#set)
1. [frozenset](#frozenset)
1. [str](#str)
1. [dict](#dict)
1. [bytearray](#bytearray)

[Data Structures to Import](#data-structures-to-import)
1. [queue](#queue)
1. [deque](#deque)
1. [heapq](#heapq)
1. [SortedList](#sortedlist)
1. [defaultdict](#defaultdict)
1. [Counter](#counter)

[Data Structures to Implement](#data-structures-to-implement)
1. [stack](#stack)
1. [linkedlist](#linkedlist)
1. [graph](#graph)

[Algorithms](#algorithms)
1. [Bit Operations](#bit-operations)
1. [DFS](#dfs)
1. [BFS](#bfs)
1. [Dynamic Programming](#dynamic-programming)
1. [Searching](#searching)
1. [Sorting](#sorting)

[Techniques](#techniques)
1. [Nested Functions](#nested-functions)
1. [Enumerate](#enumerate)
1. [Comparing Objects](#comparing-objects)
1. [Map Function](#map-function)
1. [Filter Function](#filter-function)
1. [Zip Function](#zip-function)

[pandas](#pandas)
1. [create](#create)
1. [output](#output)
1. [read](#read)
1. [update](#update)

[numpy](#numpy)

[plt](#plt)

[conda](#conda)

[TODO](#todo)

# Data Structures Built-in

### list
- indexed collection of data
- inset/deleting at front requires shifting
- can use as a stack
``` python
a = [1,2]
a += [3]
a.index(2) # returns index of first instance of the value 2
a.remove(2) # removes first instance of the value 2
a.pop(1) # removes index (or last if not specified)
a.count(2) # counts number of 2s in the list
```
### tuple
- immutable list
``` python
a = (1,3,2)
b = (1,)
c = tuple(list1)
a[1]
```

### set
- uses hash table w/ linked list
``` python
a = set([2,1,3])
print(1 in set)
a.add(4)
a.remove(4)
```

### frozenset
- immutable set
``` python
a = frozenset([1,2,3])
```

### str
- immutable array of bytes (modifying creates a new string)
- represents unicode characters
``` python
a = "hel'
a[2]
a += "lo"
print("o" in a)
```

### dict
- collection of key-value pairs
- advanced version of hash table
``` python
a = {"a":2, "h":5}
a["b"] = 3
print("a" in a)
a["a"]
del a["a"] # or a.pop("a") which also gets item

a.keys() # returns iterable
a.values() # returns iterable
for key, value in a.items():
```

### bytearray
- sequence of integers
- integers are byte size: 0 <= x <= 255
``` python
a = bytearray((23,4,3))
b = bytearray((3,))
a[2] # returns integer
a.append(30)
```

# Data Structures to Import

### queue
- FIFO (oldest out)
``` python
from queue import Queue
a = Queue()
a.put(1)
a.get()
```

### deque
- remove either end in O(1)
``` python
from collections import deque
a = deque()
a.append(1) # appends right
a.popleft()
a.pop() # pops right
```

### heapq
- algorithm when used with list to make a priority queue
- this is a min-heap. to use a max-heap easily, make vals negative
``` python
import heapq
a = [1,3,4,5]
heapq.heapify(a)
heapq.heappush(a, 6)
heapq.heappop(a)
```
- use tuples to sort based on index 0
``` python
a = [(1, "a"), (5, "d")]
heapq.heapify(a)
```

### SortedList
- maintains a sorted list
- nlogn creation
- logn adding and removing
``` python
from sortedcontainers import SortedList
a = SortedList([1, 5, 4])
a.add(2)
a.remove(5) # a.discard(5) for not throwing error if not present
a.pop(2) # default will pop -1 (last element)

a.bisect_left(5) # gets index of where you would insert 5
# [1,3,5,5,6] bisect_left is 2, bisect_right is 4 based on same elements present
a.count(5)
a.index(5)
```

### defaultdict
- dict but accessing unknown key creates the key with a default value instead of erroring
```
from collections import defaultdict

a = defaultdict(lambda: 1)
a["d"] += 1 # a["d"] is now 2
```

### Counter
- dict where values are the counted number of times the key appears
```
from collections import Counter
a = Counter("hello")
# {"h":1, "e":1, "l":2, "o":1"}
```
```
# useful trick
a = Counter([1, 3, 4, 1, 2, 1, 1, 3, 4, 3, 5, 1, 2, 5, 3, 4, 5])
b = counter.most_common(3) # [(1, 5), (3, 4), (4, 3)]
```


# Data Structures to Implement

### stack
- just use a list
``` python
a = []
a += [1]
a.pop()
```
### linkedlist
- make a simple Node class
``` python
class Node:
  def __init__(self, val):
    self.val = val
    self.next = None
```
``` python
root = Node(2)
```

### graph
- use dict to act as an adjacency list
``` python
a = {
  '5' : ['3','7'],
  '3' : ['2', '4'],
  '7' : ['8'],
  '2' : [],
  '4' : ['8'],
  '8' : []
}
```

# Algorithms

### Bit Operations
- TODO

### DFS
- for trees (recursive)
``` python
def preorder(root):
  return [root.val] + preorder(root.left) + preorder(root.right) if root else []
def inorder(root):
  return  inorder(root.left) + [root.val] + inorder(root.right) if root else []
def postorder(root):
  return  postorder(root.left) + postorder(root.right) + [root.val] if root else []
```
- for graphs, must track visited bc of cycles (recursive)
``` python
def dfs(graph, visited, node):  #function for dfs 
    if node not in visited:
        print(node)
        visited.add(node)
        for neighbour in graph[node]:
            dfs(visited, graph, neighbour)
```
``` python
graph = {
  '5' : ['3','7'],
  '3' : ['2', '4'],
  '7' : ['8'],
  '2' : [],
  '4' : ['8'],
  '8' : []
}
visited = set() # Set to keep track of visited nodes of graph (bc of graph cycles)
dfs(graph, visited, '5')
```

### BFS
- for graphs, must track visited bc of cycles (uses queue)
- starts from a certain node, s (all nodes labeled 0, 1...)
``` python
def BFS(self, s):
  visited = [False] * (len(self.graph))
  queue = []

  # start at source
  queue.append(s)
  visited[s] = True

  while queue:
    s = queue.pop(0)
    print (s, end = " ")

    # go through neighbors
    for i in self.graph[s]:
      if visited[i] == False:
        queue.append(i)
        visited[i] = True
```

### Dynamic Programming

- recursion with memoization
``` python
memo = {}
def factorial(n):
  if n == 1:
    return 1
  elif n >= 2:
    mem[n] = n * factorial(n-1)
    return memo[n]
```

### Searching
- linear search: check left to right
- binary search: recursive on sorted array
``` python
import bisect
def search(self, nums, target):
  index = bisect.bisect_left(nums, target)
  return index if index < len(nums) and nums[index] == target else -1
```
``` python 
# returns index of x in arr if present, else -1
def binary_search(arr, low, high, x):
    if high < low:
      return -1 # element not present
    
    mid = (high + low) // 2
    if arr[mid] == x:
        return mid
    elif arr[mid] > x:
        return binary_search(arr, low, mid - 1, x)
    else:
        return binary_search(arr, mid + 1, high, x)
```

### Sorting
- Selection: repeatedly find smallest w/ linear search
- Insertion: move next element into left part that is sorted
- Merge: recursive breakdown and then merge lists back up
- Quick: partition about element, recurse on left and right sides
- Python uses Tim (combo of insertion and merge)

``` python
def sortCmp(e):
  return len(e)
  
a = ['ab', 'a', 'df', 'sdf']

# sort mutates (default ascending (False))
a.sort()
a.sort(reverse=True, key=sortCmp)

# sorted doesn't mutate (default ascending (False))
b = sorted(a)
b = sorted(a, key=sortCmp, reverse=True)
```

# Techniques

### Nested Functions
- not as readable, but less memory (since not referencing the class)
``` python
class Solution:
  def do(self):
    def helper():
      return
    return helper

# instead of helper functions...

class Solution:
  def helper(self):
    return
  def do(self):
    return self.helper
```

### Enumerate
- simplifies loops needing value and index
``` python
for index, value in enumerate(values):
```

### Comparing Objects
- just define this function
``` python
def __lt__(self, other):
  return self.intAttribute < other.intAttribute
```

### Map Function
- given function and iterable, returns iterable (map object) with all items run through the function
```
def squ(n):
  return n ** 2
map(squ, [1,3,2]) # [1,9,4]
```

### Filter Function
- given function (that returns a boolean) and iterable, returns iterable (filter object) with only items that cause the given function to return True
```
def odd(n):
  return bool(n%2)
filter(odd, [1,2,3,4]) # [1,3]
```

### Zip Function
- given any number of iterables of equal length, returns iterable (zip object) of tuples (grouping items of the same index)
```
zip([1,2,3],[4,5,6],[7,8,9]) # [(1,4,7),(2,5,8),(3,6,9)]
```

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

# conda
Create different environments which hold different packages. The "base" environment has everything

- To create an environment, in terminal:
```
conda create --name env_name
```
set python version
```
conda install python=3.5.0
```

- To enter environment
```
conda activate env_name
```

- To see list of environment names
```
conda env list
```

- To see list of packages in current environment
```
conda list
```

- To install package in current environment
```
conda install pandas
```

# TODO
- bitoperations
- https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/
