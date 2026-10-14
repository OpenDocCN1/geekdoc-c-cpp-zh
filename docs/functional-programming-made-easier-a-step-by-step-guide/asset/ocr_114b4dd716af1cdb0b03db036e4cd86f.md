```
instance bindMaybe :: Bind Maybe where
  bind Nothing _ = Nothing ①
  bind (Just x) f = f x
```

① The compiler is generating if logic to check Patterns, which, effectively, checks for errors in this implementation.

And since the Monad’s bind implementation does this work for us, we’re freed to code without thinking too much about it.

Here are some common Monads and their Monadic Computations:

```
Identity  -> No Computation
Maybe     -> Error Checking
Either    -> Error Checking
Writer    -> Log Appending
Reader    -> Threading Read Only Value
State     -> Threading State
```

We haven’t seen Reader or State just yet so their Monadic Computation may not make sense, but they will.

But look at Maybe or Either and notice what we’ve been calling a Side-effect is really a Parallel Computation, i.e. the Monadic Computation that’s being performed every time we use bind. Visually, it’s hidden from us, buried in the implementation of >>=, and even more so thanks to do notation.

But it’s there all the same and the compiler certainly won’t forget about it.

Another thing that’s important to think about is that the Monad’s API Functions help bridge the gap between the Parallel Computations. Here’s a diagram to illustrate how tell does this: