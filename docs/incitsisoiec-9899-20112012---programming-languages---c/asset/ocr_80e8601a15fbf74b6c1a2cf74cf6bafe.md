The aligned_alloc function allocates space for an object whose alignment is specified by alignment, whose size is specified by size, and whose value is indeterminate. The value of alignment shall be a valid alignment supported by the implementation and the value of size shall be an integral multiple of alignment.

# Returns

The aligned_alloc function returns either a null pointer or a pointer to the allocated space.

# 7.22.3.2 The calloc function

# Synopsis

```
#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
```

# Description

The calloc function allocates space for an array of nmemb objects, each of whose size is size. The space is initialized to all bits zero.²96

# Returns

The calloc function returns either a null pointer or a pointer to the allocated space.

# 7.22.3.3 The free function

# Synopsis

```
#include <stdlib.h>
void free(void *ptr);
```

# Description

The free function causes the space pointed to by ptr to be deallocated, that is, made available for further allocation. If ptr is a null pointer, no action occurs. Otherwise, if the argument does not match a pointer earlier returned by a memory management function, or if the space has been deallocated by a call to free or realloc, the behavior is undefined.

# Returns

The free function returns no value.

296 Note that this need not be the same as the representation of floating-point zero or a null pointer constant.