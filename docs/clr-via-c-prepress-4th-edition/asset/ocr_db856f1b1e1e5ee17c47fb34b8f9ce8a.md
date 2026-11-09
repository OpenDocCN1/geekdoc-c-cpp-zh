![](bbox=[0.158, 0.086, 0.745, 0.287])

FIGURE 17-3 Initial state of the delegate objects referred to by the fb1, fb2, and fb3 variables.

The reference variable to a Feedback delegate object, `fbChain`, is intended to refer to a chain or set of delegate objects that wrap methods that can be called back. Initializing `fbChain` to `null` indicates that there currently are no methods to be called back. The `Delegate` class's public, static `Combine` method is used to add a delegate to the chain:

```
~~~csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb1);
~~~
```

When this line of code executes, the `Combine` method sees that we are trying to combine `null` and `fb1`. Internally, `Combine` will simply return the value in `fb1`, and the `fbChain` variable will be set to refer to the same delegate object referred to by the `fb1` variable, as shown in Figure 17-4.

![](bbox=[0.158, 0.552, 0.745, 0.785])

FIGURE 17-4 State of the delegate objects after inserting the first delegate in the chain.

To add another delegate to the chain, the `Combine` method is called again:

```
~~~csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb2);
~~~
```

Internally, the `Combine` method sees that `fbChain` already refers to a delegate object, so `Combine`