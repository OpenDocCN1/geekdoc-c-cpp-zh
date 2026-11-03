Exercise 8-2: Edit the source code from Listing 8-1 so that addition instead of subtraction is performed in Line 8. Can you explain the program's output?

# Introducing the if keyword

The if keyword is used to make decisions in your code based upon simple comparisons. Here's the basic format:

```
if(expression)
{
    statement;
}
```

The expression is a comparison, a mathematical operation, the result of a function, or some other condition. When the expression is true, the statements (or statement) enclosed in braces are executed; otherwise, they're skipped.

The if statement's expression need not be mathematical. It can be a function that returns a true or false value, for example:

```
if( ready() )
```

This statement evaluates the return of the ready() function. If the function returns a true value, the statements belonging to if are executed.

Any non-zero value is considered true in C. Zero is considered false. So this statement is true:

```
if(1)
```

And this statement is always false:

```
if(0)
```

You know whether a function returns a true or false value by reading the function's documentation, or you can set a true or false return value when writing your own functions.

You cannot compare strings by using an if comparison. Instead, you use specific string comparison functions, which are covered in Chapter 13.

When only one statement belongs to an if comparison, the braces are optional.

![](bbox=[0.15, 0.85, 0.22, 0.95])