# How It Works

The function now supports positive and negative powers of x, so the first action is to check whether the value for the power that x is to be raised to, n, is negative:

```
if (n < 0)
{
    x = 1.0/x;
    n = -n;
}
```

Supporting negative powers is easy; it just uses the fact that x⁻ⁿ can be evaluated as (1/x)ⁿ. Thus if n is negative, you set x to be 1.0/x and changed the sign of n so it’s positive.

The next if statement decides whether or not the power() function should call itself once more:

```
if (n > 0)
    return x*power(x, n-1);
else
    return 1.0;
```

The if statement provides for the value 1.0 being returned if n is zero, and in all other cases it returns the result of the expression, x*power(x, n-1). This causes a further call to the function power() with the index value reduced by 1. Thus the else clause in the if statement provides the essential mechanism necessary to avoid an indefinite sequence of recursive function calls.

Clearly, within the function power(), if the value of n is other than zero, a further call to the function power() occurs. In fact, for any given value of n other than 0, the function calls itself n times, ignoring the sign of n. The mechanism is illustrated in Figure 5-4, where the value 3 for the index argument is assumed.

As you see, the power() function is called a total of four times to generate x³, three of the calls being recursive where the function is calling itself.

# Using Recursion

Unless you have a problem that particularly lends itself to using recursive functions, or if you have no obvious alternative, it’s generally better to use a different approach, such as a loop. This is much more efficient than using recursive function calls. Think about what happens with our last example to evaluate a simple product, x*x*...x, n times. On each call, the compiler generates copies of the two arguments to the function, and also has to keep track of the location to return to when each return is executed. It’s also necessary to arrange to save the contents of various registers in your computer so that they can be used within the function power(), and of course these need to be restored to their original state at each return from the function. With a quite modest depth of recursive call, the overhead can be considerably greater than if you use a loop.

This is not to say you should never use recursion. Where the problem suggests the use of recursive function calls as a solution, it can be an immensely powerful technique, greatly simplifying the code. You’ll see an example where this is the case in the next chapter.