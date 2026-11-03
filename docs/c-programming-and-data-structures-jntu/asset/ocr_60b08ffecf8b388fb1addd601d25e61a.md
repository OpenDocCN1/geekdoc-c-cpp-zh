Nesting of function calls is also possible. For example, a statement like

```
p = mul(mul(5,2),6);
```

is valid. This represents two sequential function calls. The inner function call is evaluated first and the returned value is again used as an actual argument in the outer function call. If mul returns the product of its arguments, then the value of p would be 60 (= 5 × 2 × 6).

# 10.13 RECURSION

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
This an example of recursion
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