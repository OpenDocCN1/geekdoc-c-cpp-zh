Functions of this type are commonly referred to as *Monadic Functions* or *Effectful Functions*. Basically, Function with Side-effects.

But how does `bind` accomplish this kind of composition, especially since it's more akin to Function Application than Function Composition?

Well, remember when we rewrote `composeDebuggable` in terms of `applyDebuggable`?

```
composeDebuggable
  :: ∀ b c d
  . (c -> Debuggable d)
  -> (b -> Debuggable c)
  -> (b -> Debuggable d)
composeDebuggable g f x = f x `applyDebuggable` g
```

But `applyDebuggable` is just `bind` specialized for `Debuggable`.

So let's write the general version of `composeDebuggable` that leverages `bind` to allow us to compose Monadic Functions.

We're going to call it `composeKleisli` for reasons that will become apparent once we talk about the *Kleisli Category*:

```
composeKleisli
  :: ∀ a b c m
  . Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f x = f x >>= g

infixr 5 composeKleisli as >>= ①
```

① This is the Operator Alias for `composeKleisli` and is commonly referred to as the *Fish Operator.*

So `bind`, Monadic Function Application, lets us write `composeKleisli` for `Monads`, just like `$`, Pure Function Application, lets us write `compose` for `Functions`: