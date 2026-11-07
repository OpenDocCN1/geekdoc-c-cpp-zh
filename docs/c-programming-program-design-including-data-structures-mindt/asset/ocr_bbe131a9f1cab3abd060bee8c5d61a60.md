For predefined functions, you only need to be concerned with the first four properties. Software companies, typically, do not give out the actual source code, which is the body of the function.

# Syntax: Value-Returning Function

The syntax of a value-returning function is:

```
functionType functionName(formal parameter list)
{
    statements
}
```

in which statements are usually declaration statements and/or executable statements. In this syntax, functionType is the type of the value that the function returns. The functionType is also called the data type or the return type of the value-returning function. Moreover, statements enclosed between curly braces form the body of the function.

# Syntax: Formal Parameter List

The syntax of the formal parameter list is:

```
dataType identifier, dataType identifier, ...
```

Consider the definition of the function abs given earlier in this chapter. Figure 6-1 identifies various parts of this function.

![](bbox=[0.183, 0.592, 0.91, 0.772])

FIGURE 6-1  Various parts of the function abs

# Function Call

The syntax to call a value-returning function is:

```
functionName(actual parameter list)
```

For example, in the expression x = abs(-5);, the function abs is called.