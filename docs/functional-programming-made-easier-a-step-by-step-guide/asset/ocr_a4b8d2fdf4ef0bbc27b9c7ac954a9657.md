```
instance applyValidation :: Semigroup err => Apply (Validation err) where
  apply (Validation (Left err1)) (Validation (Left err2))
      = Validation $ Left (err1 <> err2) ①
```

① We combine the errors here. Notice how we didn’t need to use mempty. That means our choice of Semigroup was a good one and will stay.

Next, we code the other error case, i.e. when the left side is an error:

```
instance applyValidation :: Semigroup err => Apply (Validation err) where
  apply (Validation (Left err1)) (Validation (Left err2))
      = Validation $ Left (err1 <> err2)
  apply (Validation (Left err)) _ = Validation $ Left err ① ②
```

① We simply use the error.

② We know that _ will only be matched to a Right otherwise the first Pattern would’ve matched.

And finally, the successful case where we have a result on both sides:

```
instance applyValidation :: Semigroup err => Apply (Validation err) where
  apply (Validation (Left err1)) (Validation (Left err2))
      = Validation $ Left (err1 <> err2)
  apply (Validation (Left err)) _ = Validation $ Left err
  apply (Validation (Right f)) x = f <$> x ①
```

① And like we’ve done so many times before when implementing an Apply Instance, we only unwrap the Function, f and then use map from the Functor Instance, which, under the covers, leverages map from Either.

And now we can write the Applicative Instance. Give it a try before proceeding.

The code for Applicative should be pretty straight forward using the same logic as we did when we wrote Either’s:

```
instance applicativeValidation ::
  Semigroup err => Applicative (Validation err) where ①
  pure = Validation <<< Right ②
```

① We still need to constrain the error Type to Semigroup since an Applicative is also an Apply, which has this constraint. If you forget this, the compiler will dutifully remind you.

② We take the Pure Value and wrap it up in a Right, which is an Either and then we wrap that up in Validation.