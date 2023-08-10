# OM Study

- [Implementations](#implementations)
- [Operating Systems](#operating-systems)
- [Common Questions](#common-questions)


# Implementations


Heap
- add by adding to end and floating up to meet invariant
- pop by removing top, moving bottom to top, and sinking down to meet invariant
```python3
class MinHeap:
  def __init__(self):
    self.heap = [0]

  def push(self, val):
    i = len(self.heap)
    self.heap.append(val)

    # float up until parent is smaller
    while i != 1 and self.heap[i//2] > self.heap[i]:
      self.heap[i//2], self.heap[i] = self.heap[i], self.heap[i//2]
      i = i//2
    
  def pop(self):
    n = len(self.heap)
    if n <= 1:
      raise RuntimeError("cannot pop empty heap")
    
    smallest = self.heap[1]
    
    # take end and sink from top
    self.heap[1] = self.heap.pop()
    n -= 1
    i = 1
    
    while i*2 < n:
      if i*2+1 < n:
        # possibly switch with left or right
        if self.heap[i] > self.heap[i*2] and self.heap[i*2] >= self.heap[i*2+1]:
          # switch with right
          self.heap[i], self.heap[i*2+1] = self.heap[i*2+1], self.heap[i]
          i = i*2+1
        elif self.heap[i] > self.heap[i*2+1] and self.heap[i*2+1] >= self.heap[i]:
          # switch with left
          self.heap[i], self.heap[i*2] = self.heap[i*2], self.heap[i]
          i = i*2
        else:
          # already satifies invariant
          break
      else:
        if self.heap[i] > self.heap[i*2]:
          # switch with left
          self.heap[i], self.heap[i*2] = self.heap[i*2], self.heap[i]
          i = i*2
        else:
          # already satifies invariant
          break

    return smallest
```

Hash table
- a good hash function distributes hash values uniformly and reduces collisions
- prime numbers used to reduce collisions
``` python3
class HashTable:
  def __init__(self, size=100):
    self.size = size
    self.table = [[] for _ in range(size)]

  def _hash_function(self, key):
    # Simple hash function using the built-in hash() function
    return hash(key) % self.size

  def put(self, key, value):
    index = self._hash_function(key)
    for kvp in self.table[index]:
      if kvp[0] == key:
        kvp[1] = value  # Update value if key already exists
        return
    self.table[index].append([key, value])

  def get(self, key):
    index = self._hash_function(key)
    for kvp in self.table[index]:
      if kvp[0] == key:
        return kvp[1]
    raise KeyError("Key not found in the hashtable")

  def remove(self, key):
    index = self._hash_function(key)
    for i, kvp in enumerate(self.table[index]):
      if kvp[0] == key:
        self.table[index].pop(i)
        return
    raise KeyError("Key not found in the hashtable")
```

Heap class with ability to push/pop

Matching engine

# Networks

- Networks interview questions: https://www.geeksforgeeks.org/networking-interview-questions/


# Operating Systems

- OS interview questions: https://www.geeksforgeeks.org/operating-systems-interview-questions/

## os basics

### os components
- os: software that act as intermediary between users and computer hardware
- kernel: central part of os that manages hardware and provides services to higher-level software
- resource manager: part of os manages allocating resources (cpu time, memory, i/o devices)
- process scheduler: part of os responsible to selecting processes and assigning to cpu for execution
- memory manager: part of os that handles memory
- device drivers: software components that act as intermediary between os and hardware devices
- shell: ui that allows interacting with os

### os types
- single-user single-task
- single-user multi-task
- multi-user
- batch: straight processing a queue of jobs
- real-time (RTOS): designed to meet strict timing requirements (often used in embedded systems)

### os architectures
- monolithic kernel: single module that handle all functionality
- microkernel: minimalistic kernel with modular extensions
    - modular extensions: software components that extend os kernel functionality

### boot process
- bootstrapping: process of loading and initializing os

steps:
1. Power-On Set-Test (POST): BIOS (basic input/output system) starts testing all hardware components
1. Bootstrap Loader: BIOS finds bootloader (program for loading OS usually stored in Master Boot Record on hard drive, sometimes external flash drive)
1. OS Load: Boot loader loads OS kernel into memory
1. Kernel Initialized: Kernel of OS initialized other components
1. User Mode Initialization
1. User Login
1. GUI Presentation

### Multitasking
- process: a running instance of a program
    - includes its own:
    - program counter (pc): keeps track of next instruction
    - memory space: program code, stack, and heap
    - execution state: either running, ready to run, waiting, or terminated
- context switching: saving and restoring the context of a process when switching between tasks 
- time-sharing: cpu time is shared among processes to provide appearance of parallel execution
- threading: achieve multitasking within a process, allowing different parts of program to run concurrently
- thread: share same memory space of parent process and each have their own execution state
- concurrency: system can manage multiple tasks (in different execution states) at same time
- parallelism: system can execute multiple tasks at same time

### Memory
- virtual memory: memory management technique to provide illusion of larger memory space than physically available by loading process's memory fron disk uppon runnning

### Virtualization
- virtual machine: emulation of a physical computer
- virtualization: creating multiple instances of an os on a single machine
- hypervisor: manages multiple virtual machines on a single machine


## Processes and Threads

## CPU Scheduling

## Memory Management

## File Systems

## Input/Output Management

## Interprocess Communication

## Deadlock and Synchronization

## Virtualization and Hypervisors

## Distributed Operating Systems

## Security and Protection Mechanisms



# Common Questions

List all the linux commands
  
| Command | Purpose |
| --- | --- |
| `cd` | change dir |
| `ls` | show dir | 
| `mv` | move file |
| `cp` | copy to |
| `rm` | remove |
| `ln` | create alias for path |
| `ps` | list processes for current user |
| `pwd` | path current dir |
| `who` | see current logins |
| `cat` | concat and print |
| `top` | running dashboard of all processes |
| `kill` | kill process |
| `find` | find file by name |
| `echo` | print str |
| `less` | print file nice UI |
| `more` | print file all |
| `touch` | create file |
| `which` | path for command's executable |
| `chmod` | change file permissions |
| `chown` | change file ownership |
| `alias` | list command aliases |
| `source` | execute file |


What is polymorphism
- you can access objects of different types through the same interface
- for example Cat is-a Animal and Dog is-a Animal in the instances cat and dog you can both run()

What is little vs big endian
- _address0_, _address1_, _address2_, _address3_, ...
- storing number in memory, depends on processor
- AbCdEf
- Big endian: Ab, Cd, Ef
  - used in data exchange over networks
- Little endian: Ef, Cd, Ab
  - efficient

What is a compiler
- translates code into bytecode that the computer's hardware can execute directly
- preprcessing: handles preprocessor directives such as #include
- compilation: translates source code into object file ".o"
- linking: combines accross different files
- library linking: external libraries

What is an interpreter
- executes code directly, line-by-line without need for compilationis 

What is a kernel:
- The core component of the operating system responsible for managing hardware, memory, processes, and essential functions

What happens when you start a computer
- Power-On Set-Test (POST): BIOS (computer's firmware) starts testing all hardware components
- Bootstrap Loader: BIOS finds boot loader (program for loading OS usually stored in Master Boot Record on hard drive, sometimes external flash drive)
- OS Load: Boot loader loads OS kernel into memory
- Kernel Initialized: Kernel of OS initialized other components
- User Mode Initialization
- User Login
- GUI Presentation

What number of threads is a lot of threads
- If there are more threads than CPU cores, then there will be a decrease in performace for context switching

How would you write a C program to check if a computer is little endian
``` c
#include <stdio.h>

int isLittleEndian() {
    unsigned int num = 1;
    char* ptr = (char*)&num;
    
    // If the first byte (lowest address) contains the least significant bit, the computer is little endian.
    return (*ptr == 1);
}
```

What happens when a URL is typed into a browser and requres a redirect
1. browser sends HTTP request to web server associated with URL
2. server generates HTTP response, the repsonse is (3xx) for redirect and has "Location" header
3. Browser get header and initiates another request to new URL

What happens when you print to STDOUT
- data added to internal buffer
- once buffer is explicitly flushed or has some size it will add to stdout stream
- stream is usually to console

How do you simplify and boolean expression
```
Identity Law:
A | 0 = A
A & 1 = A

Null Law:
A | A' = 1
A & A' = 0

Domination Law:
A | A = A
A & A = A

Is Commutative (change symbol order)
Is Associative (change operation order)
(A | B) | C = A | (B | C)
(A & B) & C = A & (B & C)

Distribute
A & (B | C) = (A & B) | (A & C)
A | (B & C) = (A | B) & (A | C)
(A | B)' = A' & B' (demorgans)
(A & B)' = A' | B' (demorgans)

May be better to check solution: with 3 variables -> 2^3 possibilities
```

Struct vs Union
- struct: contains each element in memory, with padding if not multiple of 8
```cpp
struct ExampleStruct {
  int a;
  char b;
  float c;
};
```
- union: contains one possible element, so size of union is size of greatest possible datatype (float here)
```cpp
union ExampleUnion {
  int a;
  char b;
  float c;
};
```

Fastest arithmetic operations on modern cpu:
- (<<), (>>)
- (*) when multiplying by power of 2 it is reduced to left shift
- (/) when dividing by power of 2 it is reduced to right shift
- (*)
- (/) (division uses * at its core)
- (%)

Auto Cast in CPP
- comparing int and float, int is auto casted to float

LTO
- Link-time Optimization
- If enabled, at link phase of compilation, allows for optimizing code across multiple compilation units rather than optimizing individual translation units in isolation

Order of Constructor/Destructor without LTO on
- class A, class B : public A. then we call `B b; A a;`
- B inherits from A
- constructors first:
  - A then B to make b
  - A to make a
- destructors after:
  - B then A to dest b
  - A to dest a

Output on successful grep
- `grep "bar" foo.txt && echo "bar exists"`

C++ fork()
- creates a new process (child process) that is an identical copy of the parent process that initially has the same code, data, and open file descriptors as the parent
- returns PID (process id)
- operating same or sequential determined by os
```cpp
// adds to buffer -> forks -> both flush buffer -> "HelloHello"
cout << "Hello";
fork();
```
```cpp
// adds to buffer -> flushes -> "Hello" -> forks
cout << "Hello\n";
fork();
```

