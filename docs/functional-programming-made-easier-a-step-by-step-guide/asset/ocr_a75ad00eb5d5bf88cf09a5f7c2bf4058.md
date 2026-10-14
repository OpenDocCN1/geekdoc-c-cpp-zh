③ This final Type doesn’t match our bind Type Signature.

Here we wound up with an m b where we only wanted a b. Look back at the error message. That’s exactly what the compiler was complaining about.

So now, what do we need to fix this?

We need a Function, which I’ll call join, that does the following:

```
join :: ∀ a m. m (m a) -> m a
```

This basically flattens out one of the Monad Contexts. In fact, in other Functional Languages, e.g. Scala, this Function is called flatten. But in PureScript and Haskell it’s called join.

So, instead of implementing a Bind Typeclass, we could implement a Typeclass that has join as its Member:

```
class Apply m <= Join m where
  join :: ∀ a. m (m a) -> m a ①
```

① I’ve dropped m from ∀ in the Type Signature since it can now be found in the Typeclass definition.

Our alternative Monad definition uses Join instead of Bind:

```
class (Applicative m, Join m) <= Monad ①
```

① Join instead of Bind.

And now we can fix our bind Function:

```
bind :: ∀ a b m. Join m => m a -> (a -> m b) -> m b ①
bind x f = join $ map f x ②
```

① Now it has to at least be a Join since we’re using join.

② We use join after map has left us with doubly nested m’s. It will flatten out one of the m’s.

When this approach is taken for Monad, bind is typically called flatMap, which should be apparent from its implementation:

```
flatMap :: ∀ a b m. Monad m => m a -> (a -> m b) -> m b ①
flatMap x f = flatten $ map f x ②
```