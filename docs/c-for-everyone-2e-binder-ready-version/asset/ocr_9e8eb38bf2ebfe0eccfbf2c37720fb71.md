```
```cpp
int primes[] = { 2, 3, 5, 7, 11 };
int* p = grow(primes, 5);
```
```

20. Consider the grow function of Self Check 19. What must its caller remember to do?

**Practice It** Now you can try these exercises at the end of the chapter: R7.19, R7.21, P7.10.

# ### Common Error 7.3

![](bbox=[0.15, 0.33, 0.25, 0.41])

# **Dangling Pointers**

> > Using a dangling pointer (a pointer that points to memory that has been deleted) is a serious programming error.

A very common pointer error is to use a pointer that points to memory that has already been deleted. Such a pointer is called a **dangling pointer**. Because the freed memory will be reused for other purposes, you can create real damage by using a dangling pointer. Consider this example:

```
```cpp
int* values = new int[n];
// Process values
delete[] values;
// Some other work
values[0] = 42;
```
```

This code will compile since the compiler does not track whether a pointer points to a valid memory location. However, the program may run with unpredictable results. If the program calls the `new` operator anywhere after deleting values, that call may allocate the same memory again. Now some other part of your program accesses the memory to which `values` points, and that program part will malfunction when you overwrite the memory. This can happen even if you don't see any call to `new`—such calls may occur in library functions.

*Never* use a pointer that has been deleted. Some programmers take the precaution of setting all deleted pointers to `NULL`:

```
```cpp
delete[] values;
values = NULL;
```
```

This is not perfect protection—you might have saved `values` into another pointer variable—but it is a reasonable precaution.

# ### Common Error 7.4

![](bbox=[0.15, 0.77, 0.25, 0.85])

# **Memory Leaks**

Another very common pointer error is to allocate memory on the heap and never deallocate it. A memory block that is never deallocated is called a **memory leak**.

If you allocate a few small blocks of memory and forget to deallocate them, this is not a huge problem. When the program exits, all allocated memory is returned to the operating system.

> > Every call to `new` should have a matching call to `delete`.

But if your program runs for a long time, or if it allocates lots of memory (perhaps in a loop), then it can run out of memory. Memory exhaustion will cause your program to crash. In extreme cases, the computer may freeze up if your program exhausted all available memory. Avoiding memory leaks is particularly important in programs that need to run for months or years, without restarting, and in programs that run on resource-constrained devices such as cell phones.

Even if you write short-lived programs, you should make it a habit to avoid memory leaks. Make sure that every call to the `new` operator has a corresponding call to the `delete` operator.