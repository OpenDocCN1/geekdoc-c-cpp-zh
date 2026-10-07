# LESSON 16 Pointers to Functions and Linked Lists

FIGURE 16.4
Adding a new first element to an existing list.

![](bbox=[0.278, 0.127, 0.863, 0.243])

![](bbox=[0.278, 0.315, 0.863, 0.429])

Notice `malloc()` is used to allocate the memory for the new element. As each new element is added, only the memory needed for it is allocated. The `calloc()` function could also be used. You should be aware of the differences between these two functions. The main difference is that `calloc()` will initialize the new element; `malloc()` will not.

> CAUTION
In this code fragments, the return value of `malloc()` is not checked to ensure that the memory was successfully allocated. In a real program, you should always check the return value of a memory allocation function.

> TIP
You should always initialize pointers to `NULL` when you declare them. Never leave a pointer uninitialized. Doing so is just asking for trouble.

# Adding an Element to the End of the List

To add an element to the end of a linked list, you start at the head pointer and go through the list until you find the last element. After you've found it, follow these steps:

+   1. Create an instance of your structure, allocating memory space using `malloc()`.