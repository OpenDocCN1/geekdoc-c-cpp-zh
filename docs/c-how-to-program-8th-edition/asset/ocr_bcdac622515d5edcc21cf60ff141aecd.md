```
```c
// call signal and pass it SIGINT and address of signalHandler
signal(SIGINT, signalHandler);
} // end function signalHandler
```
```

```
```text
 1   2   3   4   5   6   7   8   9  10
11  12  13  14  15  16  17  18  19  20
21  22  23  24  25  26  27  28  29  30
31  32  33  34  35  36  37  38  39  40
41  42  43  44  45  46  47  48  49  50
51  52  53  54  55  56  57  58  59  60
61  62  63  64  65  66  67  68  69  70
71  72  73  74  75  76  77  78  79  80
81  82  83  84  85  86  87  88  89  90
91  92  93  94  95  96  97  98  99
Interrupt signal (2) received.
Do you wish to continue (1 = yes or 2 = no)? 1
100
```
```

```
```text
 1   2   3   4
Interrupt signal (2) received.
Do you wish to continue (1 = yes or 2 = no)? 2
```
```

**Fig. F.6** | Using signal handling. (Part 2 of 2.)

# F.10 Dynamic Memory Allocation with calloc and realloc

In Chapter 11, we discussed C++-style dynamic memory allocation with new and delete. C++ programs should use new and delete, rather than C’s functions `malloc` and `free` (header `<cstdlib>`). However, most C++ programmers will find themselves reading a great deal of C legacy code, and therefore we include this additional discussion on C-style dynamic memory allocation.

The general utilities library (`<cstdlib>`) provides two other functions for dynamic memory allocation—`calloc` and `realloc`. These functions can be used to create and modify dynamic arrays. As shown in Chapter 8, a pointer to an array can be subscripted like an array. Thus, a pointer to a contiguous portion of memory created by `calloc` can be manipulated as an array. Function `calloc` dynamically allocates memory for an array and initializes the memory to zeros. The prototype for calloc is

```
```cpp
void *calloc( size_t nmemb, size_t size );
```
```

It receives two arguments—the number of elements (`nmemb`) and the size of each element (`size`)—and initializes the elements of the array to zero. The function returns a pointer to the allocated memory or a null pointer (0) if the memory is not allocated.

Function `realloc` changes the size of an object allocated by a previous call to `malloc`, `calloc` or `realloc`. The original object’s contents are not modified, provided that the memory allocated is larger than the amount allocated previously. Otherwise, the contents are unchanged up to the size of the new object. The prototype for realloc is

```
```cpp
void *realloc( void *ptr, size_t size );
```
```