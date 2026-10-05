# C Language: Arrays

An array is a collection of variables of the same type that are referred through a common name. A specific element in an array is accessed through an index. In C and C+, arrays consist of contiguous memory locations. The lowest address corresponds to the first element of the array and the highest address to the last element. Arrays may have from one to several dimensions. The most common array is the null-terminated string, which is simply a sequence of characters enclosed in quotation marks terminated by a null character ('\0').

# Single Dimensional Arrays

These types of arrays are specified with the following syntax:

```
type name[size];
```

Here, type declares the type of the array, which is the type of each element of the array, and size defines the number of elements that the array will hold. Arrays must be explicitly declared so that the compiler can allocate space for them in memory. Here is an example:

```
int flowers[5];
```

Array elements are accessed with the bracket operator ([]) and an index value which starts at zero and ranges up to not including the size of the array. The index 0 refers to the first element of the array:

```
int p = flowers[0];
int p = flowers[2]; // third array element
```