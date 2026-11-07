in which statements are usually declaration and/or executable statements. The formal parameter list may be empty, in which case, in the function heading, the empty parentheses are still needed.

# FORMAL PARAMETER LIST

The formal parameter list has the following syntax:

```
```text
dataType& variable, dataType& variable, ...
```
```

You must specify both the data type and the variable name in the formal parameter list. The symbol & after dataType has a special meaning; some parameters will have & and some will not, and we will explain why later in this chapter.

# FUNCTION CALL

The function call has the following syntax:

```
```text
functionName(actual parameter list);
```
```

# ACTUAL PARAMETER LIST

The actual parameter list has the following syntax:

```
```text
expression or variable, expression or variable, ...
```
```

in which expression can consist of a single constant value. As with value-returning functions, in a function call, the number of actual parameters together with their data types must match the formal parameters in the order given. Actual and formal parameters have a one-to-one correspondence. (Functions with default parameters are discussed at the end of this chapter.) A function call results in the execution of the body of the called function.

Example 6-8 shows a void function with parameters.

# EXAMPLE 6-8

```
```cpp
void funexp(int a, double b, char c, int x)
{
    .
    .
    .
}
```
```

The function funexp has four parameters.

![](bbox=[0.913, 0.386, 1.0, 0.493])