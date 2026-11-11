![](bbox=[0.447, 0.026, 0.55, 0.442])

That is how we can access the elements. The *array[1/2,1]* returns the element located at row 2 and column 1 of the array.

# Jagged Arrays

A jagged array is simply an array of arrays. These arrays are storing arrays instead of data type values directly. To initialize a jagged array, we use two square brackets [][]. In the first bracket, we specify the size of the array while in the second bracket, we specify the dimension of the array which is to be stored as values. Here is an example to show the declaration and initialization of a jagged array:

```
using System;
public class MyArray
{
public static void Main()
{
int[][] jaggedArray = new int[2][];

jaggedArray[0] = new int[4]{1, 2, 3, 4};
```