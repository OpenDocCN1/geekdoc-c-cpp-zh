
We're not going to use `x` and the compiler has no preconceived ideas about its Type. So it will always compile.

Then we simply put `undefined` in the expression, which will always compile.

After making these changes, our Function compiles and the Type Hole causes the following compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_949_0.png)

One nice thing about Type Holes is that below the Inferred Type is a list of all of the Types for all the other Variables that are involved in the code that's part of the Type Hole.

But the real news here is in the Type that it inferred:

```
m0 (m0 (Tuple b1 s2))
```

We have our underlying Monad in our underlying Monad. Not good. But how did this happen?

See if you can see where I went wrong by looking back at our code before we started using `undefined`:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
-- COMPILER ERROR!!
apply (StateT fmf) (StateT fmx) = StateT \s ->
  fmf s <#> \(Tuple f s') -> fmx s <#> \(Tuple x s'') -> Tuple (f x) s''
```

Can you see why I have nested underlying Monads?

It's because I'm mapping TWICE! This gives us a Monad in the SAME Monad. So, how do we fix this?

If your inclination is to use `join`, you're on the right track. But remember, `join` is written in terms of `bind` and with `bind`, we never have this problem.

So, why not just use `bind`?

Let's start over:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> ???
```

At this point, we're going to want to start with a `do` block:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    ???
```

Now, we're going to call `fmf` and extract its Tuple:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    Tuple f s' <- fmf s
    ???
```

And now, we'll call `fmx` and extract its Tuple:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    Tuple f s' <- fmf s
    Tuple x s'' <- fmx s' ①
    ???
```

① Do NOT forget to pass the updated State to `fmx`, i.e. the State that's returned and possibly updated by `fmf`.

And now we can apply `f` to `x` and wrap everything up in a Tuple and then wrap that up in the underlying Monad:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    Tuple f s' <- fmf s -- COMPILER ERROR!!
    Tuple x s'' <- fmx s'
    pure $ Tuple (f x) s'' ①
```

① Make sure to return the final State `s''` since it may have been updated by `fmx`.

And after all of that...

We have a compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_951_0.png)

And this one is an easy one. We've used `do` syntax to code in the underlying Monad, so we'll have to ensure that `m` is more than just a `Functor`. So, we'll change the `Functor` Constraint to `Bind`:

```
instance applyStateT :: Bind m => Apply (StateT s m) where ①
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    Tuple f s' <- fmf s
    Tuple x s'' <- fmx s'
    pure $ Tuple (f x) s''  -- COMPILER ERROR!!
```

① Replace `Functor` Constraint with `Bind`.

And now the compiler isn't happy for a different reason:

![](img/8c0e9b687c62642e828ccb5481e11313_951_1.png)

Another easy error to fix. Since we're using `pure` to construct our underlying Monad, it needs to be an `Applicative` too.

But wait, it's already a `Bind`, and a `Bind` and an `Applicative` is a `Monad`. That means that all we have to do is change our Constraint from `Bind` to `Monad` and we should be good:

```
instance applyStateT :: Monad m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> do
    Tuple f s' <- fmf s
    Tuple x s'' <- fmx s'
    pure $ Tuple (f x) s''
```

① Replace `Bind` Constraint with `Monad`.

Don't forget to remove the import for `Undefined` since we don't need it anymore. Well, I can't say that we won't need it later, but we should remove it just the same so we don't forget and leave it behind.

Luckily, the compiler will tell us when an import is "redundant", i.e. not necessary.

And we probably want to remove it from our `spago.dhall` so `spago` won't bug us with warnings on every single build that we aren't using the `undefined` package.

Now, we're ready to write the `Applicative` Instance. The `Applicative` is usually pretty easy, so please don't read further until you've given it a try.

Here's the instance definition:

```
instance applicativeStateT :: Monad m => Applicative (StateT s m) where
```

The Constraint is the same as the Constraint we used on our `Apply` Instance since it's `Applicative`'s Superclass. If we forget this, the compiler will be sure to remind us.

Next, we'll start the implementation with our typical pattern:

```
instance applicativeStateT :: Monad m => Applicative (StateT s m) where
  pure x = StateT \s -> ???
```

The `StateT` Function must return a Tuple in the underlying Monad, so we should add that:

```
instance applicativeStateT :: Monad m => Applicative (StateT s m) where
  pure x = StateT \s -> pure $ Tuple ??? ???
```

The State will not change as a result of running this, so we'll just return `s` in the second position.

```
instance applicativeStateT :: Monad m => Applicative (StateT s m) where
  pure x = StateT \s -> pure $ Tuple ??? s
```

The first position of the `Tuple` is the Pure Computation. In the case of `pure`, it's just `x`, our Pure Value. So, we'll add that to the first position:

```
instance applicativeStateT :: Monad m => Applicative (StateT s m) where
  pure x = StateT \s -> pure $ Tuple x s
```

The next thing you should code up is the `Bind` Instance. Please give it a try before advancing any further.

Here's the instance definition:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
```

The Constraint is a `Monad` since `Applicative`, our Superclass, has that same Constraint.

Next, the left-hand side of the expression:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind (StateT fmx) f = ???
```

> The name `fmx` is to remind us that we have a Function that will return a Monadic Value.

Now, we're going to use our common pattern:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind (StateT fmx) f = StateT \s -> ???
```

Now what?

What is the next step? And how do you figure out what to do next here?

To answer this question, you first need to state what you HAVE and what you WANT. We'll do that with Types. But before we do, we should add the Type Signature for `bind` specialized for `StateT`:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind :: ∀ a b. StateT s m a -> (a -> StateT s m b) -> StateT s m b
  bind (StateT fmx) f = StateT \s -> ???
```

Now we can list what we HAVE followed by what we WANT with particular attention paid to the Types:

```
-- HAVE
fmx :: s -> m (Tuple a s)
f :: a -> StateT s m b
s :: s

-- WANT
\s -> ??? :: s -> m (Tuple b s)
StateT \s -> ??? :: StateT s m b
```

If the Type for `fmx` isn't clear, then remember that the function `StateT` contains `fmx`, and `StateT fmx` is of Type `StateT s m a` (see the specialized Type Signature for `bind`). Once you see that, `fmx`'s Type Signature then comes from `StateT`'s Type definition:

```
newtype StateT s m a = StateT (s -> m (Tuple a s))
```

The next question to ask is how can I combine the things I HAVE to give me the things I WANT. Take a look at what we have and see if you can combine them to get us closer to what we want.

When I do this, I think about the Monadic Function, `f`, and how it needs an `a` before I can use it. Then I look around and the only `a` that's available to me is in `fmx`.

But before I can get the `a` I have to first call `fmx` with an `s`. So we'll write down what we can compute with `fmx` and `f`:

```
-- HAVE
fmx :: s -> m (Tuple a s)
f :: a -> StateT s m b
s :: s

-- COMPUTED
fmx s :: m (Tuple a s)

-- WANT
\s -> ??? :: s -> m (Tuple b s)
StateT \s -> ??? :: StateT s m b
```

Well, that got us one step closer to the `a`, but it's locked up in our underlying Monad. But I don't know anything about that Monad, other than the fact that it's a Monad.

That means I can use any Monad typeclass methods to get at that `a`.

So what's the easiest way to get to that `a`?
