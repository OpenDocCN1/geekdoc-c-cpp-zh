![](bbox=[0.191, 0.061, 0.809, 0.529])

Let’s see how our `sum` function is affected by favoring the *Left*:

```
0 + 5 + (-1) + 14 + 99 = 117
```

If now if we favor the *Right* we’ll get:

```
0 + 99 + 14 + (-1) + 5 = 117
```

Notice the result is the same. So using `sum` to help us decide which side to favor doesn’t help us much.

We also need to remember that we’re writing the `Foldable` instance for all functions, not just `sum`. So we need to consider the best way to traverse it so it works well for all `Foldable` operations, e.g. Subtraction. With Subtraction, the results will NOT be the same.

But, we didn’t specify anything special about this Binary Tree. It’s just a Binary Tree. It’s not balanced or sorted. So we cannot make any decisions based on that information.

So, let’s make another executive decision and just choose *Left*.

Now that we’ve decided on how to traverse, we’re ready to code the `Foldable` instance for `Tree`. Consult