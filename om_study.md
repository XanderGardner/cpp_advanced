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

## Introduction to Operating Systems

### Definition and Purpose of Operating Systems:

**Description:** Operating Systems (OS) are software that act as an intermediary between users and computer hardware, managing resources and providing a convenient environment for running applications.

**Key Definitions:**
- **Kernel:** The central component of an operating system that manages hardware resources and provides essential services to higher-level software.
- **Resource Manager:** The part of the OS responsible for managing and allocating various system resources like CPU time, memory, and I/O devices.
- **Process:** A running instance of a program, consisting of executable code, memory space, and system resources.
- **User Interface:** The means through which users interact with and control the operating system and applications.

### Functions and Components of an Operating System:

**Description:** An OS performs various functions like process management, memory management, file system management, device management, and user interface handling. It consists of several components that work together to execute these functions effectively.

**Key Definitions:**
- **Process Scheduler:** The component responsible for selecting and assigning processes to the CPU for execution.
- **Memory Manager:** The module that handles memory allocation, organization, and protection.
- **File System:** A hierarchical structure that manages files and directories on storage devices.
- **Device Drivers:** Software components that facilitate communication between the operating system and hardware devices.
- **Shell:** The user interface that allows users to interact with the operating system through commands.

### Types of Operating Systems (e.g., Batch, Time-sharing, Real-time):

**Description:** Operating systems can be categorized based on their primary mode of operation, such as batch processing, time-sharing (multi-user), and real-time (meeting strict deadlines).

**Key Definitions:**
- **Batch Processing:** A mode in which a series of jobs are executed without user intervention.
- **Time-sharing (Multitasking):** Allowing multiple users or tasks to share resources like CPU time simultaneously.
- **Real-time Operating System (RTOS):** An OS designed to meet strict timing requirements of real-time applications, often used in embedded systems.

### Operating System Services and User Interfaces:

**Description:** OS provides various services to applications and users, including file management, networking, security, and process control. User interfaces allow interaction between users and the system.

**Key Definitions:**
- **API (Application Programming Interface):** A set of functions and protocols that allow applications to communicate with the operating system.
- **CLI (Command-Line Interface):** A text-based interface where users interact with the OS by typing commands.
- **GUI (Graphical User Interface):** A visual interface that uses graphical elements like windows, icons, and menus for user interaction.
- **System Calls:** Interfaces that allow applications to request services from the OS kernel.

### Evolution of Operating Systems:

**Description:** The history of operating systems has witnessed significant advancements from early mainframes to modern distributed systems, reflecting the evolution of computing technology and user requirements.

**Key Definitions:**
- **Batch Processing Systems:** Early systems that processed large volumes of data in batches without user interaction.
- **Time-sharing Systems:** Introduced the concept of multiple users sharing a single system concurrently.
- **Personal Computers:** OS developed for individual users, bringing computing to a broader audience.
- **Cloud Computing:** Leveraging remote servers to provide scalable computing resources over the internet.

### Operating System Architectures (e.g., Monolithic, Microkernel):

**Description:** The design and organization of operating systems can be classified into different architectures, such as monolithic (single large kernel) and microkernel (minimal kernel with modular extensions).

**Key Definitions:**
- **Monolithic Kernel:** A single, large software module that handles most operating system functionalities.
- **Microkernel:** A minimalistic kernel that provides essential services, with additional functionalities implemented as separate modules.
- **Kernel Extensions:** Additional software components that extend the functionality of the OS kernel.

### Bootstrapping and Boot Process:

**Description:** Bootstrapping is the process of loading an operating system into the computer's memory and initializing the system to start running applications. The boot process involves several stages to get the system up and running.

**Key Definitions:**
- **Bootloader:** A small program that initializes the computer's hardware and loads the operating system.
- **BIOS (Basic Input/Output System):** Firmware that performs hardware initialization during the boot process.
- **UEFI (Unified Extensible Firmware Interface):** Modern firmware interface that replaces BIOS and provides more advanced features.

### System Calls and Application Programming Interface (API):

**Description:** System calls are interfaces provided by the operating system for applications to request services like I/O, memory management, and process control. The API serves as a set of functions that developers can use to interact with the OS.

**Key Definitions:**
- **System Call:** A mechanism that allows user-level processes to request services from the OS kernel.
- **Library API:** A set of functions provided by libraries that applications can use to perform various tasks.
- **POSIX (Portable Operating System Interface):** A standardized API for Unix-like operating systems.

### Multiprogramming and Multitasking Concepts:

**Description:** Multiprogramming allows multiple programs to reside in memory simultaneously, while multitasking enables the execution of multiple tasks concurrently, giving users the illusion of running multiple applications simultaneously.

**Key Definitions:**
- **Time-sharing:** A technique where CPU time is shared among multiple tasks to provide the appearance of parallel execution.
- **Context Switching:** The process of saving and restoring the context of a process when switching between tasks.
- **Process State:** The condition of a process at a particular point in time, such as running, waiting, or terminated.

### System Modes and Privilege Levels (User Mode, Kernel Mode):

**Description:** Modern CPUs support different privilege levels, allowing the OS to differentiate between user-mode (restricted access) and kernel-mode (full access) operations, ensuring security and stability.

**Key Definitions:**
- **Supervisor Mode:** The highest privilege level of a CPU, allowing direct access to hardware resources.
- **Ring Levels:** Privilege levels assigned to different software layers, with ring 0 being the highest (kernel) and higher rings being less privileged.
- **Protection Rings:** Mechanisms to prevent user-mode processes from interfering with kernel operations.

### System Modes and Privilege Levels (User Mode, Kernel Mode):

**Description:** Modern CPUs support different privilege levels, allowing the OS to differentiate between user-mode (restricted access) and kernel-mode (full access) operations, ensuring security and stability.

**Key Definitions:**
- **Supervisor Mode:** The highest privilege level of a CPU, allowing direct access to hardware resources.
- **Ring Levels:** Privilege levels assigned to different software layers, with ring 0 being the highest (kernel) and higher rings being less privileged.
- **Protection Rings:** Mechanisms to prevent user-mode processes from interfering with kernel operations.

### Virtualization and Hypervisors:

**Description:** Virtualization allows multiple virtual instances of an operating system to run on a single physical machine. Hypervisors are software layers that manage virtualized environments.

**Key Definitions:**
- **Virtualization:** The process of creating multiple virtual instances of an operating system or hardware on a single physical machine.
- **Hypervisor:** A software layer that enables the management of multiple virtual machines (VMs) on a single physical host.

### Distributed Systems and Networking:

**Description:** Operating systems in distributed systems manage resources across multiple interconnected computers. Networking services are essential for communication between nodes.

**Key Definitions:**
- **Distributed System:** A collection of interconnected computers that work together to achieve a common goal.
- **Networking Services:** Operating system services that enable communication and data sharing between nodes in a network.

### Fault Tolerance and Reliability:

**Description:** Operating systems aim to provide fault tolerance and reliability by ensuring system availability and recovering from errors and failures.

**Key Definitions:**
- **Fault Tolerance:** The ability of a system to continue functioning properly in the presence of faults or errors.
- **Reliability:** The measure of a system's ability to perform its functions without failure over a specified period.

### Security and Access Control:

**Description:** Operating systems implement security measures to protect data, prevent unauthorized access, and ensure system integrity.

**Key Definitions:**
- **Access Control:** The process of controlling who can access which resources and perform which actions.
- **Authentication:** Verifying the identity of users or processes before granting access to resources.
- **Authorization:** Granting specific permissions to authenticated users or processes based on their roles or privileges.

### Memory Protection and Address Translation:

**Description:** Memory protection mechanisms prevent processes from accessing memory locations outside their allocated areas. Address translation is used to map virtual addresses to physical memory.

**Key Definitions:**
- **Memory Protection:** Preventing processes from accessing memory locations that they are not authorized to access.
- **Address Translation:** The process of converting virtual addresses used by processes into physical addresses in memory.


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

