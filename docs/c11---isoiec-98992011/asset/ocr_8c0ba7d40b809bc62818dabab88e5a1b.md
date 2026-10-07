# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.26 Threads <threads.h>

# 7.26.1 Introduction

+   1 The header <threads.h> includes the header <time.h>, defines macros, and declares types, enumeration constants, and functions that support multiple threads of execution. ³¹¹⁵

+   2 Implementations that define the macro __STDC_NO_THREADS__ need not provide this header support any of its facilities.

+   3 The macros are
```cpp
thread_local
```
expands to _Thread_local;
```cpp
ONCE_FLAG_INIT
```
expands to a value that can be used to initialize an object of type once_flag; and
```cpp
TSS_DTOR_ITERATIONS
```
expands to an integer constant expression representing the maximum number of times that destructors will be called when a thread terminates.

+   4 The types are
```cpp
cnd_t
```
which is a complete object type that holds an identifier for a condition variable;
```cpp
thrd_t
```
which is a complete object type that holds an identifier for a thread;
```cpp
tss_t
```
which is a complete object type that holds an identifier for a thread-specific storage pointer;
```cpp
mtx_t
```
which is a complete object type that holds an identifier for a mutex;
```cpp
tss_dtor_t
```
which is the function pointer void (*) (*), used for a destructor for a thread-specific storage pointer;

> ³¹⁵ See “future library directions” (7.31.15).

376

Library

7.26.1