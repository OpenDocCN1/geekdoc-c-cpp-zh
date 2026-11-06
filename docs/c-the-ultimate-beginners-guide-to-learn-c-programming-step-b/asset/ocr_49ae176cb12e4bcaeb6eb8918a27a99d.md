When an array has been declared, it doesn’t mean that it has already been initialized in the memory. After initializing an array, it is possible to assign values to it.

Array initialization can be done at the time of its declaration using the *new* keyword. When this keyword is used, an instance of the array is created. This is demonstrated below:

```
public class MyArray
public static void Main()
{
    int[] intArray_1 = new int[4];

    int[] intArray_2 = new int[4]{10, 20, 30, 40};

    int[] intArray_3 = {10, 20, 30, 40};
}
}
```

First, we have declared an array to store 4 integers. Note that the specification of the array size has been done within the square brackets. We have also done the same thing in our second statement, but values have also been assigned to the indices within the curly braces {}. In the third statement, we have declared an array and assigned values to it without specifying its size.

# Late Initialization

It is possible for us to initialize an array after it has been declared. This means that it is not a must for us to do both the declaration and the initialization of an array at the same time. Here is an example:

```
using System;
public class MyArray
{
    public static void Main()
    {
        string[] array1, array2;
```