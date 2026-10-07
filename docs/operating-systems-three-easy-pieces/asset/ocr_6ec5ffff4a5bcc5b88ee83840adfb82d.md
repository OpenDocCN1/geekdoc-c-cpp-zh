# THE ABSTRACTION: ADDRESS SPACES

0KB

| | Operating System (code, data, etc.) |
|---||
| 64KB | (free) |
| 128KB | Process C (code, data, etc.) |
| 192KB | Process B (code, data, etc.) |
| 320KB | (free) |
| 384KB | Process A (code, data, etc.) |
| 448KB | (free) |
| 512KB | (free) |

Figure 13.2: Three Processes: Sharing Memory

# 13.3 The Address Space

However, we have to keep these pesky users in mind, and doing so requires the OS to create an easy to use abstraction of physical memory. We call this abstraction the address space, and it is the running program’s view of memory in the system. Understanding this fundamental OS abstraction of memory is key to understanding how memory is virtualized.

The address space of a process contains all of the memory state of the running program. For example, the code of the program (the instructions) have to live somewhere, and thus they are in the address space. The program, while it is running, uses a stack to keep track of where it is in the function call as well as to allocate local variables and pass parameters and return values from routines. Finally, the heap is used for dynamically-allocated, user-managed memory, such as that you might receive from a call to malloc() in C or new in an object-oriented language like C++ or Java. Of course, there are other things in two (e.g., statically-initialized variables), but for now let us assume these these three components: code, stack, and heap.

In the example in Figure 13.3 (page 132), we have a tiny address space (only 16KB). The program code lives at the top of the address space (a) it is a pain to represent a 32-bit

> ^1 We will often use small examples like this because a) is a pain to represent a 32-bit address space and (b) the math is harder. We like simple math.

© 2008–19, ARPACI-DUSSEAU

THREE EASY PIECES