In the absence of checked exceptions (as seen in Java), it's a good practice to document the “exceptional contract” (if any is applicable) of a delegate. This allows callers to see what exceptions they should be willing to handle, while the party that instantiates a delegate should make sure to refer to a method that obeys those rules:

```
/// <summary>Implements an engine's running procedure.</summary>
/// <exception cref="OutOfFuelException">Raised when fuel ran out.</exception>
delegate void EngineRunner();
```

A generic engine controller using an EngineRunner to run the engine's procedure now knows it should be willing to handle an OutOfFuelException appropriately, while the manufacturer of an engine knows that particular exception type should be used when signaling this particular exceptional error condition.

Under the covers, invocation of a delegate involved nothing more than a call to the Invoke instance method. One particular exceptional condition that can arise from this is having a null reference for the delegate object:

```
Action ouch = null;
ouch(); // throws NullReferenceException
```

In other words, use null checks (where appropriate) to guard against such conditions unless you absolutely positively expect a non-null delegate instance to be present (for example, because of null checks earlier on).

In Figure 17.12, the delegate invocation that occurs in the following method is shown, illustrating the call to the underlying Invoke method:

```
static int Calculate(Func<int, int, int> op, int a, int b) {
    return op(a, b);
}
```

![](bbox=[0.07, 0.88, 0.85, 0.95])

FIGURE 17.12 Delegate invocation unraveled.