```
-- HAVE
fm x :: s -> m (Tuple a s)
f :: a -> StateT s m b
s :: s
\s -> ??? :: s -> m (Tuple b s)

-- WANT
StateT \s -> ??? :: StateT s m b
```

If the Type for fmx isn’t clear, then remember that the Function StateT contains, fmx, is of Type StateT s m a (see specialized Type Signature for bind). Once you see that, fmx’s Type Signature then comes from StateT’s Type definition:

```
newtype StateT s m a = StateT (s -> m (Tuple a s))
```

Next question to ask is how can I combine the things I HAVE to give me the things I WANT. Take a look at what we have and see if you can combine them to get us closer to what we want.

When I do this, I think about the Monadic Function, f, and how it needs an a before I can use it. Then I look around and the only a that’s available to me is in fmx.

But before I can get the a I have to first call fmx with an s. So we’ll write down what we can compute with fmx and f:

```
-- HAVE
fm x :: s -> m (Tuple a s)
f :: a -> StateT s m b
s :: s
\s -> ??? :: s -> m b

-- COMPUTED
fm x s :: m (Tuple a s)

-- WANT
StateT \s -> ??? :: StateT s m b
```

We’ll that got us one step closer to the a, but it’s locked up in our underlying Monad. But I don’t know anything about that Monad, other than the fact that it’s a Monad.

But that fact is quite useful. That means I can use any Monad Typeclass Methods to get at that a.

So what’s the easiest way to get to that a?