```
```cpp
delete timePtr;
```
```

This statement first calls the destructor for the object to which `timePtr` points, then deallocates the memory associated with the object, returning the memory to the free store.

![](bbox=[0.119, 0.326, 0.192, 0.381])

# Common Programming Error 10.1

*Not releasing dynamically allocated memory when it’s no longer needed can cause the system to run out of memory prematurely. This is sometimes called a “**memory leak**.”*

![](bbox=[0.118, 0.584, 0.191, 0.638])

# Error-Prevention Tip 10.1

*Do not delete memory that was not allocated by new. Doing so results in undefined behavior.*

![](bbox=[0.118, 0.811, 0.191, 0.866])

# Error-Prevention Tip 10.2