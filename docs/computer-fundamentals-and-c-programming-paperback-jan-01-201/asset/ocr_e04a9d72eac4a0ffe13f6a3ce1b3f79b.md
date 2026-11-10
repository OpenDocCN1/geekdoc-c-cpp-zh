The second **return** statement provides the connecting link between successive calls. Each call to **add_array** increments first by one, so the next array element becomes the first element for that call. In the base case, the termination condition (`first == last`) evaluates to true and returns the last element. This initiates the return of the other pending calls, where each call adds its “first element” to this value. Eventually, when the first call returns, all elements defined by **first** and **last** have been added. This is how the function can be invoked from **main**:

```
```c
#include <stdio.h>
short add_array(short arr[], short first, short last);
int main(void)
{
    short arr[10] = {1, 3, 5, 7, 9, 12, 14, 16, 18, 20};
    short first = 0, last = 9;
    printf("Sum of elements %hd to %hd = %hd\n",
           first, last, add_array(arr, first, last));
    return 0;
}
```
```

The program outputs 105, the sum of all ten elements. For an array of a few hundred elements, adopting an iterative solution won’t result in significant savings. But before adding a million elements, you have to choose between using a million recursive calls or a single iterative one. (The choice is actually obvious.)

# 11.14.2  Computing the Power of a Number Recursively

We developed an iterative version of the **power** function in Program 11.9. This function can also be implemented using recursion because the *n*th power of a number can be described in terms of the (*n* - 1)th power of the same number. In other words, `power(2, 10) = 2 * power(2, 9)`. This relationship is implemented with the following code:

```
```c
long power(short base, short exponent)
{
    long result;
    if (exponent == 1)
        result = base;
    else
        result = power(base, exponent - 1) * base;
    return result;
}
```
```

Because each call to **power** reduces the exponent by one, repeated calls will eventually lead to the base case, **power(2, 1)**, where the terminating condition stops further recursion. Here, the second assignment to **result** provides the connecting link between successive calls.

# 11.14.3  Using Recursion to Compute Fibonacci Numbers

Section 8.3.3 adopted an iterative approach for deriving the terms of the Fibonacci sequence. To recall briefly, a Fibonacci sequence starts with the numbers 0 and 1, but every subsequent term is formed by summing the previous two. Here are the first 10 terms of the sequence: