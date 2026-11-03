# Table 15.1 Memory Allocation Functions

| Function | Task |
|---|---|
| malloc | Allocates requested size of bytes and returns a pointer to the first byte of the allocated space. |
| calloc | Allocates space for an array of elements, initializes them to zero and then returns a pointer to the memory. |
| free | Frees previously allocated space. |
| realloc | Modifies the size of previously allocated space. |

# Memory Allocation Process

Before we discuss these functions, let us look at the memory allocation process associated with a C program. Figure 15.1 shows the conceptual view of storage of a C program in memory.

![](bbox=[0.35, 0.56, 0.75, 0.75])

Fig. 15.1 Storage of a C program

The program instructions and global and static variables are stored in a region known as permanent storage area and the local variables are stored in another area called stack. The memory space that is located between these two regions is available for dynamic allocation during execution of the program. This free memory region is called the heap. The size of the heap keeps changing when program is executed due to creation and death of variables that are local to functions and blocks. Therefore, it is possible to encounter memory "overflow" during dynamic allocation process. In such situations, the memory allocation functions mentioned above return a NULL pointer (when they fail to locate enough memory requested).

# Allocating a Block of Memory

A block of memory may be allocated using the function malloc. The malloc function reserves a block of memory of specified size and returns a pointer of type void. This means that we can assign it to any type of pointer. It takes the following form:

```
ptr = (cast-type*) malloc(byte-size);
```

ptr is a pointer of type cast-type. The malloc returns a pointer (of cast type) to an area of memory with size byte-size.