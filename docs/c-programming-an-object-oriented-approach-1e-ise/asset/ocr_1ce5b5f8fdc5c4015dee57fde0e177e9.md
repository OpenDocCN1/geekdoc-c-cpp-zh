The first line of output shows the original array; the second line shows the array after modification.

# **No Returning Array from Function**

C++ does not allow us to return an array from a function. In other words, we cannot have a function prototype such as the following.

```
~~~cpp
type [] function (const type array [], int size);    // It is not allowed in C++
~~~
```

When passing arrays to function, we have three choices as shown below:

```
~~~cpp
// array will not change.
void (const type array [], int size);
// array will change.
void (type array [], int size);
// array1 will not change, but array 2 can be modified version of array1.
void (const type array1 [], type array2 [], int size);
~~~
```

> > To simulate returning an array from a function, we can use two arrays (one constant and one nonconstant).

# **EXAMPLE 8.13**

Assume we want to write a function to reverse the contents of an array without changing the original array. This is possible if we create two similar arrays, the original and the modified one (which can originally be empty) as shown in Program 8.8. Note that we print both the original and modified arrays.

# **Program 8.8** Simulating array return by passing two arrays

```
~~~cpp
1 /***********************************************************
2  * Passing two array to a function simulating returning an array.
3  ***********************************************************/
4 #include <iostream>
5 using namespace std;
6 /***********************************************************
7  * Function reverse is a function that takes two arrays. It uses
8  * the first array to reverse the element in the second array.
9  ***********************************************************/
10 void reverse (const int array1[], int array2[], int size)
11 {
12   for (int i = 0, j = size - 1; i < size; i++, j--)
13   {
14     array2[j] = array1[i];
15   }
16   return;
17 }
~~~
```