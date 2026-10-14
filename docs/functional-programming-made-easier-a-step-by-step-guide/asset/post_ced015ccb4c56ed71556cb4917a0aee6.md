
## 17.4. Code for Applicative Instance for Either

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

Now we can write the instance for `show`:

```
instance showEither :: (Show a, Show b) => Show (Either a b) where
  show = genericShow
```

Notice how both `a` and `b` are constrained to have `Show` Instances.

Next, we write the `Bifunctor` Instance:

```
import Data.Bifunctor (class Bifunctor) ❶

instance bifunctorEither :: Bifunctor Either where
  bimap f _ (Left x)  = Left $ f x
  bimap _ g (Right y) = Right $ g y
```

❶ We need to import the `Bifunctor` class.

And now we’ll write the `Apply` Instance a line at a time. First, the instance definition:

```
instance applyEither :: Apply (Either a) where
```

Notice how we’re specifying `Either a` instead of `Either` for the same reason we do in `Functor`.

Next we will write the `Right` case:

```
instance applyEither :: Apply (Either a) where
  apply (Right f) x = f <$> x
```

Just like we did with `Maybe`, we’re only unwrapping the first parameter and then leveraging the `map` from the `Functor` Instance.

And finally, we write the `Left` case:

```
instance applyEither :: Apply (Either a) where
  apply (Right f) x = f <$> x
  apply (Left y)  _ = Left y
```

Here’s where short-circuiting is applied. We ignore the second Parameter when we have a `Left`. This has the effect of ignoring all subsequent `Rights` and `Lefts` once we encounter our first `Left`. This is the same short-circuiting behavior we implemented with `Maybe` when we encountered a `Nothing`.

The difference to note here is that it really doesn’t matter which `Nothing` we favor since they are all the same. But with `Either`, that’s not the case and so we favor the FIRST `Left`.

Technically, we favor the FIRST `Nothing` too, but we just didn’t think about that with `Maybe`, but we need to think about it with `Either`.

And finally, let’s write the Applicative one line at a time:

```
instance applicativeEither :: Applicative (Either a) where
```

Notice the `Either a` again for all the same reasons.

And we’re going to use the same reasoning we did when we used `Just` as the value for `pure` in `Maybe` by using `Right` since `Left` would annihilate the Pure Value:

```
instance applicativeEither :: Applicative (Either a) where
  pure = Right
```

Run the tests to see how our new code performs.

And it doesn’t:

```
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- bifunctors
```

Add `bifunctors` to your `spago.dhall` and try again.

## 17.5. Validation

In the previous Chapter, we saw we could use `<$>` to call a Function to construct a Full Name while doing validation:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String
                 -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
           <*> (middle `errIfMissing` "Middle name must exist")
           <*> (last `errIfMissing` "Last name must exist")
```

Since this returns an `Either`, which has an Explicit Behavior (or Effect) of Short-circuiting, we only get the first error. In the above example, if both `first` and `last` are missing, we’d never know that.

We’d only get the error regarding the fact that `first` is `Nothing`. But sometimes, we want to accumulate ALL errors.

To do this, we’re going to need something like `Either` without the Short-circuiting behavior.

We’re going to call this Type, `Validation`:

```
newtype Validation err result = Validation (Either err result)
```

Notice how we are simply just wrapping `Either` in a `newtype`. This will allow us to leverage `Either`’s implementation when it suits us, i.e. when `Validation`’s behavior is identical to `Either`, we’ll tell the compiler to derive an instance using `newtype`.

With a new Type we also have the option of overriding certain things we don’t like about `Either`, e.g. how it short-circuits in `apply`.

So, go ahead and add this definition to your code and derive the `Functor` and `Bifunctor` instances using `derive newtype instance`. But don’t forget, to leverage `derive newtype instance`, you first have to derive `Newtype`.

Give it a go before reading on.

Okay, so that was a tall order. Let’s start with the `Newtype` derivation:

```
import Data.Newtype (class Newtype)

newtype Validation err result = Validation (Either err result)
derive instance newtypeValidation :: Newtype (Validation err result) _
```

> Import the `Newtype` class.

Now we’re free to derive `Functor` and `Bifunctor` by leveraging the underlying implementations of `Either` by using `derive newtype instance`:

```
newtype Validation err result = Validation (Either err result)
derive instance newtypeValidation :: Newtype (Validation err result) _
derive newtype instance functorValidation :: Functor (Validation err)
derive newtype instance bifunctorValidation :: Bifunctor Validation
```

Let’s round out our derivations by deriving `Eq` and `Ord`. Give it a try before continuing on.

There are 2 ways to do the derivation. With or without the newtype:

```
derive newtype instance eqValidation ::
  (Eq err, Eq result) => Eq (Validation err result) ①
derive instance eqValidation ::
  (Eq err, Eq result) => Eq (Validation err result) ①
```

① Each line of code is valid, just not both.

So, since they’re equivalent, no sense typing the extra word:

```
derive instance eqValidation ::
  (Eq err, Eq result) => Eq (Validation err result)
derive instance ordValidation ::
  (Ord err, Ord result) => Ord (Validation err result)
```

Our new Type is pretty capable for most common operations at this point and not different from Either, yet.

The next step is the whole reason for this Type. We want to write an Apply Instance that collects all of the errors in some sort of Semigroup or Monoid.

When faced with this choice, it’s best to choose the simplest constraint to start, i.e. Semigroup. The compiler will let us know if we need a Monoid, e.g. if we use mempty and didn’t realize it.

But if we constrain our Type to Monoid right out of the gate, then the compiler will NOT complain if we don’t use mempty. It’s up to us to remember to ask the question, "Did we constrain our Type too much".

Stop reading here and code the Apply Instance to collect the errors in a Semigroup as opposed to short-circuiting like Either. Try not to read ahead to the answer.

To code the Apply instance, let’s start with the instance definition:

```
instance applyValidation :: Semigroup err => Apply (Validation err) where
```

Notice that we constrain the error Type to be a Semigroup so we can collect the errors up in it. In practice, Array a is the most likely candidate for this Type, where a is some error Type. The simplest example being String.

Next, we code the error case where we combine errors:
