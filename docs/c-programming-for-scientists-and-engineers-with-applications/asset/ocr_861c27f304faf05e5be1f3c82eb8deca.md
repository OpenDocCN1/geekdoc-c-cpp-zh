The array element a[4] is passed by value. If the value of the parameter in the function is changed the change will not be reflected in the argument in the calling function.

```
#define ARSIZE 10
void funccomp( int *x); /* function prototype */
int i, a[5] = { 2, 3, 4, 5, 6 }; /* array declaration and initialization */
funccomp(&a[4]); /* function call */
void funccomp(int *x) /* function header and body */
{
  .
  return;
}
```

Here the array element a[4] is passed by address and picked up by a pointer variable. If the value of the parameter in the function is changed the change will be reflected in the argument in the calling function.

# Exercises

+   1. Write a program to input 100 values into an array a[100]. Compute the count, sum, and average of positive numbers and the count, sum, and average of negative numbers. Output the array, ten numbers per row, the count, sum, and the average of the positive and negative numbers.
2. Write a program to generate 500 numbers in the range of 1 to 20 using the random generator. Count the number of times each number occurs in this set and print the numbers and their frequencies. Use an array to store the numbers.
3. Write a program to generate the Cartesian coordinates from polar coordinates for a circle with radius $r$ and the angle $\theta$ in the increments of $5^{\circ}$. Store the $x$ and $y$ coordinate values in one-dimensional arrays. The formula for the conversion of polar coordinates to Cartesian coordinates is as follows:

```
x = r \cos \theta\ny = r \sin \theta
```