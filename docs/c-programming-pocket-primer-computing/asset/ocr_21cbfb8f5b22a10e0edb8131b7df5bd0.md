The loop in Listing 6.12 attempts to swap by executing this code sequence: a = b; b = a; a = b; which obviously does not perform a swap: it simply assigns b to a. The solution involves performing a *correct* swap. The purpose of this code sample is to show you how easy it is to write buggy C code that looks correct.

# MEMORY ALLOCATION FUNCTIONS IN C

The C programming language supports several functions that enable you to dynamically allocate (and free) memory in a C program:

+   - malloc()
+   - calloc()
+   - realloc()
+   - free()

The malloc() function allocates a block memory in C programs, which is very useful when you define custom structures (as discussed in chapter 6).

The calloc() function allocates a block of memory (just like the malloc() function) and also initializes the allocated memory to zero.

The realloc() function resizes a memory block that was allocated by malloc() or calloc(). If there is sufficient room after the memory block, or if the block is shrinking, it may be possible to do the reallocation in place. If the memory block needs to be reallocated in a new location, the existing data will be copied to the new block and the old block will be freed.

The free() function has the opposite purpose: it frees the memory that was allocated by the functions malloc(),