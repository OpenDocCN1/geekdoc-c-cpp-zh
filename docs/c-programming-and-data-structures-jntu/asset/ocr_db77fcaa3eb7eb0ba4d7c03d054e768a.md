# 10.24 C Programming and Data Structures

```
printf("%f\n", largest(value,4));
}
float largest(a,n)
float a[];
int n;
{
int i;
float max;
max = a[0];
for(i = 1; i < n; i++)
if(max < a[i])
max = a[i];
return(max);
}
```

When the function call largest(value, 4) is made, the values of all elements of the array value are passed to the corresponding elements of array a in the called function. The largest function finds the largest value in the array and returns the result to the main.

# Example 10.5

Write a program to calculate the standard deviation of an array of values. The array elements are read from the terminal. Use functions to calculate standard deviation and mean.

S.D. = \sqrt{\frac{1}{n} \sum_{i=1}^n (\bar{x} - x_i)^2}
where \bar{x} is the mean of the values.

A multifunction program consisting of main, std-dev, and mean functions is shown in Fig. 10.11. main reads the elements of the array value from the terminal and calls the function std-dev to print the standard deviation of the array elements. std-dev, in turn, calls another function mean to supply the average value of the array elements. Both std-dev and mean are defined as floats and therefore they are declared as floats in the declaration part of their calling functions.

When dealing with array arguments, we should remember one major distinction. If a function changes the values of array elements, then these changes will be made to the original array that passed to the function. When an entire array is passed as an argument, the contents of the array are not copied into the formal parameter array; instead, information about the addresses of array elements are passed on to the function. Therefore, any changes introduced to the array elements are truly reflected in the original array in the calling function.

```
Program
/*
 FUNCTIONS WITH ARRAYS
 */
#include <math.h>
#define SIZE 5
main()
```