# # 14 Dynamic Memory Allocation

# **OBJECTIVES**

+   - Implement Function for Dynamic Memory Allocation
- Describe Concept of Linked List

Dynamic memory allocation is a very important and useful feature in C language. So far we have designed programs that contained static allocation of memory. For example, when an array is declared, its size is to be mentioned. Similarly, when an array of structure was created, we mentioned its size at program design time. In real-life scenario, we cannot assume the size of an array to be fixed. This means we cannot decide the memory required at program design time.

Programmer normally allocates maximum size to an array, assuming that the number of elements will not be greater than the specified maximum number. However, the number of elements may change during the execution of a program. When the number of element increases, we need to allocate more memory space to accommodate the additional elements. On the other hand, it is possible that we may not utilize the memory allocated to an array completely, thereby affecting the efficiency of memory space utilization. Such situations can be handled easily with dynamic memory allocation techniques. C provides a powerful and flexible way to manage memory allocation at runtime. It is called dynamic memory allocation. The term dynamic here means that we can specify the size of memory required at runtime. In this Chapter, we will learn about the various functions used for dynamic memory allocation and the concept of linked list.

# ## 14.1 Function for Dynamic Memory Allocation

C language provides a set of standard functions to handle memory allocation effectively. With dynamic memory allocation, the variables of C program can be allocated in the memory as and when needed, and also free the memory allocated to the variable as per the needs of the user. Table 1 lists the library functions available in C language for dynamic memory allocation:

**Table 1: Functions for Dynamic Memory Allocation**

| Function | Purpose |
| :--- | :--- |
| malloc( ) | To allocate memory as per specified size. It returns pointer to the first byte of allocated space. |
| calloc( ) | To allocate memory as per specified size and also initialize them to zero. It returns pointer to the first byte of allocated space. |
| free ( ) | To free previously allocated memory space. |
| realloc( ) | To modify the memory space previously allocated. |