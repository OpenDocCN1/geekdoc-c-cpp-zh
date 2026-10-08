# 12.8. Advanced Pointer Concepts

The code starts by declaring an integer pointer ptr and an integer variable a. Then, it dynamically allocates memory for an integer using malloc() and assigns the address of the allocated memory to ptr.

After allocating memory, the code stores the value 33 into the memory location pointed to by ptr using the dereferencing operator *ptr. See Fig. 12.4.

![](bbox=[0.185, 0.196, 0.715, 0.283])

Next, the program assigns the address of the variable a to ptr. This action causes the pointer to no longer point to the dynamically allocated memory, resulting in memory leak because the previously allocated memory is not freed. See Fig. 12.5.

![](bbox=[0.215, 0.419, 0.715, 0.513])

Finally, the program attempts to free memory using the free() function. However, since ptr now holds the address of a stack variable (a), it leads to an undefined behavior because the memory was not dynamically allocated.

This scenario creates a memory leak because the originally allocated memory is no longer accessible or usable, but it is not released. Additionally, attempting to free the memory causes an undefined behavior, as free() is intended for dynamically allocated memory, not stack variables.

Another example of a dangling pointer occurs when trying to access memory that has already been deallocated, as shown below:

```
int *ptr = malloc(sizeof(int));
*ptr = 10;
free(ptr);
*ptr = 20; // ptr is now
```

In this example, ptr is dynamically assigned memory, then deallocated using free(), making it a dangling pointer. Attempting to access the memory location pointed to by ptr after deallocation can lead to unpredictable behavior.

To prevent dangling pointers, make sure to initialize pointers properly and set them to NULL after deallocating memory. Avoid using pointers after freeing the