parameters in function definitions to accomplish this. Strings are also one-dimensional

arrays of characters. They will be discussed in the next chapter.

# 6.1 1-D Arrays

1-D arrays refer to one dimensional arrays. Such arrays can be considered as a single

row or column containing a fixed number of elements. They have only one index. An

array is just like a normal variable except for index. Index always start from 0 and end at

(arraySize-1).

A general format for array declaration in C is as follows:

```
Type arrayName [arraySize];
```

Type refers to the data type of array, followed by identifier and in the end array size

enclosed in brackets.

Arrays may be of storage class automatic, static or extern but not register. ANSI C

supports the initialization of all three types of arrays using an initializer but traditional C

only allowed it for static or extern registers.

The general format for initializing 1-D arrays is as follows:

```
Type identifier [size] = {list of elements separated by commas}
```