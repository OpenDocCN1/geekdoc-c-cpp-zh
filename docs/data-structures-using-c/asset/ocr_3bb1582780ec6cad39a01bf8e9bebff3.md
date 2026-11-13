In each of these cases, the problem is reduced to a smaller version of itself.
Program Code 4.3 is a recursive code for computation of Eq. (4.4).

```
PROGRAM CODE 4.3

Long int Power(int x, int y)
{
    if(y == 0)    // end condition
        return(1);
    else
        return(x * Power(x, y - 1);
        // This is the "recursive call"
}
```

The end condition in Program Code 4.3 can be y = 1; then the return value will be x
(Program Code 4.6). The iterative version of the same computation is demonstrated in
Program Code 4.4.

```
PROGRAM CODE 4.4

Long int Power(int x, int y)
{
    int result = 1;
    for(int i = 1; i <= y; i++)
        result = result * x;
    return(result);
}
```

# 4.3 USE OF STACK IN RECURSION

We have studied stack as a data structure in Chapter 3. The stack is a special area of
memory where temporary variables are stored. It acts on the LIFO principle. To understand
how recursive functions use the stack, let us discuss Program Code 4.2. The core
steps are given in the following code:

```
if(n <= 1)
    return 1;
else
    return n * Factorial(n - 1);
```

Let n = 3; that is, let us compute the value of 3!, which is 3 x 2 x 1 = 6. When the function
is called for the first time, n holds the value 3, so the else statement is executed. The
function knows the value of n but not of Factorial(n - 1), so it pushes n (value = 3)