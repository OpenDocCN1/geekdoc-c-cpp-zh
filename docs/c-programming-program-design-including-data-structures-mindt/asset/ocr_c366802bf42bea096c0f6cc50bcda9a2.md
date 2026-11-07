```
    int secret(int x)
    {
        if (x > 5)        //Line 1
            return 2 * x; //Line 2
    }
```

Because this is a value-returning function of type `int`, it must return a value of type `int`. Suppose the value of `x` is 10. Then the expression `x > 5` in Line 1 evaluates to `true`. So the `return` statement in Line 2 returns the value 20. Now suppose that `x` is 3. The expression `x > 5` in Line 1 now evaluates to `false`. The `if` statement therefore fails, and the `return` statement in Line 2 does _not_ execute. However, there are no more statements to be executed in the body of the function. In this case, the function returns a strange value. It thus follows that if the value of `x` is less than or equal to 5, the function does not contain any valid `return` statements to return a value of type `int`.

A correct definition of the function `secret` is:

```
    int secret(int x)
    {
        if (x > 5)        //Line 1
            return 2 * x; //Line 2

        return x;         //Line 3
    }
```

![](bbox=[0.938, 0.317, 1.0, 0.454])

Here, if the value of `x` is less than or equal to 5, the `return` statement in Line 3 executes, which returns the value of `x`. On the other hand, if the value of `x` is, say 10, the `return` statement in Line 2 executes, which returns the value 20 and also terminates the function.

Recall that in a value-returning function, the `return` statement returns the value. Consider the following `return` statement:

```
    return x, y;    //only the value of y will be returned
```

This is a legal `return` statement. You might think that this `return` statement is returning the values of `x` and `y`. However, this is not the case. Remember, a `return` statement returns _only_ one value, even if the `return` statement contains more than one expression. If a `return` statement contains more than one expression, _only_ the value of the _last_ expression is returned. Therefore, in the case of the above `return` statement, the value of `y` is returned. The following program further illustrates this concept:

```
    // This program illustrates that a value-returning function
    // returns only one value, even if the return statement
    // contains more than one expression. This is a legal, but not
    // a recommended code.

    #include <iostream>

    using namespace std;
```