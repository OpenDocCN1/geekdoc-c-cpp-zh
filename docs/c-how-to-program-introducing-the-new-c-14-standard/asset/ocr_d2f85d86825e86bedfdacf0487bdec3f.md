the following `while` statement executes, the variable `product` contains the result:

```
```cpp
{
    int product{3};

    while (product <= 100) {
        product = 3 * product;
    }
}
```
```

Each iteration of the `while` statement multiplies `product` by 3, so `product` takes on the values 9, 27, 81 and 243 successively. When `product` becomes 243, `product <= 100` becomes *false*. This terminates the iteration, so the final value of `product` is 243. At this point, program execution continues with the next statement after the `while` statement.

![](bbox=[0.12, 0.62, 0.193, 0.675])

# Common Programming Error

# 4.2

*Not providing in the body of a `while` statement an action that eventually causes the condition in the `while` to become false results in a logic error called an **infinite loop** (the loop never terminates).*