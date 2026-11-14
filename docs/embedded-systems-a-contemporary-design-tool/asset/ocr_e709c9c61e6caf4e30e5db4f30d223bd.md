| Block | | | | | | | Group |
|---|---|---|---|---|---|---|---|
| 0 | 64 | 128 | • | • | • | 384 | 448 | 0 |
| 1 | 65 | 129 | | | | 385 | 449 | 1 |
| 2 | 66 | 130 | | | | 386 | 450 | 2 |
| • | | | | | | | |
| • | | | | | | | |
| • | | | | | | | |
| 63 | 127 | 192 | | | | 447 | 511 | 63 |

The tag table will have 128 entries. Table 4.3 illustrates how the main memory addresses are mapped to the cache addresses.

# Table 4.3 Main Memory to Cache Mapping

Set Number | Cache | Main Memory | Group Number
---|---|---|---
Tag Table | | | 
2 - 7 | 128 448 | 0 64 128 • • • 384 448 | 0
1 | 0 65 129 | 1 65 129 | 1
2 | 2 380 | 2 66 130 | 2
6 | • • | • • • | •
• | • • | | •
2 | 63 192 127 | 63 127 192 | 447 511 | 63

Each Tag is 3 bits
Tag Number
450 mod 64 = 2

# 4.20 DYNAMIC MEMORY ALLOCATION

Dynamic memory allocation is usually interpreted as the process of allocating memory at runtime associated with some extensible data structure such as a linked list or heap. The linked-list-based scheme works well for an embedded system. The C malloc and C++ new operators are examples of routines that are used in conjunction with the heap.

Remember: in embedded systems we generally use two kinds of memory, ROM and RAM (which may be cache or main memory). Here we are more concerned with managing main memory to accommodate

+   • Programs larger than main memory.
+   • Multiple processes in main memory.
+   • Multiple programs in main memory.

Traditional virtual memory schemes are completely nondeterministic and, thus, are rarely used in real-time systems, particularly those systems with hard deadlines.