© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

# Returns

4 The **strand** function returns no value.

5 EXAMPLE The following functions define a portable implementation of **rand** and **strand**.

```
static unsigned long int next = 1;
int rand(void)      // RAND_MAX assumed to be 32767
{
    next = next * 110351245 + 12345;
    return (unsigned int)(next/65536) % 32768;
}
void strand(unsigned int seed)
{
    next = seed;
}
```

# 7.22.3 Memory management functions

The order and continuity of storage allocated by successive calls to the **aligned_alloc**, **malloc**, and **realloc** functions is unspecified. The pointer returned if the allocation succeeds is suitably assigned so that it may be assigned to a pointer to any object with a fundamental alignment requirement and then used to access such an object or array of objects in the space (until the space is explicitly declared). The lifetime of an allocated object extends from the allocation until the deallocation. Each allocation shall yield a pointer to an object disjoint from any other object. The pointer returned points to the start (lowest address) of the allocated space. If the size of the space requested is zero, the behavior is implementation-defined: either a null pointer is returned, or the behavior is as if the size were nonzero value, except that the returned pointer shall not be used to access an object.

For purposes of determining the existence of a data race, memory allocation functions behave as though they accessed memory locations accessible through their arguments and no other static duration. These functions may, however, visibly modify the state they allocate or deallocate. Each call to **free** or **realloc** deallocates a region $p$ of memory synchronizes with any allocation that allocates all or part of the region $p$. This synchronization occurs after any access of $p$ by the allocating function.

# 7.22.3.1 The aligned_alloc function

# Synopsis

```
#include <stdlib.h>
void *aligned_alloc(size_t alignment, size_t size);
```

§7.22.3.1

Library

347