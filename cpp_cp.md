# C++ For Competitive Programming
STL:

[stl data structures](#stl-data-structures)
- [string](#string)
- [struct](#struct)
- [vector](#vector)
- [array](#array)
- [forward_list](#forward_list)
- [pair](#pair)
- [tuple](#tuple)
- [list](#list)
- [stack](#stack)
- [queue](#queue)
- [priority_queue](#priority_queue)
- [bitset](#bitset)

[sets](#sets)
- [set](#set)
- [unordered_set](#unordered_set)
- [multiset](#multiset)
- [unordered_multiset](#unordered_multiset)

[maps](#maps)
- [map](#map)
- [unordered_map](#unordered_map)
- [multimap](#multimap)
- [unordered_multimap](#unordered_multimap)

[stl algorithms](#stl-algorithms)
- [sorting](#sorting)
- [searching](#searching)

Implemented:

[hashing](#hashing)
- [counter](#counter)

[dynamic programming](#dynamic-programming)
- [memoization](#memoization)
- [generating subsets](#generating-subsets)
- [generating permutations](#generating-permutations)
- [bitmasking](#bitmasking)

[grouping](#grouping)
- [union-find](#union-find)

[node structures](#node-structures)
- [ListNode](#listnode)
- [TreeNode](#treenode)
  - [dfs](#dfs-node-version)
  - [bfs](#bfs-node-version)

[graphs](#graphs)
- [graph-representations](#graph-representations)
- [dfs](#graph-dfs)
- [bfs](#graph-bfs)
- [check for cycles](#check-for-cycles)
- [max flow](#max-flow)

[range queries](#range-queries)
- [binary indexed trees](#binary-indexed-trees)
- [segment trees](#segment-trees)

[strings](#strings)
- [trie](#trie)
- [z-array](#z-array)

[todo](#todo)

---

># stl data structures

# string
- dynamic array of characters
```cpp
// create
string s = "abcdefg";

// size
s.length();

// read
char ch = s[2];

// as stack
a.back()
a.front()
s.push_back('a');
s.pop_back();

// update
s.append("more");
s[2] = 'c';
b.replace(2,3,"hit"); // replace charts starting 2, length 3 with "hit"
transform(s.begin(), s.end(), s.begin(), [](auto c) { return toupper(c); }); // to uppercase

// delete
s.clear();
a.erase(2,3); // deletes chars starting 2, length 3

// substrings
string b = a.substr(2,3); // substring starting 2, length 3
string b = a.substr(2);   // substring starting 2, to end
size_t pos = a.find("bcd"); // returns string::npos if not found
size_t a = s.find_last_of(",");

// string to/from int
string a = to_string(123);
int b = atoi("123");

// char to/from int and string
isalpha('a') // true if character
tolower('A') // lowercases character
isdigit('2') // true if character is an integer
string s = string(1, 'a'); // string from char
int a = '9' - 48; // char to int (subtract 48)

// splitting string by token using stringstream
#include <sstream>
string input = "abc,def,ghi";
istringstream ss(input);
string token;
while(getline(ss, token, ',')) {
  cout << token << '\n';
}
```

# struct
- multiple variables in one container
```cpp
struct name {
  int num;
  string str;
};
name var_name;
var_name.num = 5;
```

# vector
- resizing array
```cpp
#include <vector>

// create
vector<int> a = {1,2,3};
vector<int> a = vector<int>(3, 5); // 5 5 5
vector<int> a;
a.assign(3, 5); // 5 5 5
vector<int> a(10); // size 10, all 0s
vector<int> a(10, 2); // size 10, all 2s
vector<vector<int>> a(3); // vector of 3 empty vectors
vector<vector<int>> a(3, vector<int>(4)); // 3 rows, 4 cols of 0s

// size
a.size()
a.empty()

// access
a[2];
a[1] = 2;
a.push_back(1);
a.emplace_back((2,3)); // push back for sinlge elements, emplace_back for tuples
a.pop_back();

// insert (emplace is inplace efficient inserting)
a.insert(a.end(), v.begin(), v.end()); // append vector to end [a, v]
a.insert(a.end(), 5, 1); // insert 5 1s
a.emplace(vec.begin(), 5); // {5,1,2,3}
a.emplace(vec.end()-1, 5); // {1,2,5,3}

// vector algorithms
#include <algorithm>

// reverse
reverse(a.begin(), a.end());

// min and max
int max_num = *max_element(a.begin(), a.end()); // iterator to max or a.end() if empty vector
int index_max = max_element(a.begin(), a.end()) - a.begin(); // index max
int min_num = *min_element(a.begin(), a.end()); // iterator to min
int index_min = min_element(a.begin(), a.end()) - a.begin(); // index min

// sum
accumulate(a.begin(), a.end(), 0); // sum all and 0

// count
count(a.begin(), a.end(), 5); // number occurances of 5

// find
int index = find(a.begin(), a.end(), 5) - a.begin(); // iterator to first occurance of 5 or a.end() if not found

// sort only nth number to get median O(n)
nth_element(arr.begin(), arr.begin() + arr.size()/2, arr.end()); //arr[n/2] is median

// get unique
unique(a.begin(), a.end()); // keeps only unique but doesn't resize, returns pointer to new end
a.erase(unique(a.begin(),a.end()),a.end()); // keeps only unique

// transform (like map): apply to each element of a vector
vector<int> out;
transform(v.begin(), v.end(), back_inserter(out), f);
for (int& n : nums) n = pow(n,2);

// filter: get vector of only valid elements
vector<int> out;
copy_if(v.begin(), v.end(), back_inserter(out), [](int i){return i>=0;} );

// partition vector
is_partitioned(vect.begin(), vect.end(), [](int x) { return x%2==0; }); // bool if partitioned
partition(vect.begin(), vect.end(), [](int x) { return x%2==0; }) // 2 3 4 3 7 9, partitions
// stable_partition(...) preserves order
// partition_point(...) iterator to first element with false property
```

# array
- basic array that holds its own size
```cpp
#include <array>

// create
const size_t n = 5;
array<int,n> a = {0}; // 0,0,0,0,0
array<int,6> a = {1,2,3}; // 1,2,3,0,0,0

// set
a[0] = 4;

// read
cout << a[3];
```

# forward_list
- singly linked list
```cpp
#include <forward_list>

forward_list<int> a = {1,2,3};
// .push_front() .pop_front() .insert_after() .remove_if()
*++a.begin(); // second element
```

# pair
- two elements grouped together
```cpp
#include <utility>
pair<int, char> p;
p.first = 100;
p.second = 'g';
pair<int, char> p(1, 'a');
pair<int, char> p(p1); // copy of p1
p = {1, 'a'};
```

# tuple
- any size list of elements of different types
```cpp
tuple<int, string, double> a = {3, "hi", 5.6};

// get all at once
auto [f, s] = a;

// get individual
int ff = get<0>(a);

// set individual
get<1>(a) = "hello";
```

# list
- double linked list
```cpp
#include <iterator>
#include <list>
list<int> l;
// make list
for (int i=0; i<10; ++i) {
  l.push_back(i); // .pop_back() to remove .back() to see
  l.push_front(i); // .pop_front() to remove, .front() to see
}
// traverse list
list<int>::iterator it;
for (it = l.begin(); it != l.end(); ++it) {
    cout << *it;
}
l.sort(); // sort
l.reverse(); // reverse
l.empty(); // if empty
l.size(); // size
l.insert(pos_iter, how_many, ele); // insert
l.erase(pos_iter_first, pos_iter_last)
// remove() removes elements
// remove_if() removes if results in true
```

# stack
- LIFO container
```cpp
#include <stack>

// create
stack<int> a;

// size
a.empty() 
a.size()

// operations
a.push(3);
a.top(); // just look
a.pop();
```

# queue
- FIFO container (add to back, remove from front)
```cpp
#include <queue>

// create
queue<int> q;

// size
q.empty();
q.size();

// operations
q.push(10);
q.pop(); // remove from front but doesn't return value
q.front();
q.back();
```

# priority_queue
- add item O(logn), take out item with highest priority O(logn)
```cpp
#include <queue>

// create
priority_queue<int> g; // default is max on top
priority_queue<int, vector<int>, greater<int>> p; // min on top

// size
g.empty();
g.size();

// operations
g.push(10);
g.top(); // look only
g.pop(); // pop top
```

# bitset
```cpp
// working with bitsets
// create
uint32_t n = 5; // takes exactly 32 bits
bitset<32> a(n);

// read
a.to_string(); // "000...0101"
a.count(n); // count number of 1s
a.any(); // if any is 1
a.all(); // if all 1s

// modify
a[0]; // access 0th bit (least significant: ie 5 -> 00000101)
a[0].flip();
```

> # sets

# set
- sorted, unique elements (binary search tree)
- iterating over set is in order
```cpp
#include <set>

// create
set<int> a;
set<int, greater<int>> b;
vector<int> v({ 1, 2, 3});
set<int> d(v.begin(), v.end());
set<int> e = {3, 2, 5};

// size
a.size();
a.empty();

// insert
a.insert(1); 

// read
a.count(5); // 1 (true) or 0 for set

// remove
a.erase(10);
a.clear();
```

# unordered_set
- not sorted, unique elements (hashing)
```cpp
#include <unordered_set>

// create
unordered_set<int> a;
vector<int> v({ 1, 2, 3});
unordered_set<int> d(v.begin(), v.end());
unordered_set<int> e = {3, 2, 5};

// size
a.size();
a.empty();

// insert
a.insert(1); 

// read
a.count(5); // 1 or 0 for set
int b = *a.begin(); // pop
a.remove(a.begin());

// remove
a.erase(10);
a.clear();
```

# multiset
- sorted, not unique elements (red-black tree)
- iterating over set is in order
```cpp
#include <set>

// create
multiset<int> a;
multiset<int, greater<int>> b;
vector<int> v({ 1, 2, 2, 3});
multiset<int> d(v.begin(), v.end());
multiset<int> e = {3, 2, 2, 5};

// size
a.size();
a.empty();

// insert
a.insert(1); 
a.insert({1,2,3}) // insert multiple
a.insert(v.begin(), v.end())

// read
a.count(5);

// remove
a.erase(10); //removes all instances
a.erase(a.find(1)); //removes one instance
a.clear();
```

# unordered_multiset
- not sorted, not unique elements (hashing)
```cpp
#include <unordered_set>

// create
unordered_multiset<int> a;
vector<int> v({ 1, 2, 2, 3});
unordered_multiset<int> d(v.begin(), v.end());
unordered_multiset<int> e = {3, 2, 2, 5};

// size
a.size();
a.empty();

// insert
a.insert(1); 
a.insert({1,2,3}) // insert multiple
a.insert(v.begin(), v.end())

// read
a.count(5);

// remove
a.erase(10); //removes all instances
a.erase(a.find(1)); //removes one instance
a.clear();
```

> # maps

# map
- sorted, unique keys in key-value pairs (binary search tree)
- iterating over map has keys in order
```cpp
#include <map>

// create
map<int, int> a;
map<int, int, greater<int>> b;
vector<pair<int,int>> v({{1,2}, {2,3}, {3,2}});
map<int, int> d(v.begin(), v.end());
map<int, int> e = {{1,2}, {2,3}};

// size
a.size();
a.empty();

// insert
a[2] = 3;
a.insert({{1,2},{2,3}}); // insert multiple
a.insert(v.begin(), v.end());

// read
a.count(5);
a[2];

// remove
a.erase(2); 
a.clear();

// iterating
for (auto i : a) {
    cout << i.first << ' ' << i.second;
}
```

# unordered_map
- not sorted, unique keys in key-value pairs (hashing)
```cpp
#include <unordered_map>

// create
unordered_map<int, int> a; // default 0 value if not inserted
vector<pair<int,int>> v({{1,2}, {2,3}, {3,2}});
unordered_map<int, int> d(v.begin(), v.end());
unordered_map<int, int> e = {{1,2}, {2,3}};

// size
a.size();
a.empty();

// insert
a[2] = 3;
a.insert({{1,2},{2,3}}); // insert multiple
a.insert(v.begin(), v.end());

// read
a.count(5);
a[2];

// remove
a.erase(2); 
a.clear();

// iterating
for (auto i : a) {
    cout << i.first << ' ' << i.second;
}
```

# multimap
- sorted, not unique keys in key-value pairs (red-black tree)
- iterating over multimap has keys in order
```cpp
#include <map>

// create
multimap<int, int> a;
multimap<int, int, greater<int>> b;
vector<pair<int,int>> v({{1,2}, {2,3}, {3,2}});
multimap<int, int> d(v.begin(), v.end());
multimap<int, int> e = {{1,2}, {2,3}};

// size
a.size();
a.empty();

// insert
a.insert({1,1});
a.insert({{1,2},{2,3}}); // insert multiple
a.insert(v.begin(), v.end());

// read
a.count(5);
auto itr = a.equal_range(1);
for (auto i = itr.first; i != itr.second; i++) {
  cout << i.first << ' ' << i.second;
}

// remove
a.erase(2); // erases all pairs with key
a.clear();

// iterating
for (auto i : a) {
    cout << i.first << ' ' << i.second;
}
```

# unordered_multimap
- not sorted, not unique keys in key-value pairs (hashing)
```cpp
#include <unordered_map>

// create
unordered_multimap<int, int> a;
vector<pair<int,int>> v({{1,2}, {2,3}, {3,2}});
unordered_multimap<int, int> d(v.begin(), v.end());
unordered_multimap<int, int> e = {{1,2}, {2,3}};

// size
a.size();
a.empty();

// insert
a.insert({1,1});
a.insert({{1,2},{2,3}}); // insert multiple
a.insert(v.begin(), v.end());

// read
a.count(5);
auto itr = a.equal_range(1);
for (auto i = itr.first; i != itr.second; i++) {
  cout << i.first << ' ' << i.second;
}

// remove
a.erase(2); // erases all pairs with key
a.clear();

// iterating
for (auto i : a) {
    cout << i.first << ' ' << i.second;
}
```

> # stl algorithms

# sorting
- uses quicksort, (heapsort if bad partitionings happens), then insertion sort once smaller
- inplace
```cpp
#include <algorithm>

vector<int> a = {3,3,5,3,4};
sort(a.begin(), a.end()); // increasing
sort(a.begin(), a.end(), greater<int>()); // decreasing
sort(a.begin(), a.end(), my_fun()); // using your comparison
```
    
# searching
- binary search
```cpp
#include <algorithm>
binary_search(a.begin(), a.end(), 5); // true or false
lower_bound(a.begin(), a.end(), 5) - a.begin(); // index {1 3 5* 5 6} or {1 6*}
upper_bound(a.begin(), a.end(), 5) - a.begin(); // index {1 3 5 5 6*} or {1 6*}
```

> # hashing

# counter
- keys as unique items of arr
- values as number of occurances in arr
```cpp
unordered_map<int, int> a;
for (auto i : arr) a[i]++;
```

> # dynamic programming

# memoization
- recursion with memoization
```cpp
int fib(vector<int> &mem, int n) {
  // memoized case
  if (mem[n]) return mem[n];

  // base case
  if (n <= 1) { mem[n] = n; return n; }

  // recurse
  mem[n] = fib(mem, n-1) + fib(mem, n-2);
  return mem[n];
}

int main() {
  int n = 10;
  vector<int> mem(n+1); // all zeros
  return fib(mem, n);
}
```

- when memoization might be 0
```cpp
int fib(unordered_map<int,int> &mem, int n) {
  // memoized case
  if (mem.count(n)) return mem[n];

  // base case
  if (n <= 1) { mem[n] = n; return n; }

  // recurse
  mem[n] = fib(mem, n-1) + fib(mem, n-2);
  return mem[n];
}

int main() {
  int n = 10;
  unordered_map<int, int> mem;
  cout << fib(mem, n);
}
```

# generating subsets
- generate subsets of set {1,...,n}
- subsets of {1,2,3} are {},{1},{2},{3},{1,2},{1,3},{2,3},{1,2,3}
```cpp
vector<int> subset;

void search(int k) {
  if (k == n+1) {
    // progress subset
  } else {
    // try with including k
    subset.push_back(k);
    search(k+1);
    subset.pop_back();

    // try without including k
    search(k+1);
  }
}
```

# generating permutations
- generate permutation of set {1,...,n}
- permutations of {1,2,3} are {1,2,3},{1,3,2},{2,1,3},{2,3,1}{3,1,2},{3,2,1}
```cpp
vector<int> permutation;
vector<bool> chosen(n+1, false);

void search() {
  if (permutation.size() == n) {
    // process permutation
  } else {
    for (int i = 1; i <= n; i++) {
      if (chosen[i]) continue;
      chosen[i] = true;
      permutation.push_back(i);
      search();
      chosen[i] = false;
      permutation.pop_back();
    }
  }
}
```
- built-in cpp way for generating permutations
```cpp
for (int i = 1; i <= n; i++) {
  permutation.push_back(i);
}
do {
  // process permutation
} while (next_permutation(permutation.begin(), permutation.end()));
```

# bitmasking
- 0 is false, numbers are true. Bits can be manipulated to work with subsets
```cpp
// basics
a & 1   // true if odd
a << 5  // left shift 5,  (multiply by 2^5)
a >> 5  // shift right 5, (divide by 2^5 rounded down)

x & (1 << k)  // true if kth bit of x set
x | (1 << k)  // set kth bit of x to 1
x & ~(1 << k) // set kth bit of x to 0
x ^ (1 << k)  // invert kth bit of x

for (int s = 0; s < (1<<n); s++) // goes through all subsets of n elements
```
- bitmasking converts permutations (n!) to subsets (n*2^n) in dynamic programming. ex: elevator has max weight x. n people each with different weights travel up on the elevator. find the min # of trips.
``` cpp
// best subset has a memoized pair representing: 1. the number of rides to get everyone up, and 2. the size of the last elevator ride
vector<pair<int, int>> best(1<<n);
best[0] = {1,0};

// iterate over subset of people
for (int s = 1; s < (1<<n); s++) {
  // worst case: n+1 rides are needed
  best[s] = {n+1,0};

  // for each person in the subset, ...
  for (int p = 0; p < n; p++) {
    if (s & (1<<p)) {

      // ... check the memoized subset without them and the cost to add them
      pair<int, int> option = best[s^(1<<p)];
      if (option.second+weight[p] <= x) {
        option.second += weight[p]l
      } else {
        option.first++;
        option.second = weight[p];
      }
      best[s] = min(best[s], option);

    }
  }
}
```

> # grouping

# union-find
- logn union and logn find
``` cpp
// initially, every number is their own leader
for (int i = 1; i <= n; i++) link[i] = i;
for (int i = 1; i <= n; i++) size[i] = 1; // track size of groups

// find function
int find(int x) {
  while (x != link[x]) x= link[x];
  return x;
}

// check if two numbers in same group
bool same(int a, int b) {
  return find(a) == find(b);
}

// unite groups of two numbers
void unite(int a, int b) {
  a = find(a);
  b = find(b);
  if (size[a] < size[b]) swap(a, b);
  size[a] += size[b];
  link[b] = a;
}
```

> # node structures

# ListNode
- ListNode use to make singly-linked list
- check if not NULL (nullptr) `if (ln->next)`
``` cpp
struct ListNode {
  int val;
  ListNode *next;
  ListNode() : val(0), next(nullptr) {}
  ListNode(int x) : val(x), next(nullptr) {}
  ListNode(int x, ListNode *next) : val(x), next(next) {}
};
```

# TreeNode
- TreeNode used to make binary tree
```cpp
struct TreeNode {
  int val;
  TreeNode *left;
  TreeNode *right;
  TreeNode() : val(0), left(nullptr), right(nullptr) {}
  TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
  TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};
```

## dfs (node version)
```cpp
void preorder(TreeNode* node) {
  if (!node) return;
  cout << TreeNode->val << " ";
  preorder(TreeNode->left);
  preorder(TreeNode->right);
}

void inorder(TreeNode* node) {
  if (!node) return;
  inorder(TreeNode->left);
  cout << TreeNode->val << " ";
  inorder(TreeNode->right);
}

void postorder(TreeNode* node) {
  if (!node) return;
  postorder(TreeNode->left);
  postorder(TreeNode->right);
  cout << TreeNode->val << " ";
}
```

## bfs (node version)
```cpp
void bfs(TreeNode* root) {
  if(!root) return;
  
  queue<TreeNode*> q;
  q.push(root);

  while (!q.empty()){
    for(int i=0; i<q.size(); i++){
      TreeNode* curr = q.front(); q.pop();
      cout << curr->val << ' ';
      
      if(curr->left) q.push(curr->left);
      if(curr->right) q.push(curr->right);
    }
  }
}
```

> # graphs

# graph representations

adjacency matrix representation
- O(n^2) space, O(1) lookup
```cpp
// create adj matrix graph
int n = 5; // number nodes 0,1,...,n-1
vector<vector<int>> graph(n, vector<int>(n)); // all 0s

// add edge 2 to 3
graph[2][3] = graph[3][2] = 1;
```

adjacency list representation
- O(|n|+|e|) space, O(n) lookup, O(1) list connected
```cpp
// create adj list graph
int n = 5; // number nodes 0,1,...,n-1
vector<vector<int>> graph(n);

// add edge 2 to 3
graph[2].push_back(3);
graph[3].push_back(2);
```

adjacency set representation
- faster lookup, sacrificing space
```cpp
// create adj set graph
int n = 5; // number nodes 0,1,...,n-1
vector<unordered_set<int>> graph(n);

// add edge 2 to 3
graph[2].insert(3);
graph[3].insert(2);
```

map set representation
- useful when nodes have different names
```cpp
// create adj list graph
unordered_map<string, unordered_set<string>> graph;

// add edge cat to dog
graph["cat"].insert("dog");
graph["dog"].insert("cat");
```

edge list representation
- a simple list of all edges
```cpp
vector<pair<int,int>> edges;
edges.push_back({1,2}); // from 1 to 2

vector<typle<int,int,int>> edges;
edges.push_back({1,2,4}); // from 1 to 2, weight 4
```

# graph dfs
- good practice
```cpp
void dfs(vector<unordered_set<int>>& graph, vector<int>& visited, int u) {
  cout << u;
  visited[u] = 1;
  for (int v : graph[u]) {
    if (visited[v]) continue;
    dfs(graph, visited, v);
  }
}

int main() {
  int n = 5;
  vector<unordered_set<int>> graph(n);
  vector<int> visited(n, 0);

  dfs(graph, visited, 4);
}
```

- with global variables
- leetcode note: always assign global vars at beginning of main or vars will be used again in the next test case unchanged
```cpp
vector<unordered_set<int>> graph;
vector<int> visited;

void dfs(int u) {
  cout << u;
  visited[u] = 1;
  for (int v : graph[u]) {
    if (visited[v]) continue;
    dfs(v);
  }
}

int main() {
  int n = 5;
  graph.assign(n, {});
  visited.assign(n, 0);
  
  dfs(4);
}
```


# graph bfs
- finding distances
``` cpp
vector<unordered_set<int>> graph;

vector<int> bfs(int s) {
  vector<int> dist(graph.size(), -1);
  queue<int> q;
  dist[s] = 0; q.push(s);
  while (q.size()) {
    int u = q.front(); q.pop();
    for (int v : graph[u]) {
      if (dist[v] == -1) {
        dist[v] = dist[u] + 1;
        q.push(v);
      }
    }
  }
  return dist;
}

int main() {
  int n = 5;
  graph.assign(n, {});
  
  vector<int> bfs(4);
}
```

# check for cycles
- algorithm to find if (possibly not connected) graph has cycle 
- maintain a set S of all nodes. Then you take a node from that set, run dfs on that node, checking for back edges (if so, you know you have a cycle). For each node you visit, remove that node from the set S. After dfs is finished, you check if S is empty. If so, then you know there are no cycles. Otherwise, you take a node from S, and run dfs/bfs on that node. The runtime should be O(n), where n is the number of nodes.
```cpp
// check undirected cycle using bfs

unordered_set<int> s; // set of elements to start from
for (int i=0; i<numCourses; i++) s.insert(i);

// bfs on 0
while (!s.empty()) {
  unordered_set<int> visited = {};
  int bfs_start = *s.begin();
  queue<int> q; q.push(bfs_start);
  while (!q.empty()) {
    int u = q.front(); q.pop();
    s.erase(u); // remove from remaining to visit
    visited.insert(u);
    for (int v : graph[u]) {
      if (visited.count(v)) {
        return false; // cycle detected
      } else {
        q.push(v);
      }
    }
  }
}
// check directed cycle using dfs
```

# max flow
- find max flow in directed graph with source s and sink t
- run time is O(EF) where E is number of edges and F is val of max flow
```cpp
// ford-fulkerson algorithm
// while (there exists path p in G)
//    push max possible flow along path p
//    update graph edges to have residual flows

// a graph with edge 2/3 has 2 out of 3 units flowing
// if a->b is 2/2, residual becomes: 2 b->a
// if a->b is 2/3, residual becomes: 1 a->b and 2 b->a
// if a->b is 0/2, residual remains: 2 a->b


// edmunds-karp algorithm uppoer bound O(E^2*V)
// bfs runs faster because more pushing flows each time
#define ms_graph vector<unordered_map<int,int>>

while (true) {
  // bfs
  vector<int> prevs(graph.size(), 0);
  queue<int> q;
  q.push(1);
  prevs[1]=1;
  while (q.size()) {
    int u = q.front(); q.pop();
    for (auto v : graph[u]) {
      if (prevs[v.first] == 0 && graph[u][v.first]>0) {
        q.push(v.first);
        prevs[v.first] = u;
      }
    }
  }

  if (prevs[n] == 0) break;

  // max sent through
  stack<int> rev;
  int i = n;
  while (i != prevs[i]) {
    rev.push(i);
    i = prevs[i];
  }
  rev.push(i);
  
  vector<int> path;
  while (!rev.empty()) {
    path.push_back(rev.top()); rev.pop();
  }

  int max_pass = INT_MAX;
  for (int i = 0; i < path.size()-1; i++) {
    int curr = path[i];
    int next = path[i+1];
    max_pass = min(graph[curr][next], max_pass);
  }
  count += max_pass;

  // recalculate
  for (int i = 0; i < path.size()-1; i++) {
    int curr = path[i];
    int next = path[i+1];
    int prev_res = graph[curr][next];
    graph[curr][next] = prev_res - max_pass;
    graph[next][curr] = max_pass + prev_res;
  }


}

// count and output
cout << count << '\n';
```
- min cut
- find minimum sum of flows of edges that can be removed to make t not reachable from s
``` cpp
// after ford-fulkerson algo is done, there does not exist a path from s to t
// the set of nodes reachable from s is a
// all edges pointing outside of a are part of min cut
```
- bipartate matching: L is left side nodes, R is right side nodes. weights are 1
- finding max matching: create node s that points to all nodes in L and create node t that all nodes in R point to.
- max flow of this graph is max matching

> # range queries

# binary indexed trees
- dynamic version of prefix sum array (an array of sums from 0 to index)
- supports update and query
```cpp
// get sum of elements [0,index]
int query_bit(vector<int>& bit, int index) {
  index = index + 1;
  int sum = 0;
  // go through ancestors
  while (index>0) {
    sum += bit[index];

    // set to parent index
    index -= index & (-index);
  }
  return sum;
}
 
// update bit by adding val to item at index
void update_bit(vector<int>& bit, int index, int val) {
  index = index + 1;

  // go through ancestors and add val
  while (index <= bit.size()) {
    bit[index] += val;

    // set to parent index
    index += index & (-index);
  }
}

// create and return binary indexed tree (bit) for arr
vector<int> create_bit(vector<int>& arr) {
  // start with a bit of all 0s
  vector<int> bit(arr.size()+1);

  // create bit using update
  for (int i=0; i<arr.size(); i++)
    update_bit(bit, i, arr[i]);

  return bit;
}

int main() {
  vector<int> a = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9};
  vector<int> bit = create_bit(a); // create bit from array
  update_bit(bit, 3, 6); // update: add 6 to index 3
  cout << query_bit(bit, 5); // get sum element [0,5]
}
```

# segment trees
- usable update and query on ranges (can include max, min, sum, and more)
```cpp
// xor example 

// set item at i to new_val
void update_st(vector<int>& st, int i, int new_val) {
  // update arr
  int n = st.size()/2;
  i += n;
  st[i] = new_val;
  for (i /= 2; i >= 1; i /= 2) {
    st[i] = st[2*i] ^ st[2*i+1];
  }
}

// return sum of elements [i,j]
int query_st(vector<int>& st, int i, int j) {
  int n = st.size()/2;
  i += n; j += n;
  int s = 0;
  while (i <= j) {
    if (i%2 == 1) s ^= st[i++];
    if (j%2 == 0) s ^= st[j--];
    i /= 2; j /= 2;
  }
  return s;
}
 
// create segment tree
vector<int> create_st(vector<int>& arr) {
    // create st of length 2 * closest power of 2
    int n = pow(2,ceil(log2(arr.size())));
    vector<int> st(n*2);
 
    for (int i = 0; i < arr.size(); i++) {
      update_st(st, i, arr[i]);
    }
    return st;
}

// Driver program to test above functions
int main()
{
  vector<int> arr = {1,2,3,4};
  vector<int> st = create_st(arr);
  update_st(st, 0, 3);
  cout << query_st(st, 0, 2);
}
```

> # strings

# trie
- insert O(n), search O(n), and has_prefix O(n) for strings with fixed alphabet size
``` cpp
class Trie {
public:
  int alpha_size = 26;
  vector<vector<pair<int,int>>> trie;

  Trie() {
    trie = vector<vector<pair<int,int>>>(1, vector<pair<int,int>>(alpha_size));
  }
  
  void insert(string word) {
    int pos = 0;
    for (int i = 0; i < word.length()-1; i++) {
      int char_i = word[i] - 'a';
      if (trie[pos][char_i].first) {
        // already has node
        pos = trie[pos][char_i].first;
      } else {
        // needs new node
        trie.push_back(vector<pair<int,int>>(alpha_size));
        trie[pos][char_i].first = trie.size()-1;
        pos = trie.size()-1;
      }
    }
    
    // handle last letter
    int char_i = word[word.length()-1] - 'a';
    trie[pos][char_i].second++;
  }
  
  bool search(string word) {
    int pos = 0;
    for (int i = 0; i < word.length()-1; i++) {
      int char_i = word[i] - 'a';
      if (trie[pos][char_i].first) {
        // already has node
        pos = trie[pos][char_i].first;
      } else {
        return false;
      }
    }
    
    // handle last letter
    int char_i = word[word.length()-1] - 'a';
    return trie[pos][char_i].second;
  }
  
  bool has_prefix(string prefix) {
    int pos = 0;
    for (int i = 0; i < prefix.length()-1; i++) {
      int char_i = prefix[i] - 'a';
      if (trie[pos][char_i].first) {
        // already has node
        pos = trie[pos][char_i].first;
      } else {
        return false;
      }
    }
    
    // handle last letter
    int char_i = prefix[prefix.length()-1] - 'a';
    return trie[pos][char_i].first || trie[pos][char_i].second;
  }
};

int main() {
  Trie t = Trie();
  t.insert("hello"); // insert word
  cout << t.search("hello"); // true if contains word
  cout << t.has_prefix("h"); // trie if contains prefix
}
```

# z-array
- In O(n) computes for each index, the length of the longest substring of s that begins at position k and is a prefix of s.
- [A,C,B,A,C] -> [-,0,0,2,0]
- Find where string a occurs in string b by making new string s=a#b where # is a character never found in either string. Find z-array of s and count numbers with length of a.

```cpp
vector<int> get_z(string s) {
  int n = s.size();
  vector<int> z(n);
  int x = 0, y = 0;
  for (int i = 1; i < n; i++) {
    z[i] = max(0,min(z[i-x],y-i+1));
    while (i+z[i] < n && s[z[i]] == s[i+z[i]]) {
      x = i; y = i+z[i]; z[i]++;
    }
  }
  return z;
}
```


# todo
- https://www.geeksforgeeks.org/top-algorithms-and-data-structures-for-competitive-programming/
- math
- functors
- kruskals algo for minimum spanning trees
- topological sort
- binary search tree
- AVL tree
- kd trees
- fenwick tree

