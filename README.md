# *Python Cheat Sheet*

## Table of Contents
[Data Structures Built-in](#data-structures-built-in)
1. [list](#list)
1. [tuple](#tuple)
1. [set](#set)
1. [frozenset](#frozenset)
1. [str](#str)
1. [dict](#dict)
1. [numpy.ndarray](#numpy.ndarray)
1. [bytearray](#bytearray)

[Data Structures to Import](#data-structures-to-import)
1. [queue](#queue)
1. [deque](#deque)
1. [heapq](#heapq)

[Data Structures to Implement](#data-structures-to-implement)
1. [stack](#stack)
1. [linkedlist](#linkedlist)
1. [graph](#graph)

[Algorithms](#algorithms)
1. [DFS](#dfs)
1. [BFS](#bfs)
1. [Dynamic Programming](#dynamic-programming)
1. [Searching](#searching)
1. [Sorting](#sorting)

[Techniques](#techniques)

## Data Structures Built-in

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
```

### numpy.ndarray
- uses numpy `import numpy as np`
```
a = np.array([2,3])
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

## Data Structures to Import

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

## Data Structures to Implement

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

## Algorithms

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

## Techniques

### nested functions over helper functions
- not as readable, but less memory (since not referencing the class)
``` python
class Solution:
  def do(self):
    def helper():
      return
    return helper

# instead of...

class Solution:
  def helper(self):
    return
  def do(self):
    return self.helper
```

### enumerate
- simplifies loops needing value and index
``` python
for index, value in enumerate(values):
```

### comparing objects
- just define this function
``` python
def __lt__(self, other):
  return self.intAttribute < other.intAttribute
```

### TODO: Add Info
- https://dev.to/codespent/understanding-map-filter-and-zip-in-python-3ifn
