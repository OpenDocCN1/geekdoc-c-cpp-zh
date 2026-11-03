A function may or may not send back any value to the calling function. If it does, it is done through the **return** statement. While it is possible to pass to the called function any number of values the called function can only return *one value* per call, at the most.

The **return** statement can take one of the following forms

```
```
return;

or

return(expression);
```
```

The first, the 'plain' **return** does not return any value; it acts much as the closing brace of the function. When a **return** is encountered, the control is immediately passed back to the calling function. An example of the use of a simple **return** is as follows:

```
```c
if(error)
    return;
```
```

The second form of **return** with an expression returns the value of the expression. For example, the function

```
```c
mul(x,y)
int    x,y;
{
    int p;
    p = x*y;
    return(p);
}
```
```

returns the value of **p** which is the product of the values of **x** and **y**. The last two statements can be combined into one statement as follows:

```
```c
return (x*y);
```
```

A function may have more than one **return** statements. This situation arises when the value returned is based on certain conditions. For example:

```
```c
if(x <= 0)
    return(0);
else
    return(1);
```
```

What type of data does a function return? All functions by default return **int** type data. But what happens if a function must return some other type? We can force a function to return a particular type of data by using a *type specifier* in the function header. Example:

```
```c
double product(x,y)
float sqr_root(p)
```
```

When a value is returned, it is automatically cast to the function's type. In functions that do computations using **double**, yet return **int**, the returned value will be truncated to an integer.

# **10.6 CALLING A FUNCTION**

A function can be called by simply using the function name in a statement. Example: