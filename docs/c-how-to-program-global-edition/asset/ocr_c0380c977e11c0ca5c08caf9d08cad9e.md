```
newPtr = malloc(sizeof(struct node));
```

evaluates sizeof(struct node) to determine a struct node object's size in bytes, allocates a new area in memory of that number of bytes and stores a pointer to the allocated memory in newPtr. The memory is not guaranteed to be initialized, though many implementations initialize it for security. If no memory is available, malloc returns NULL.

Function free deallocates memory—i.e., the memory is returned to the system so that it can be reallocated in the future. To free memory dynamically allocated by the preceding malloc call, use the statement

```
free(newPtr);
```

C also provides functions calloc and realloc for creating and modifying dynamic arrays. These functions are discussed in Section 14.9. The sections that follow discuss lists, stacks, queues and trees, each of which is created and maintained with dynamic memory allocation and self-referential structures.

# Portability Tip 12.1

A structure's size is not necessarily the sum of the sizes of its members. This is so because of various machine-dependent boundary alignment requirements (see Chapter 10).

# Error-Prevention Tip 12.1

When using malloc, test for a NULL pointer return value, which indicates that the memory was not allocated.

# Common Programming Error 12.2

Not freeing dynamically allocated memory when it's no longer needed can cause the system to run out of memory prematurely. This is sometimes called a "memory leak."

# Error-Prevention Tip 12.2

When memory that was dynamically allocated is no longer needed, use free to return the memory to the system immediately. Then set the pointer to NULL to eliminate the possibility that the program could refer to memory that's been reclaimed and which may have already been allocated for another purpose.

# Common Programming Error 12.3

Freeing memory not allocated dynamically with malloc is an error.

# Common Programming Error 12.4

Referring to memory that has been freed is an error that typically results in the program crashing.

# 12.4 Linked Lists

A linked list is a linear collection of self-referential structures, called nodes, connected by pointer links—hence, the term "linked" list. A linked list is accessed via a pointer to the first node of the list. Subsequent nodes are accessed via the link pointer member stored in each node. By convention, the link pointer in the last node of a list is set to NULL to mark