# 29. MEMORY MANAGEMENT

This chapter explains dynamic memory management in C. The C programming language provides several functions for memory allocation and management. These functions can be found in the **<stdlib.h>** header file.

| S.N. | Function and Description |
|---|---|
| 1 | **void *calloc(int num, int size);**<br>This function allocates an array of **num elements** each of which size in bytes will be **size**. |
| 2 | **void free(void *address);**<br>This function releases a block of memory block specified by address. |
| 3 | **void *malloc(int num);**<br>This function allocates an array of **num** bytes and leave them initialized. |
| 4 | **void *realloc(void *address, int newsize);**<br>This function re-allocates memory extending it upto **newsize**. |

# Allocating Memory Dynamically

While programming, if you are aware of the size of an array, then it is easy and you can define it as an array. For example, to store a name of any person, it can go up to a maximum of 100 characters, so you can define something as follows:

```
char name[100];
```

But now let us consider a situation where you have no idea about the length of the text you need to store, for example, you want to store a detailed description about a topic. Here we need to define a pointer to character without defining how much memory is required and later, based on requirement, we can allocate memory as shown in the below example:

```
#include <stdio.h>
```