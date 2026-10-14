Since we had trouble last time, we’re going to first write the identity Type Signature specialized for Kleisli. Hopefully, it’ll help us write the code:

```
instance categoryKleisli :: Monad m => Category (Kleisli m) where
  identity :: ???
```

Wow. I didn’t expect this part to be so hard. I’m not sure what to put here. Do you know?

To figure this out, we’ll start with an easier problem that’s just like this one. We’re going to write the Type Signature for Pure Functions. We’ll start with the code:

```
instance categoryFn :: Category (->) where
  identity x = x
```

And now, we’ll add the Type Signature:

```
instance categoryFn :: Category (->) where
  identity :: ∀ a. a -> a
  identity x = x
```

That was much easier. What we’d like to do is use this as a template for the Type Signature for our Kleisli version. Unfortunately, a -> a doesn’t look much like our Kleisli Type.

So, let’s rewrite the Type Signature using Prefixed Notation:

```
instance categoryFn :: Category (->) where
  identity :: ∀ a. (->) a a ①
  identity x = x
```

① -> is now in prefixed position.

And then let’s rename -> to Function:

```
instance categoryFn :: Category (->) where
  identity :: ∀ a. Function a a ①
  identity x = x
```

① We replaced (->) with Function.

That’s more like it. We have Function a a. This looks much closer to our Kleisli Type.