All encoders and decoders should follow the following law:

```
decodeJson <<< encodeJson = pure
```

Remember, `pure` is Identity in the Kleisli Category. Here the `Monad` is `Either` since `decodeJson` can fail. In this case, it cannot since `encodeJson` is called first, assuming we have written a proper decoder.

Look over our encoder and decoder to make sure we can roundtrip data through them and get back what we started with.

The following code is a test, albeit incomplete, of roundtripping:

```
log $ show $ (decodeJson $ encodeJson Pie :: Either _ Dessert) ① ②
```

+   ① Should print `(Right Pie)`, i.e. equivalent to `pure Pie`.
+   
+   ② We have to add an explicit Type definition to let the compiler know what Type `decodeJson` should produce. This is because it cannot figure that out since it’s just give some Json Value, which could be anything.

Now, we should write an encoder and decoder for `Meal`. Here’s its definition again:

```
data MainDish = Steak | Chicken

data SideDish = Rice | Asparagus

type Meal =
  { main :: MainDish
  , side :: SideDish
  , dessert :: Dessert
  }
```

But before we can do that, we must have encoders for both `MainDish` and `SideDish`. These are nearly identical to `Dessert`, so I’m just going to give you them complete: