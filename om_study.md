# OM Study

# List all the linux commands

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


# What is polymorphism
- you can access objects of different types through the same interface
- for example Cat is-a Animal and Dog is-a Animal in the instances cat and dog you can both run()

# What is little vs big endian
- _address0_, _address1_, _address2_, _address3_, ...
- storing number in memory, depends on processor
- AbCdEf
- Big endian: Ab, Cd, Ef
  - used in data exchange over networks
- Little endian: Ef, Cd, Ab
  - efficient

# What is a compiler
- translates code into bytecode that the computer's hardware can execute directly
- preprcessing: handles preprocessor directives such as #include
- compilation: translates source code into object file ".o"
- linking: combines accross different files
- library linking: external libraries

# What is an interpreter
- executes code directly, line-by-line without need for compilationis 

# What is a kernel:
- The core component of the operating system responsible for managing hardware, memory, processes, and essential functions

# What happens when you start a computer
- Power-On Set-Test (POST): BIOS (computer's firmware) starts testing all hardware components
- Bootstrap Loader: BIOS finds boot loader (program for loading OS usually stored in Master Boot Record on hard drive, sometimes external flash drive)
- OS Load: Boot loader loads OS kernel into memory
- Kernel Initialized: Kernel of OS initialized other components
- User Mode Initialization
- User Login
- GUI Presentation

# What number of threads is a lot of threads
- If there are more threads than CPU cores, then there will be a decrease in performace for context switching

# How would you write a C program to check if a computer is little endian
``` c
#include <stdio.h>

int isLittleEndian() {
    unsigned int num = 1;
    char* ptr = (char*)&num;
    
    // If the first byte (lowest address) contains the least significant bit, the computer is little endian.
    return (*ptr == 1);
}
```

# What happens when a URL is typed into a browser and requres a redirect
1. browser sends HTTP request to web server associated with URL
2. server generates HTTP response, the repsonse is (3xx) for redirect and has "Location" header
3. Browser get header and initiates another request to new URL

# What happens when you print to STDOUT
- data added to internal buffer
- once buffer is explicitly flushed or has some size it will add to stdout stream
- stream is usually to console

# What are the components of a computer

# Heap class with ability to push/pop

# Implement matching engine
