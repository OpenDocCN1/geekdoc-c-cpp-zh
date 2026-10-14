# 17.4. Code for Applicative Instance for Either

As always the Type definition comes first:

```
data Either a b = Left a | Right b
```

Then we’ll derive Eq:

```
data Either a b = Left a | Right b
derive instance eqEither :: (Eq a, Eq b) => Eq (Either a b)
```

Notice how we constrained both a and b to have Eq instances.

Then Ord:

```
data Either a b = Left a | Right b
derive instance eqEither :: (Eq a, Eq b) => Eq (Either a b)
derive instance ordEither :: (Ord a, Ord b) => Ord (Either a b)
```

Once again, notice the constraints.

Next we’ll derive Functor:

```
data Either a b = Left a | Right b
derive instance eqEither :: (Eq a, Eq b) => Eq (Either a b)
derive instance ordEither :: (Ord a, Ord b) => Ord (Either a b)
derive instance functorEither :: Functor (Either a)
```

Notice how we Partially Applied the Type, a, to the Type Constructor Either. That’s because Functor’s Type Parameter has Kind Type -> Type but Either has Kind Type -> Type -> Type. This means we can only map over the b Type Parameter, i.e. the Right of Either.

Next, we’ll derive Generic:

```
data Either a b = Left a | Right b
derive instance eqEither :: (Eq a, Eq b) => Eq (Either a b)
derive instance ordEither :: (Ord a, Ord b) => Ord (Either a b)
derive instance functorEither :: Functor (Either a)
derive instance genericEither :: Generic (Either a b) _
```