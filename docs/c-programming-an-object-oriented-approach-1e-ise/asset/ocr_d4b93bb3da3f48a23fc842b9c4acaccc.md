value-returning recursive function. In the case of a void recursive function, general cases are continuously called until a base case is reached; the general case does not have to hold any information. In the case of a value-returning function, the general cases are called until the base case is reached. Each general case must hold some information (the value of *n*) until the call to the next step is returned. The base case then returns the value of `sum(0)` to the previous general case, which returns the value of `sum(1)` to the previous general case, and so on.

# 17.1.2 Recursive Algorithms

In this section we solve simple recursive algorithms.

# Sum and Factorial

We discussed how to solve the *sum(n)* problem recursively. A sibling of the *sum(n)* function is the *factorial(n)* function (also called product). In the *sum* function, we must add numbers from *n* to 0; in the *factorial* function, we must multiply numbers from *n* to 1.

```
```cpp
// Sum function
int sum(int n)
{
    if (n <= 0)
    {
        return 0;
    }
    return sum(n - 1) + n;
}

// Factorial function
int factorial(int n)
{
    if (n <= 1)
    {
        return 1;
    }
    return factorial(n - 1) * n;
}
```
```

Note that *sum(0)* is 0, while *factorial(1)* is 1. In the *sum* function, we use the addition operator; in the *factorial* function, we use the multiplication operator. Note that in the *sum* function, *sum(n − 1)* is the value returned from the next call and in the factorial function, *factorial(n − 1)* is the value returned from the next call.

Program 17.1 tests the value of *sum(n)* and *factorial(n)* using the same value for *n* in each call. We can see that the *sum* grows slowly, but the *factorial* grows rapidly.

# **Program 17.1** Testing recursive sum and factorial

```
```cpp
/************************************************************/
/* A program to find the sum and factorial of an integer     */
/************************************************************/
#include <iostream>
using namespace std;

// Declaration of sum function
int sum(int n);
// Declaration of factorial function
int factorial(int n);

int main()
```
```