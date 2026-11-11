contract and throw the indicated exceptions. It would not be appropriate to use assertions instead.

Should you assert that `a` is not `null`? That is not appropriate either. The method documentation is silent on the behavior of the method when `a` is `null`. The callers have the right to assume that the method will return successfully in that case and not throw an assertion error.

However, suppose the method contract had been slightly different:

```
```text
@param a the array to be sorted (must not be null).
```
```

Now the callers of the method have been put on notice that it is illegal to call the method with a null array. Then the method may start with the assertion

```
```java
assert a != null;
```
```

Computer scientists call this kind of contract a *precondition*. The original method had no preconditions on its parameters—it promised a well-defined behavior in all cases. The revised method has a single precondition: that `a` is not `null`. If the caller fails to fulfill the precondition, then all bets are off and the method can do anything it wants. In fact, with the assertion in place, the method has a rather unpredictable behavior when it is called illegally. It sometimes throws an assertion error, and sometimes a null pointer exception, depending on how its class loader is configured.

# 7.4.4 Using Assertions for Documenting Assumptions

Often, programmers use comments to document their underlying assumptions. Consider this example from http://docs.oracle.com/javase/8/docs/technotes/guides/language/assert.html:

```
```java
if (i % 3 == 0)
    . . .
else if (i % 3 == 1)
```
```