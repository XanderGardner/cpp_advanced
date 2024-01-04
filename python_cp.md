# Python for Competitive Programming

Basics
- [read input](#read-input)
- [throw errors](#throw-errors)
- [random](#random)

Basic Data Types
- [int](#int)
- [char](#char)
- [str](#str)

Collections
- [list](#list)
- [tuple](#tuple)
- [bytearray](#bytearray)
- [stack](#stack)
- [queue](#queue)
- [deque](#deque)

Ordered Collection
- [heapq (priority queue)](#heapq)
- [SortedList](#sortedlist)

Set
- [set](#set)
- [frozenset](#frozenset)

Maps
- [dict](#dict)
- [defaultdict](#defaultdict)
- [OrderedDict](#ordereddict)
- [Counter](#counter)

Node Based
- [linkedlist](#linkedlist)
- [tree](#tree)
  - [binary search tree](#binary-search-tree)
  - [DFS](#tree-dfs)
  - [BFS](#tree-bfs)
- [graph](#graph)
  - [DFS](#graph-dfs)
  - [BFS](#graph-bfs)
  - [topological sort](#topological-sort)
  - [minimum spanning tree](#minimum-spanning-tree)

Range Queries
- [segment tree](#segment-tree)

Grouping
- [union-find](#union-find)

Strings
- [trie](#trie)
- [z-array](#z-array)

Algorithms
- [Searching](#searching)
- [Sorting](#sorting)
- [Dynamic Programming](#dynamic-programming)
  - [bitmasking](#bitmasking)

Python Techniques
- [Nested Functions](#nested-functions)
- [Enumerate](#enumerate)
- [Comparing Objects](#comparing-objects)
- [Map Function](#map-function)
- [Filter Function](#filter-function)
- [Zip Function](#zip-function)

Math
- [Operations](#operations)
- [Sum Sequence](#sum-sequence)
- [Combination](#combinations)

Other Guides
- [Time Complexity](#time-complexity)

------

# read input
- read from stdin
```python
import sys

def main():
  words = []

  # stdin.readline().strip().split("")
  for line in sys.stdin:
    words += line.strip().split(" ")
  print(words)

if __name__ == "__main__":
  main()
```

# throw errors
- assert
```python
assert(5==5)
```
- raise error
```python
raise ValueError("message") # for argument checking
raise RuntimeError("message")
```
- try catch
```python
try:
  result = a / b
  return result
except Exception as e:
  print("An error occurred:", e)
  return None
```

# random
- generate random numbers
```python
import random

x = random.randint(a, b) # random int between [a,b]
y = random.random() # random float between (0,1)
z = random.choice([1,3,4]) # random element from list
```

# int
- integer
```python
# max integer and min integer
import sys
maxint = sys.maxsize # sys.maxint for versions before python3
minint = -sys.maxsize-1
```

# char
- character
```python
# get ascii code of character
code = ord('A') 

# check if uppercase
'A'.isupper()

# check alpha numerical
'y'.isalnum()

# convert to lower or uppercase
'A'.lower()
'a'.upper()
```

# str
- immutable array of bytes (modifying creates a new string)
- represents unicode characters
``` python
a = "hel'
a[2]
a += "lo"
print("o" in a) # True

# remove all whitespace
s_new = "".join(s.split())

# replace characters
s_new = s.replace(" ", "")

# split based on character
s_new = s.split(",")

# check if is digit
"3".isdigit() # True
"453".isdigit() # True
```

# list
- indexed collection of data
- inset/deleting at front requires shifting
- can use as a stack
``` python
a = [1,2]
a = [[0] for _ in range(5)] # list of lists without self-referencing
a += [3]
a.index(2) # returns index of first instance of the value 2
a.remove(2) # removes first instance of the value 2
a.pop(1) # removes index (or last if not specified)
a.count(2) # counts number of 2s in the list
```
# tuple
- immutable list
``` python
a = (1,3,2)
b = (1,)
c = tuple(list1)
a[1]
```

# bytearray
- sequence of integers
- integers are byte size: 0 <= x <= 255
``` python
a = bytearray((23,4,3))
b = bytearray((3,))
a[2] # returns integer
a.append(30)
```

# stack
- just use a list
``` python
a = []
a += [1]
a.pop()
```

# queue
- FIFO (oldest out)
``` python
from queue import Queue
a = Queue()
a.put(1)
a.get()
a.qsize()
```

# deque
- remove either end in O(1)
- can be used as a linkedlist, stack, or queue
``` python
from collections import deque
a = deque()

# right end
a.append(1)
a.pop()

# left end
a.appendleft(1)
a.popleft()

# as a queue
a = deque()
a.append(3)
a.popleft()
```

# heapq
- algorithm when used with list to make a priority queue
- this is a min-heap. to use a max-heap easily, make vals negative
``` python
import heapq

# create
a = [1,3,4,5]
heapq.heapify(a)

# push
heapq.heappush(a, 6)

# pop
heapq.heappop(a)
```

- use tuples to sort based on index 0
``` python
a = [(1, "a"), (5, "d")]
heapq.heapify(a)
```

# SortedList
- maintains a sorted list
- nlogn creation
- logn adding and removing
- can usually use heapq array instead
``` python
from sortedcontainers import SortedList

# create
a = SortedList([1, 5, 4])

# add
a.add(2)

# remove
a.remove(5)
a.discard(5) # will not throw error if not present
a.pop(2) # default will pop -1 (last element is largest)

# get index
a.bisect_left(5) # gets index of where you would insert 5
a.count(5)
a.index(5)
```

# set
- uses hash table w/ linked list
``` python
a = set([2,1,3])
print(1 in set)
a.add(4)
a.remove(4)
```

# frozenset
- immutable set
``` python
a = frozenset([1,2,3])
```

# dict
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

# defaultdict
- dict but accessing unknown key creates the key with a default value instead of erroring
```
from collections import defaultdict

a = defaultdict(lambda: 1)
a["d"] += 1 # a["d"] is now 2
```

# OrderedDict
- keys ordered by when they were made
- if the value of a certain key is changed, the position of the key remains unchanged in OrderedDict
```python
from collections import OrderedDict

a = OrderedDict()
a[3] = "j" 

a.popitem() # pop the most recently addded item
a.popitem(last=False) # pop the oldest added item
```

# Counter
- dict where values are the counted number of times the key appears
```python
from collections import Counter
a = Counter("hello") # {"h":1, "e":1, "l":2, "o":1"}

a.most_common(2) # get top 2 most common [('l', 2), ('h', 1)]
```

# linkedlist
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

# tree
``` python
class Node:
  def __init__(self, val):
    self.val = val
    self.left = None
    self.right = None

  def solution(self):
    a = Node(5)
```

### binary search tree

``` python
class Node:
  def __init__(self, val):
    self.val = val
    self.left = None
    self.right = None

class BinarySearchTree:
  def __init__(self):
      self.root = None

  def insert(self, val):
    if self.root is None:
      self.root = Node(val)
    else:
      self.insert_rec(self.root, val)

  def insert_rec(self, curr, val):
    if val < curr.val:
      if curr.left is None:
        curr.left = Node(val)
      else:
        self.insert_rec(curr.left, val)
    else:
      if curr.right is None:
        curr.right = Node(val)
      else:
        self.insert_rec(curr.right, val)

  def search(self, val):
    return self.search_rec(self.root, val)

  def search_rec(self, curr, val):
    if curr is None or curr.val == val:
      return curr
    if val < curr.val:
      return self.search_rec(curr.left, val)
    else:
      return self.search_rec(curr.right, val)

class Solution:
  def test(self):
    # example
    bst = BinarySearchTree()
    bst.insert(5)
    bst.insert(2)
    print(bst.root.val)
    bst.search(2)
```   

### tree DFS
``` python
def preorder(root):
  return [root.val] + preorder(root.left) + preorder(root.right) if root else []
def inorder(root):
  return  inorder(root.left) + [root.val] + inorder(root.right) if root else []
def postorder(root):
  return  postorder(root.left) + postorder(root.right) + [root.val] if root else []
```

### tree BFS
- gets level order traversal
``` python
curr_row = [root]

while len(curr_row) > 0:
  next_row = []

  for node in curr_row:
    print(node.val) # process

    if node.left:
      next_row += [node.left]
    if node.right:
      next_row += [node.right]

  curr_row = next_row
```

# graph
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

### graph DFS
- for graphs, must track visited bc of cycles (recursive)
``` python
def dfs(graph, visited, node):
  if node not in visited:
    print(node)
    visited.add(node)
    for neighbour in graph[node]:
      dfs(visited, graph, neighbour)

visited = set() 
dfs(graph, visited, '5')
```

### graph BFS
- for graphs, must track visited bc of cycles (uses queue)
``` python
def BFS(s):
  visited = set()
  queue = []

  # start at source
  queue.append(s)
  visited.add(s)

  while queue:
    s = queue.pop(0)
    print(s) # process

    # go through neighbors
    for i in self.graph[s]:
      if i not in visited:
        queue.append(i)
        visited.add(i)
```

# topological sort
- used to order the vertices of a directed graph in such a way that for every directed edge (u, v), vertex u comes before vertex v in the ordering
- commonly used in tasks that involve dependency resolution, scheduling, and finding a valid sequence of steps or events
``` python
def topological_sort(graph):
  visited = set()
  stack = []
  
  def dfs(vertex):
    visited.add(vertex)
    for neighbor in graph[vertex]:
      if neighbor not in visited:
        dfs(neighbor)
    stack.append(vertex)
  
  for vertex in graph:
    if vertex not in visited:
      dfs(vertex)
  
  return stack[::-1]

graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}
result = topological_sort(graph)
print(result)  # Output: ['A', 'C', 'F', 'B', 'E', 'D']
```

# minimum spanning tree
- prim's algorithm:
- Initialize a tree with a single vertex, chosen arbitrarily from the graph.
- Grow the tree by one edge: Of the edges that connect the tree to vertices not yet in the tree, find the minimum-weight edge, and transfer it to the tree.
- Repeat step 2 (until n vertices are in the tree).

# segment tree
- usable update and query on ranges (can include max, min, sum, and more)
``` python
def update_st(self, st, i, new_val):
    n = int(len(st)/2)
    i += n
    st[i] = new_val
    i = int(i/2)
    while i >= 1:
        st[i] = max(st[2*i], st[2*i+1])
        i = int(i/2)

def query_st(self, st, i, j):
    n = int(len(st)/2)
    i += n
    j += n
    s = 0
    while i <= j:
        if (i%2 == 1):
            s = max(s, st[i])
            i += 1
        if (j%2 == 0):
            s = max(s, st[j])
            j -= 1
        i = int(i/2)
        j = int(j/2)
    return s

def create_st(self, a):
    n = pow(2,math.ceil(math.log2(len(a))))
    st = [0] * (n*2)

    for i in range(len(a)):
        self.update_st(st, i, a[i])
    return st

```

# union-find
- logn union and logn find
``` python
# create union find
link = list(range(n))
size = [1] * n # track size of groups

def find(x):
  if link[x] != x:
    link[x] = find(link[x])
  return link[x]

def union(x, y):
  root_x = find(x)
  root_y = find(y)

  if root_x == root_y:
      return

  if size[root_x] < size[root_y]:
      link[root_x] = root_y
      size[root_y] += size[root_x]
  else:
      link[root_y] = root_x
      size[root_x] += size[root_y]

union(0, 1) # union items 0 and 1
find(1) # find group for 1
find(1) == find(2) # check if itmes 1 and 2 are in the same group
```

# trie
- insert O(n), search O(n), and has_prefix O(n) for strings with alphabet
``` python
class TrieNode:
  def __init__(self):
    self.children = {}
    self.is_end_of_word = False

class Trie:
  def __init__(self):
    self.root = TrieNode()

  def insert(self, word):
    current = self.root
    for char in word:
      if char not in current.children:
        current.children[char] = TrieNode()
      current = current.children[char]
    current.is_end_of_word = True

  def search(self, word):
    current = self.root
    for char in word:
      if char not in current.children:
        return False
      current = current.children[char]
    return current.is_end_of_word

  def starts_with(self, prefix):
    current = self.root
    for char in prefix:
      if char not in current.children:
        return False
      current = current.children[char]
    return True

trie = Trie()
trie.insert("apple")
trie.search("apple")
trie.starts_with("app")
```

# z-array
- In O(n) computes for each index, the length of the longest substring of s that begins at position k and is a prefix of s.
- [A,C,B,A,C] -> [-,0,0,2,0]
- Find where string a occurs in string b by making new string s=a#b where # is a character never found in either string. Find z-array of s and count numbers with length of a.

```python
def get_z(s):
  n = len(s)
  z = [0] * n
  x, y = 0, 0

  for i in range(1, n):
    z[i] = max(0, min(z[i - x], y - i + 1))
    while i + z[i] < n and s[z[i]] == s[i + z[i]]:
      x = i
      y = i + z[i]
      z[i] += 1
  return z
```

# Searching
- linear search: check left to right
- binary search: recursive on sorted array
``` python
import bisect

# [1,3,5,5,6] bisect_left is 2, bisect_right is 4 based on same elements present

def search(self, nums, target):
  index = bisect.bisect_left(nums, target)
  return index if index < len(nums) and nums[index] == target else -1
```

- implement binary search
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

# Sorting
- Selection: repeatedly find smallest w/ linear search
- Insertion: move next element into left part that is sorted
- Merge: recursive breakdown and then merge lists back up
- Quick: partition about element, recurse on left and right sides
- Python uses Tim (combo of insertion and merge)

``` python
def sortCmp(e):
  return len(e)
  
a = ['ab', 'a', 'df', 'sdf']

# a.sort()
a.sort()
a.sort(reverse=True, key=sortCmp)

# sorted(a) doesn't mutate
b = sorted(a)
b = sorted(a, key=sortCmp, reverse=True)
```

# Dynamic Programming

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

- dp with cache
- each call has an accossiated state (usually position and other) which is memoized with cache
- each state has a list of actions you can do
- return the best result from each action that can be done
``` python
@cache
def dp(i, owned_state):
  # base case
  if i == n:
    return 0

  # recursive case
  # state: position, if owns stock
  # action: buy, hold, sell
  if owned_state:
    # hold or sell
    return max(
      dp(i+1, True),
      dp(i+1, False)+prices[i]
    )
  else:
    # hold or buy
    return max(
      dp(i+1, False),
      dp(i+1, True)-prices[i]-fee
    )

return dp(0, False)
```

### bitmasking
- 0 is false, numbers are true. Bits can be manipulated to work with subsets
```python
# basics
a & 1   # true if odd
a << 5  # left shift 5,  (multiply by 2^5)
a >> 5  # shift right 5, (divide by 2^5 rounded down)

x & (1 << k)  # true if kth bit of x set
x | (1 << k)  # set kth bit of x to 1
x & ~(1 << k) # set kth bit of x to 0
x ^ (1 << k)  # invert kth bit of x

a = str(bin(x)) # get binary string "0b101101" ("0b" prefix always attached)
str(bin(x))[2:].count("1") # number of set bits

# goes through all subsets of n elements
for s in range(1<<n):
  print(s)
```
- bitmasking converts permutations (n!) to subsets (n*2^n) in dynamic programming. ex: elevator has max weight x. n people each with different weights travel up on the elevator. find the min # of trips.
``` cpp
# best subset has a memoized pair representing: 1. the number of rides to get everyone up, and 2. the size of the last elevator ride
best = {};
best[0] = (1,0);

# iterate over subset of people
for s in range(1<<n):
  # worst case: n+1 rides are needed
  best[s] = (n+1,0);

  # for each person in the subset, ...
  for p in range(n):
    if s & (1<<p):

      # ... check the memoized subset without them and the cost to add them
      option = best[s^(1<<p)];
      if option[1] + weight[p] <= x:
        option[1] += weight[p]
      else:
        option[0] += 1
        option[1] = weight[p];

      best[s] = min(best[s], option);
```

# Nested Functions
- not as readable, but less memory (since not referencing the class)
``` python
class Solution:
  def do(self):
    globalval = 5
    def helper():
      nonlocal globalval # sometimes required to access globalval within
      return
    return helper

# instead of helper functions...

class Solution:
  def helper(self):
    return
  def do(self):
    return self.helper
```

# Enumerate
- simplifies loops needing value and index
``` python
for index, value in enumerate(values):
```

# Comparing Objects
- just define this function
``` python
def __lt__(self, other):
  return self.intAttribute < other.intAttribute
```

# Map Function
- given function and iterable, returns iterable (map object) with all items run through the function
```python
def squ(n):
  return n ** 2
map(squ, [1,3,2]) # [1,9,4]
```

# Filter Function
- given function (that returns a boolean) and iterable, returns iterable (filter object) with only items that cause the given function to return True
```
def odd(n):
  return bool(n%2)
filter(odd, [1,2,3,4]) # [1,3]
```

# Zip Function
- given any number of iterables of equal length, returns iterable (zip object) of tuples (grouping items of the same index)
```
zip([1,2,3],[4,5,6],[7,8,9]) # [(1,4,7),(2,5,8),(3,6,9)]
```

# Sum Sequence
- n: number of numbers in sequence
- a: first number in sequence
- d: difference between numbers
- sum = na + dn(n-1)/2
- Example:
  - 20+25+...+ (30 numbers in total)
  - n = 30
  - a = 20
  - d = 5

# Operations
- log
```python
math.log(50,3) # base 3
```

# Combinations
- n choose k
```
import math
math.comb(n, k)
```

# Time Complexity
| n | Possible complexities |
|----|----|
| n $\leq$ 10 | $n!$, $n^7$, $n^6$|
| n $\leq$ 20 | $2^n*n$, $n^5$|
| n $\leq$ 80 | $n^4$|
| n $\leq$ 400 | $n^3$|
| n $\leq$ 7500 | $n^2$|
| n $\leq 7*10^{4}$ | $n\sqrt{n}$|
| n $\leq 5*10^{5}$ | $n\log{n}$|
| n $\leq 5*10^{6}$ | $n$|
| n $\leq 10^{18}$ | $\log^2{n}$, $\log{n}$, $1$|
