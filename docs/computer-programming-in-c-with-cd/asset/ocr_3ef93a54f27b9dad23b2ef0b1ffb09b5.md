![](bbox=[0.22, 0.161, 0.845, 0.219])

Then, the address of the first element of this array can be represented by using the following code snippet:

```
```cpp
&arr[0]; // we have used address operator to denote the address of first element
```
```

Alternatively, any element of the array can be represented by using the following code snippet:

```
```cpp
&arr[i]; // for any element at the given index location denoted by i
```
```

Now, declare an integer pointer variable by using the following code snippet:

```
```cpp
int * ptr; // an integer pointer
```
```

After declaring the integer pointer variable, we can explicitly assign the address of the first element or any other element of array to the newly created pointer variable by using the following code snippet:

```
```cpp
ptr = &arr[0];               //ptr points to address of arr[0]
```
```

or,

```
```cpp
ptr = &arr[i]; points the address elements referenced by i
```
```

Moreover, you can also assign the address of first element on an array to a pointer variable, just by passing the name of array or we can say without specifying any index number by using the following code snippet:

```
```cpp
ptr = arr;                   //ptr points to address of arr[0]
```
```

In C++, you can use the array name as well as pointer to array to access and manipulate the values of array elements. However, the working of arrays and pointers is quite different. Since pointers are variables, which can be manipulated by using operators (+, -, ++, --); whereas, arrays being a linear collection of variables cannot be manipulated by using operations such as arr++, where arr is the name of the array. Listing 7 shows how to handle an array by using pointer (you can find the ArrayPointer.cpp file on the CD in the code\chapter4 folder):

# ▶ Listing 7: Handling Array by Using Pointer

```
```cpp
#include<iostream.h>
void main()
```
```