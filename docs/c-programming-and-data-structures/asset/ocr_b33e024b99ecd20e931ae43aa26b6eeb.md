```
max = a[i];
return(max);
}
```

When the function call largest(value,4) is made, the values of all elements of array value become the corresponding elements of array a in the called function. The largest function finds the largest value in the array and returns the result to the main.

In C, the name of the array represents the address of its first element. By passing the array name, we are, in fact, passing the address of the array to the called function. The array in the called function now refers to the same array stored in the memory. Therefore, any changes in the array in the called function will be reflected in the original array.

Passing addresses of parameters to the functions is referred to as pass by address (or pass by pointers). Note that we cannot pass a whole array by value as we did in the case of ordinary variables.

# EXAMPLE 5.5

Write a program to calculate the standard deviation of an array of values. The array elements are read from the terminal. Use functions to calculate standard deviation and mean.

Standard deviation of a set of n values is given by

S.D. = sqrt( (1/n) * sum_{i=1}^{n} (x̄ - x_i)^2 )

where x̄ is the mean of the values.

```
Program
#include <math.h>
#define SIZE 5
float std_dev(float a[], int n);
float mean (float a[], int n);
main ()
{
    float value[SIZE];
    int i;
    printf("Enter %d float values\n", SIZE);
    for (i=0; i < SIZE; i++)
        scanf("%f", &value[i]);
    printf("Standard deviation is %f\n", std_dev(value,SIZE));
}
float std_dev(float a[], int n)
{
    int i;
    float x, sum = 0.0;
    x = mean (a,n);
    for(i=0; i < n; i++)
        sum += (x-a[i])*(x-a[i]);
    return(sqrt(sum/(float)n));
}
float mean(float a[],int n)
```