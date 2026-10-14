```
instance bindRWS :: Bind (RWS r w s) where ①
```

① (RWS r w s) is our m.

So, now here’s bind’s Type Signature specialized for RWS:

```
bind :: ∀ a b. RWS r w s a -> (a -> RWS r w s b) -> RWS r w s b
```

Now we can answer what is f x:

```
x :: a
f :: a -> RWS r w s b
f x :: RWS r w s b
```

Here’s where we left off:

```
instance bindRWS :: Bind (RWS r w s) where
  bind (RWS g) f = RWS \rws -> g rws # \(Tuple x rws') -> f x ???
```

Knowing what we know now, are we done?

If you said no, then you’re right. Our Lambda is supposed to return a Tuple, but instead we have an RWS.

This means that, we’re going to need a Run Function like we’ve written so many times before, e.g. parse, runState, runReader, runFoldL, etc.

Here’s runState as a reference:

```
runState :: ∀ a s. State s a -> (s -> Tuple a s)
runState (State f) = f
```

Go ahead and write runRWS and see if you can finish the Bind Instance before advancing. Hint: you can look at how we’ve written these Run Functions before since they’re all pretty much the same.

Here’s our Run Function’s Type Signature: