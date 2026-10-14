Look at `fmx s >>>= ...`.

That’s were things go wrong. Since `ExceptT` is below us in the Stack, it’s going to call it’s `bind`, which Short-circuits on errors. So, during the error case, the Lambda NEVER GETS CALLED. That’s the whole point of Short-circuiting.

This means that `s'` will NOT capture the changes made in the failed computation.

It turns out that there’s no way to fix this. We just never know enough about the underlying `Monads` to extract the modified State.

So if we cannot fix it, we’ll have to learn to live with it, which means we need to understand how to properly use `catchError` and what pitfalls we can expect.

Before we can do that, we’ll need to understand about the `spy` Function. `spy` will take any Value and display its Internal Representation on the Console no matter if it has a `Show` Instance or not. It’s used for debugging purposes.

Here’s its Type Signature:

```
spy :: ∀ a. DebugWarning => String -> a -> a
```

First thing to notice about `spy`’s Type Signature is that `DebugWarning` is a marker Constraint that the compiler will look for and give you a warning that you’re using `spy` in a Function.

The reason for this is because `spy` breaks the contract that all Functions in PureScript are Pure. It does this because it prints to the Console. This is ONLY to be used for debugging purposes. It should NEVER be used in production code.

Realize that when you use `spy` and the compiler memoizes the result of a Function call, your `spy` output may or may not occur once for every call to the Function where it’s used.

***Memoize*** is the term for remembering the result of a computation to avoid having to call a Function again. The compiler remembers the result by storing it in memory somewhere, or, in the case of Haskell, which generates binary code, it save it in a CPU register.

The compiler can make these sorts of optimizations in Pure Functional Programming since it knows that all Functions are Pure and calling it with the same input will produce the same output.

The second thing to notice about `spy`’s Type Signature is that its first Parameter is a `String`. This is what `spy` will prefix the output with followed by a colon and a space. This is useful to help to you know what you’ve printed out.

The Value that `spy` will output is the second Parameter, `a`.

Third thing to notice is that `spy` returns an `a`. So, it’s like `identity` but with a REAL WORLD Side-effect. Not Pure Side-effects like we’ve been doing with `Monads`.