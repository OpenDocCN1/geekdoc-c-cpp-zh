# Example 2: Power Function

Here's an example of a function that raises an int to the power of an unsigned int and returns the result as a long:

```
// power.c

long power(int base, unsigned expon) {
    int i;
    long num = 1;

    for (i = 0; i < expon; ++i) {
        num *= base;
    }
    return num;
}
```

The function follows a simple algorithm, multiplying base by itself expon times. A for loop is used to control the number of multiplications, and variable num stores the value to be returned.

The function header:

```
long power(int base, unsigned expon)
```

informs us the type of the return value, long, the name of the function, power, and a list of arguments used by the function, int base, unsigned expon. The arguments and their types are enclosed in parentheses, each pair separated by commas.

+   The body of the function is bounded by a set of braces. Any variables declared here will be treated as local.

+   Upon reaching a return statement, control of the program returns to the calling function. num is the value which is returned from the function. If the final closing brace is reached before any return value, then the function will return automatically, any return value will then be meaningless.

+   The return value of a function is always converted to the type given by the type specifier of the function. In this case the solution to the function is being held in a long variable, num.