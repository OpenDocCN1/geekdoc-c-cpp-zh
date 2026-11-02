# Common Error 7.4

# Memory Leaks

Another very common pointer error is to allocate memory on the free store and never deallocate it. A memory block that is never deallocated is called a **memory leak.**

If you allocate a few small blocks of memory and forget to deallocate them, this is not a huge problem. When the program exits, all allocated memory is returned to the operating system.

But if your program runs for a long time, or if it allocates lots of memory (perhaps in a loop), then it can run out of memory. Memory exhaustion will cause your program to crash. In extreme cases, the computer may freeze up if your program exhausted all available memory. Avoiding memory leaks is particularly important in programs that need to run for months or years, without restarting, and in programs that run on resource-constrained devices such as cell phones.

Even if you write short-lived programs, you should make it a habit to avoid memory leaks. Make sure that every call to the new operator has a corresponding call to the delete operator.

Every call to new should have a matching call to delete.

![](bbox=[0.75, 0.22, 0.95, 0.47])

Be sure to recycle any free store memory that your program no longer needs.

# 7.5 Arrays and Vectors of Pointers

When you have a sequence of pointers, you can place them into an array or vector. An array and a vector of ten int* pointers are defined as

```
```cpp
int* pointer_array[10];
vector<int*> pointer_vector(10);
```
```

The expression pointer_array[i] or pointer_vector[i] denotes the pointer with index i in the sequence.

One application of such pointer sequences are two-dimensional arrays in which each row has a different length, such as the triangular array shown in Figure 8.

![](bbox=[0.35, 0.8, 0.85, 0.95])

Figure 8 A Triangular Array