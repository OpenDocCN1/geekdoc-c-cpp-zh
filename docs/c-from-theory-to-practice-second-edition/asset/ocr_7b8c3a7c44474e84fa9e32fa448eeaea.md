test() declares two integer variables with values 10 and 20 and returns their sum. This value is stored into sum and the program displays 30. Notice that it is not needed to declare sum; we could write printf("%d\n", test()); test() is called first and the returned value is used as an argument in printf().

Before ending this section, we'd like to point out that the order of the function calls in a compound expression, such as d = a() + b() * c(); is undefined. In other words, these three functions can be called in any order. Don't assume that the b() and c() functions will be called first because of the multiplication's precedence. And if any of them changes a variable on which some other may depend, the value assigned to d will depend on the evaluation order.

# Function Call with Parameters

A call to a function that takes parameters is made by writing the function name followed by a list of arguments, enclosed in parentheses. Using arguments is one way to pass information to a function. The difference between parameter and argument is that the term parameter refers to the variables that appear in the definition of the function, while the term argument refers to the expressions that appear in the function call. For example, consider the following program:

```
```c
#include <stdio.h>

int test(int x, int y);

int main(void)
{
    int sum, a = 10, b = 20;

    sum = test(a, b); /* The variables a and b become the function's arguments. */
    printf("%d\n", sum);
    return 0;
}

int test(int x, int y) /* The variables x and y are the function's parameters. */
{
    return x+y;
}
```
```

The argument can be any valid expression, such as constant, variable, math, or logical expression, even another function with a return value. Notice that we could omit sum and write printf("%d\n", test(a, b)); test() is called first, and then printf() outputs the return value.

Because the order in which arguments are evaluated is not specified, don't write something like printf("%d %d\n", ++a, test(a, b)); It depends on the compiler whether a is incremented, before or after test() is called.

The number of the arguments and their types should match the function declaration. If the arguments are less, the compiler will produce an error message. If the types of the arguments don't match the types of the parameters, the compiler will try to convert implicitly the types of the mismatched arguments to the types of the corresponding parameters. If it is successful, the compiler may display a warning message to inform the programmer