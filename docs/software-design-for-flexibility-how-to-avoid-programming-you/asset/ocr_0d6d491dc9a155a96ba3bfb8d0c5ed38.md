Note carefully how reentering this captured continuation, by calling the-continuation, returns control to the point before the addition and, therefore, before assigning variable sum and returning the symbol ok. This is why invoking returns the symbol ok. However, sum is assigned the sum of 2 and the argument supplied to the-continuation. So when we get the value of sum we get new. This demonstrates how to use a captured continuation to proceed from intermediate return points. We will see how this mechanism can be used for backtracking in 5.5.3.

# 5.5.3 From continuations to amb

It turns out that anything we want to do, including implementing amb, can be done with just the Scheme native call/cc; let's see how to do that.

Indeed, continuations are a natural mechanism for supporting backtracking. A choice can be made, and if that choice turns out to be inappropriate, an alternative choice can be made and its consequences worked out. (Wouldn't we like real life to have this!) In our square-root example, the square-root program should return the amb of both square roots, where amb is the operator that chooses and returns one of them, with the option to provide the other if the first is rejected. The receiver can then just proceed to use the given solution; but if at some point the receiver finds that its computation does not meet some constraint, it can fail, causing the amb operator to revise its choice and return with the new choice through its continuation. In essence, the continuation allows the generator of choices to be written as a coroutine that interacts with the receiver/tester of the choices.

The heart of the backtracker is amb-list, which takes a sequence of sibling chunks, each representing an alternative value for the amb expression. The thunks are produced by an amb macro, which syntactically transforms amb expressions into amb-list expressions, as follows:

```
(amb en) =>=
(amb-list (list (lambda () el) ... (lambda () en)))
```

The amb macro (written in portable syntax-rules) is: