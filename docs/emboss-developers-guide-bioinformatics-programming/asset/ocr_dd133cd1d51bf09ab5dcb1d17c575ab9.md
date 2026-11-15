# 5.4.1.4 Failsafe object construction

Many (but currently not all) functions that modify an object passed by argument will allocate memory for it if an unallocated (NULL) pointer is passed. This is provided as a safety measure against sloppy programming. You should not rely on it. It's recommended that, where appropriate, all object pointers are explicitly allocated in your code before they are used, and of course freed later once you are done with them.

# 5.4.1.5 Dynamic objects

Memory for most objects is dynamically reallocated (and freed) as needed by the library functions. This means for example you can append text to a string object without worrying whether there is sufficient space available, or write to an array element without first checking the array is big enough (new elements will be created as necessary). Similarly, memory is freed automatically when it is no longer needed. The most commonly used dynamic objects are the strings and arrays mentioned, but most of the object functions show this behaviour.

# 5.4.1.6 EMBOSS is free of arbitrary limits

There are no arbitrary hard-coded limits in the code. For example there is no hard-coded maximum to the length of a sequence or the number of sequences in a sequence alignment, and no upper limits to the size of a matrix you can create. The only restrictions come from the hardware you are using.

# 5.4.2 General memory management

# 5.4.2.1 General macros

Instead of calling malloc, calloc or free directly you should use the macros provided:

| Macro | Description |
|---|---|
| AJALLOC(nbytes) | Allocates nbytes of uninitialised memory. This is equivalent to using malloc. |
| AJALLOCO(nbytes) | Allocates nbytes of memory and initialises the memory to zero. Equivalent to using calloc. |
| AJCALLOC(count, nbytes) | Allocates an array of count elements of nbytes. The array elements are uninitialised. Equivalent to using malloc. |
| AJCALLOCO(count, nbytes) | Allocates an array of count elements of nbytes and initialises the memory to zero. Equivalent to using calloc. |
| AJRESIZE(ptr, nbytes) | Resizes previously allocated memory (referenced by ptr) to a new size of nbytes. Initialises new additional reserved memory (if any) to zero. The original memory contents are preserved regardless of whether the block is moved or not. If a NULL pointer is passed then a new block of memory is allocated automatically. Equivalent to using realloc. |
| AJFREE(ptr) | Frees memory using free and sets the pointer to NULL. Ignores NULL pointers. |

Most of these macros allocate (or reallocate) some memory and return a pointer to it. In case of failure a NULL pointer is returned and an exception raised. The exception message is