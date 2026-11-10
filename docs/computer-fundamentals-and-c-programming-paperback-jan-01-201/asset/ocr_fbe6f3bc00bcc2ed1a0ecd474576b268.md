# # 16 Dynamic Memory Allocation and Linked Lists

# ### WHAT TO LEARN

+   - Concepts of *dynamic memory allocation* and the returned generic pointer.
+   - Allocating memory with the **malloc** and **calloc** functions.
+   - Freeing the allocated block with the **free** function.
+   - Resizing an allocated memory block with **realloc**.
+   - How negligence leads to *memory leaks* and *dangling pointers*.
+   - How 2D arrays can be simulated on-the-fly while a program is running.
+   - Attributes of a *linked list* and how they overcome the limitations of an array.
+   - Manipulating a linked list with user-defined functions.
+   - Features of the abstract data types—*stacks*, *queues* and *trees*.

# ## 16.1 MEMORY ALLOCATION BASICS

Up until now, memory for variables, arrays and structures have been allocated at the time of their *definition*. For variables and arrays, definition is synonymous with *declaration*. The amount of memory thus allocated is fixed at compile time and can't be modified at runtime. This inflexibility becomes a serious limitation when working with arrays. In our quest to ensure that arrays are large enough to accommodate our needs, we often tend to oversize them. Because of the wastage resulting from this *static* allocation of memory, our programs are often not as efficient as they could otherwise have been.

The solution to this problem lies in *dynamically* allocating memory at runtime, i.e., as and when the program needs it. Access to the allocated block is provided by a generic pointer that is automatically aligned to reflect the correct type of data pointed to. Because a pointer to a contiguous memory block can also be treated as an array, we can easily manipulate this array. In the course of program execution, if this memory chunk is found to be under- or over-sized, it can be resized using a special function (**realloc**) of the standard library.