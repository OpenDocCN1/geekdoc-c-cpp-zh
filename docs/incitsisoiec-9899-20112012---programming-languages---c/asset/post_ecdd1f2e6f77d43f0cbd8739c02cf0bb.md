
The aligned_alloc function allocates space for an object whose alignment is specified by alignment, whose size is specified by size, and whose value is indeterminate. The value of alignment shall be a valid alignment supported by the implementation and the value of size shall be an integral multiple of alignment.

## Returns

The aligned_alloc function returns either a null pointer or a pointer to the allocated space.

## 7.22.3.2 The calloc function

### Synopsis

```
#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
```

### Description

The calloc function allocates space for an array of nmemb objects, each of whose size is size. The space is initialized to all bits zero.²296

## Returns

The calloc function returns either a null pointer or a pointer to the allocated space.

## 7.22.3.3 The free function

### Synopsis

```
#include <stdlib.h>
void free(void *ptr);
```

### Description

The free function causes the space pointed to by ptr to be deallocated, that is, made available for further allocation. If ptr is a null pointer, no action occurs. Otherwise, if the argument does not match a pointer earlier returned by a memory management function, or if the space has been deallocated by a call to free or realloc, the behavior is undefined.

## Returns

The free function returns no value.

296 Note that this need not be the same as the representation of floating-point zero or a null pointer constant.

## 7.22.3.4 The malloc function

### Synopsis

```
#include <stdlib.h>
void *malloc(size_t size);
```

### Description

The malloc function allocates space for an object whose size is specified by size and whose value is indeterminate.

### Returns

The malloc function returns either a null pointer or a pointer to the allocated space.

## 7.22.3.5 The realloc function

### Synopsis

```
#include <stdlib.h>
void *realloc(void *ptr, size_t size);
```

### Description

The realloc function deallocates the old object pointed to by ptr and returns a pointer to a new object that has the size specified by size. The contents of the new object shall be the same as that of the old object prior to deallocation, up to the lesser of the new and old sizes. Any bytes in the new object beyond the size of the old object have indeterminate values.

If ptr is a null pointer, the realloc function behaves like the malloc function for the specified size. Otherwise, if ptr does not match a pointer earlier returned by a memory management function, or if the space has been deallocated by a call to the free realloc function, the behavior is undefined. If memory for the new object cannot be allocated, the old object is not deallocated and its value is unchanged.

### Returns

The realloc function returns a pointer to the new object (which may have the same value as a pointer to the old object), or a null pointer if the new object could not be allocated.

## 7.22.4 Communication with the environment

### 7.22.4.1 The abort function

### Synopsis

```
#include <stdlib.h>
_Noreturn void abort(void);
```

### Description

The abort function causes abnormal program termination to occur, unless the signal SIGABRT is being called and the signal handler does not return. Whether open streams with unwritten buffered data are flushed, open streams are closed, or temporary files are removed implementation-defined. An implementation-defined form of the status unsuccessful termination is returned to the host environment by means of the function call raise(SIGABRT).

### Returns

The abort function does not return to its caller.

## 7.22.4.2 The atexit function

### Synopsis

```
#include <stdlib.h>
int atexit(void (*func)(void));
```

### Description

The atexit function registers the function pointed to by be called without arguments at normal program termination.(297) It is unspecified whether a call to the atexit function that does not happen before the exit function is called will succeed.

#### Environmental limits

The implementation shall support the registration of at least 32 functions.

### Returns

The atexit function returns zero if the registration succeeds, nonzero if it fails.

Forward references: the at_quick_exit function (7.22.4.3), the exit function (7.22.4.4).

> 297 The atexit registrations are distinct from the at_exit registrations, so applications may need to call both.

## 7.22.4.3 The at_quick_exit function

### Synopsis

```
#include <stdlib.h>
int at_quick_exit(void (*func)(void));
```

### Description

The at_quick_exit function registers the function pointed to by be called without arguments at normal program termination.(298) It is unspecified whether a call to the at_quick_exit function that does not happen before the at_exit function is called will succeed.

#### Environmental limits

The implementation shall support the registration of at least 32 functions. 

### Returns

The at_quick_exit function returns zero if the registration succeeds, nonzero if it fails.

298 Note that the at_quick_exit registrations are distinct from the at_exit registrations, so applications may need to call both.

## 7.22.4.4 The exit function

### Synopsis

```
#include <stdlib.h>
_Noreturn void exit(int status);
```

### Description

The exit function causes normal program termination to occur. Whether open streams with unwritten buffered data are flushed, open streams are closed, or temporary files are removed implementation-defined. An implementation-defined form of the status unsuccessful termination is returned to the host environment by means of the function call raise(SIGABRT).

First, the exit function calls all functions registered by atexit, in the reverse order of their registration. Then, it calls all functions registered by at_quick_exit, in the reverse order of their registration. Finally, control is returned to the host environment. If the argument does not match a pointer earlier returned by a memory management function, or if the space has been deallocated by a call to free or realloc, the behavior is undefined.

## 7.22.4.5 The _Exit function

### Synopsis

```
#include <stdlib.h>
_Noreturn void _Exit(int status);
```

### Description

The _Exit function causes normal program termination to occur. Whether open streams with unwritten buffered data are flushed, open streams are closed, or temporary files are removed implementation-defined. An implementation-defined form of the status unsuccessful termination is returned to the host environment by means of the function call raise(SIGABRT).

## 7.22.4.6 The getenv function

### Synopsis

```
#include <stdlib.h>
char *getenv(const char *name);
```

### Description

The getenv function searches an environment list, provided by the host environment, for a string that matches the string pointed to. The set of environment names and the method for altering the environment are implementation-defined. The getenv function need not avoid data races with other threads of execution that modify the environment list.

The getenv function returns a pointer to a string associated with the matched member. The string pointed to shall not be modified by the program, but may be overwritten by a subsequent call to getenv. If the specified name cannot be found, a null pointer is returned.

## 7.22.4.7 The quick_exit function

### Synopsis

```
#include <stdlib.h>
Noreturn void quick_exit(int status);
```

### Description

The quick_exit function causes normal program termination to occur. Whether open streams with unwritten buffered data are flushed, open streams are closed, or temporary files are removed implementation-defined. An implementation-defined form of the status unsuccessful termination is returned to the host environment by means of the function call raise(SIGABRT).

The quick_exit function first calls all functions registered by at_quick_exit, in the reverse order of their registration. Then, it calls all functions registered by atexit, in the reverse order of their registration. Finally, control is returned to the host environment. If the value of status is EXIT_SUCCESS, an implementation-defined status is returned. If the value of status is EXIT_FAILURE, an implementation-defined status is returned.
