The next section discusses the function free.

# Function free

Compilers use a mechanism of automatic memory management called garbage collection to free unwanted or unused memory space that has been allocated at compile time. The availability of an identifier within a program is governed by the storage class of the identifier as discussed in Chapter 8. This storage class is also used at the time of garbage collection to identify whether a memory block can be freed or not. When we allocate memory dynamically at runtime the responsibility to free unwanted or used memory space lays with programmer. Managing of memory space is more required when we have limited storage, in such cases unwanted or unused memory blocks should be freed as soon as possible. The syntax to use the function free is as follows:

```
free(ptr);
```

The preceding syntax, when used, will free a memory block within the heap that is associated with pointer *ptr*. After the compiler frees the memory block the pointer ptr is assigned a NULL value.

# 14.2 Concept of Linked List

We have seen that an array allocates contiguous bytes of memory for all its elements as a one block. Even when the dynamic memory allocation function is used, the entire block is to be contiguous in memory. Can we write a program that may store each element of array at different places in memory? The answer is yes. Then a next question that arises is how to keep track of individual addresses of each memory. With the knowledge of pointers and structures, which we have already discussed, a linked list can be created within a C program. A linked list allocates space for each element separately in its own block of memory called a *linked list element* or *node*. As discussed earlier in Chapter 11, an array of structures can also be created within a C program. Thus, in this case, each node will be a structure. Pointers will be used to connect each node of the list. All nodes in a link list create a linking between each other similar to a chain. Each node will contain an address of another node. Figure 5 illustrates the view of linked list:

![](bbox=[0.23, 0.66, 0.87, 0.74])

To create a linked list, a structure is to be declared. Each node in a linked list is actually a structure. The structure will contain data items similar to the structure declared earlier in Chapter 11. However, it will contain an additional item. This additional item is a pointer variable of type structure node. Thus, it will be a nested structure. When a new node will be added to the list, the pointer variable will hold address of the new added structure. Such a structure can be represented as follows: