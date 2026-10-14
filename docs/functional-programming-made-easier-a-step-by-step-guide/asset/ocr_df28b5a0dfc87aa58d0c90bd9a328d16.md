```
Control.Monad.Monad x0
```

Looks like x is a Monad. Let’s add that Constraint and rename it to m:

```
liftExcept
  :: ∀ e a m t
  . Monad m
  => MonadTrans t
  => Monad (t m)
  => m (Either e a)
  -> t m a
```

Error:

```
Control.Monad.Error.Class.MonadError e0 (t5 m3)
```

Looks like t m is a MonadError. Let’s add that and REMOVE the Monad (t m) Constraint since it’ll be covered by the MonadError Constraint:

```
liftExcept
  :: ∀ e a m t
  . MonadError e (t m)
  => Monad m
  => MonadTrans t
  => m (Either e a)
  -> t m a
liftExcept ma = ma # lift >>= liftEither
```

And this compiles!!

When the compiler doesn’t give us a Type Signature or if Type Holes in the Type Signature don’t work because of missing Constraints, then this technique is pretty easy.

In our case, we know that t is ExceptT e which means that t m a is ExceptT e m a where m is a Monad. We could’ve use a Monomorphic Type for t, i.e. ExceptT e, but having this Polymorphic is always better since we could always use this elsewhere.

But now that we have this as a generalized Function with only t in the Type Signature, the name liftExcept seems wrong.

But what is a good name?