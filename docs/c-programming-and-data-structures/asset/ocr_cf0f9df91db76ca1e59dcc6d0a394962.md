main reads the values of a, b and c and calls the function ratio to calculate the value a/(b−c). This ratio cannot be evaluated if (b−c) = 0. Therefore, ratio calls another function difference to test whether the difference (b−c) is zero or not; difference returns 1, if b is not equal to c; otherwise returns zero to the function ratio. In turn, ratio calculates the value a/(b−c) if it receives 1 and returns the result in float. In case, ratio receives zero from difference, it sends back 0.0 to main indicating that (b−c) = 0.

Nesting of function calls is also possible. For example

```
P = mul(mul(5,2),6);
```

is valid. This represents two sequential function calls. The inner function call is evaluated first and the returned value is again used as an actual argument in the outer function call. If mul returns the product of its arguments, then the value of p would be 60 (=5×2×6).

Note that the nesting does not mean defining one function within another. Doing this is illegal.

# 5.16 RECURSION

When a called function in turn calls another function a process of ‘chaining’ occurs. Recursion is a special case of this process, where a function calls itself. A very simple example of recursion is presented below:

```
main()
{
    printf("This is an example of recursion\n")
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
factorial of n = n(n-1)(n-2).......1.

For example,
factorial of 4 = 4x3x2x1 = 24

A function to evaluate factorial of n is as follows:

```
factorial(int n)
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