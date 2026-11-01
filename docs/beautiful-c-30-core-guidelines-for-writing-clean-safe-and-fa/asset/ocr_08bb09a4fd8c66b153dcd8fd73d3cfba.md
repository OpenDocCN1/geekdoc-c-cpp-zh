memory is meaningless. Also, by tak-ing a void*, the function is discarding information known at the call site: the type of object.

We can fix this immediately by jumping to C++ and exchanging the void* for a template parameter:

Click here to view code image

```
template <typename T>
void sort(T* base, size_t num, size_t size,
    int(*comp)(const T*, const T*));
```

This optimization improves the design by catching a typical error at compile time rather than runtime: passing a nonsensical comparison function. A void* can point to anything at all, while a T* must point to an instance of T. If you had a set of float-ing-point values that you wanted to sort, and your comparison function sorted char-acters, a call to sort may yield the wrong result.

Next, consider the two size_t parameters. First, they are an accident waiting to happen. The client must take care to pass these parameters in the correct order; they will get no warning from the compiler if they get this wrong. However, the size parameter is now redundant. Since the type being sorted is now part of the function signature, the size is known at compile time. The signature now looks like this:

Click here to view code image

```
template <typename T>
void sort(T* base, size_t num, int(*comp)(const
T*, const T*));
```

Specializing the function over the type gives the compiler more information. There may be optimizations available if the total volume of memory occupied by the objects being sorted is less than, for example, the size of the L1 cache.

The final parameter is a function pointer. This is a callback function. The sort function will invoke this when it needs to decide the order of two objects. Optimiza-tions are hard to come by here, but since sort is now a