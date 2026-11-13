arr1 is actually a pointer to memory that is large enough to store 10 ints, rather than a first-class array type. Applying = to arrays is thus an attempt to copy two pointer values rather than the entire array, and with the declaration above, it is illegal, because arr1 is a constant pointer. When arr1 is passed to a function, only the value of the pointer is passed; information about the size of the array is lost. Thus, the size must be passed as an additional parameter. There is no index range checking, since the size is unknown. In the declaration above, the size of the array must be known at compile time. A variable cannot replace 10. If the size is unknown, we must explicitly declare a pointer and allocate memory via new[]. For instance,

```
int *arr2 = new int [ n ];
```

Now arr2 behaves like arr1, except that it is not a constant pointer. Thus, it can be made to point at a larger block of memory. However, because memory has been dynamically allocated, at some point it must be freed with delete[]:

```
delete [ ] arr2;
```

Otherwise, a memory leak will result, and the leak could be significant if the array is large. Built-in C-style strings are implemented as an array of characters. To avoid having to pass the length of the string, the special null-terminator "\0" is used as a character that signals the logical end of the string. Strings are copied by strcpy, compared with strcmp, and their length can be determined by strlen. Individual characters can be accessed by the array indexing operator. These strings have all the problems associated with arrays, including difficult memory management, compounded by the fact that when strings are copied, it is assumed that the target array is large enough to hold the result. When it is not, difficult debugging ensues, often because room has not been left for the null terminator.

The standard vector class and string class are implemented by hiding the behavior of the built-in C-style array and string. Chapter 3 discusses the vector class implementation. It is almost always better to use the vector and string class, but you may be forced to use the C-style when interacting with library routines that are designed to work with both C and C++. It is also occasionally necessary (but this is rare) to use the C-style in a section of code that must be optimized for speed.

# 1.6 Templates

Consider the problem of finding the largest item in an array of items. A simple algorithm is the sequential scan, in which we examine each item in order, keeping track of the maximum. As is typical of many algorithms, the sequential scan algorithm is type independent. By type independent, we mean that the logic of this algorithm does not depend on the type of items that are stored in the array. The same logic works for an array of integers, floating-point numbers, or any type for which comparison can be meaningfully defined. Throughout this text, we will describe algorithms and data structures that are type independent. When we write C++ code for a type-independent algorithm or data structure, we would prefer to write the code once rather than recode it for each different type.