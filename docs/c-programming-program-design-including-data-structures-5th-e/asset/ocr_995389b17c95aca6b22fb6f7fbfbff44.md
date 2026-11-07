Suppose that `num`, `num1`, and `num2` are **double** variables. Also suppose that `num1 = 45.75` and `num2 = 35.50`. Figure 6-2 shows various calls to the function `larger`.

![](bbox=[0.204, 0.166, 0.888, 0.372])

**FIGURE 6-2**  Function calls

You can also write the definition of the function `larger` as follows:

```
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

Because the execution of a `return` statement in a function terminates the function, the preceding function `larger` can also be written (without the word `else`) as:

```
double larger(double x, double y)
{
    if (x >= y)
        return x;

    return y;
}
```

Note that these forms of the function `larger` do not require you to declare any local variables.

+   **NOTE**
+   
+   1. In the definition of the function `larger`, `x` and `y` are formal parameters.
+   2. The `return` statement can appear anywhere in the function. Recall that once a `return` statement executes, all subsequent statements are skipped. Thus, it's a good idea to return the value as soon as it is computed.