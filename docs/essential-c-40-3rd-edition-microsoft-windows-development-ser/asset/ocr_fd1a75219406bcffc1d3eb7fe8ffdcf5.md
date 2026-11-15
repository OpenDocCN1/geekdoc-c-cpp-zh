The amount of memory that is required for the value type is fixed at compile time and will not change at runtime. This fixed size allows value types to be stored in the area of memory known as the stack.

# Reference Types

In contrast, reference types and the variables that refer to them point to the data storage location (see Figure 8.2). Reference types store the reference (memory address) where the data is located, instead of representing the data directly. Therefore, to access the data, the runtime will read the memory location out of the variable and then dereference it to reach the location in memory that contains the data. The memory area of the data a reference type points to is the heap.

![](bbox=[0.246, 0.396, 0.856, 0.903])

Figure 8.2: Reference Types Point to the Heap