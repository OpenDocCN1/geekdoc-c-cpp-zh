
Nesting of function calls is also possible. For example, a statement like

```
p = mul(mul(5,2),6);
```

is valid. This represents two sequential function calls. The inner function call is evaluated first and the returned value is again used as an actual argument in the outer function call. If mul returns the product of its arguments, then the value of p would be 60 (= 5 × 2 × 6).

## 10.13 RECURSION

When a called function in turn calls another function a process of 'chaining' occurs. Recursion is a special case of this process, where a function calls itself. A very simple example of recursion is presented below:

```
main()
{
    printf("This is an example of recursion\n");
    main();
}
```

When executed, this program will produce an output something like this:

This is an example of recursion
This is an example of recursion
This is an example of recursion
This is an ex

Execution is terminated abruptly; otherwise the execution will continue indefinitely.

Another useful example of recursion is the evaluation of factorials of a given number. The factorial of a number n is expressed as a series of repetitive multiplications as shown below:

factorial of n = n(n-1)(n-2)....1.

For example,

factorial of 4 = 4 × 3 × 2 × 1 = 24

A function to evaluate factorial of n is as follows:

```
factorial(n)
int n;
{
    int fact;
    if (n==1)
        return(1);
    else
        fact = n*factorial(n-1);
        return(fact);
}
```

Let us see how the recursion works. Assume n = 3. Since the value of n is not 1, the statement

```
fact = n * factorial(n-1);
```

will be executed with n = 3. That is,

```
fact = 3 * factorial(2);
```

will be evaluated. The expression on the right-hand side includes a call to factorial with n = 2. This call will return the following value:

```
2 * factorial(1)
```

Once again, factorial is called with n = 1. This time, the function returns 1. The sequence of operations can be summarized as follows:

```
fact = 3 * factorial(2)
= 3 * 2 * factorial(1)
= 3 * 2 * 1
= 6
```

Recursive functions can be effectively used to solve problems where the solution is expressed in terms of successively applying the same solution to subsets of the problem. When we write recursive functions, we must have an if statement somewhere to force the function to return without the recursive call being executed. Otherwise, the function will never return.

## 10.14 FUNCTIONS WITH ARRAYS

Like the values of simple variables, it is also possible to pass the values of an array to a function. To pass an array to a called function, it is sufficient to list the name of the array, without any subscripts, and the size of the array as arguments. For example, the call

```
largest(a,n);
```

will pass all the elements contained in the array a of size n. The called function expecting this call must be appropriately defined. The largest function header might look like:

```
float largest(array, size)
float array[];
int size;
```

The function largest is defined to take two arguments, the array name and the size of the array to specify the number of elements in the array. The declaration of the formal argument array is made as follows:

```
float array[];
```

The pair of brackets informs the compiler that the argument array is an array of numbers. It is not necessary to specify the size of the array here.

Let us consider a problem of finding the largest value in an array of elements. The program is as follows:

```
main()
{
    float largest();
    static float value[4] = {2.5, -4.75, 1.2, 3.67};
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

### Example 10.5

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
{
float value[SIZE], std_dev();
int i;
printf("Enter %d float values\n", SIZE);
for(i=0; i < SIZE; i++)
scanf("%f", &value[i]);
printf("Std deviation is %f\n", std_dev(value, SIZE));
}
float std_dev(a,n)
float a[];
int n;
{
int i;
float mean(), x = 0.0;
x = mean(a,n);
for(i=0; i < n; i++)
sum += (x-a[i])*(x-a[i]);
return(sqrt(sum/(float)n));
}
float mean(a,n)
float a[];
int n;
{
int i;
float sum = 0.0;
for(i=0; i < n; i++)
sum = sum + a[i];
return(sum/(float)n);
}
```

```
Output
Enter 5 float values
35.0 67.0 79.5 14.20 55.75
Std.deviation is 23.231582
```

Fig. 10.11 Passing of arrays to a function

However, this does not apply when an individual element is passed as argument. Example 10.6 highlights these concepts.

### Example 10.6

Write a program that uses a function to sort an array of integers.

A program to sort an array of integers using the function sort() is given in Fig. 10.12. Its output clearly shows that a function can change the values in an array passed as argument.

```
Program
/------------------------------------------------------------
/ SORTING OF ARRAY ELEMENTS
------------------------------------------------------------
main()
{
int i ;
static int marks[5] = {40, 90, 73, 81, 35};
printf("Marks before sorting\n");
for(i = 0; i < 5; i++)
    printf("%d", marks[i]);
printf("\n");
sort(5, marks);
printf("Marks after sorting\n");
for(i = 0; i < 5; i++)
    printf("%4d", marks[i]);
printf("\n");
}
sort(m,x)
int m, x[];
{
    int i, j, t;
    for(i = 1; i < m-1; i++)
        for(j = 1; j <= m-i; j++)
            if(x[j-1]>x[j])
            {
                t = x[j-1];
                x[j-1] = x[j];
                x[j] = t;
            }
}
Output
Marks before sorting
40 90 73 81 35
Marks after sorting
35 40 73 81 90
```

Fig. 10.12 Sorting of array elements using a function

## 10.15 THE SCOPE AND LIFETIME OF VARIABLES IN FUNCTIONS— STORAGE CLASSES

Variables in C differ in behaviour from those in most other languages. For example, in a BASIC program, a variable retains its value throughout the program. It is not always the case in C. It all depends on the ‘storage’ class a variable may assume.

As mentioned earlier, a variable in C can have any one of the four storage classes:

- 1. Automatic variables
- 2. External variables
- 3. Static variables
- 4. Register variables

We shall briefly discuss the scope and longevity of each of the above class of variables. The scope of variable determines over what part(s) of the program a variable is actually available for use (active). Longevity refers to the period during which a variable retains a given value during execution of a program (alive). So longevity has a direct effect on the utility of a given variable.

The variables may also be broadly categorized, depending on the place of their declaration, as internal (local) or external (global). Internal variables are those which are declared within a particular function, while external variables are declared outside of any function.
