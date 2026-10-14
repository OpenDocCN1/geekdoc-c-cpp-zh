
![](img/8c0e9b687c62642e828ccb5481e11313_703_0.png)

It found a `b` but wants a `Maybe t1`. Not super helpful other than telling us that the Types don’t match. The red underline is a clue that the compiler is referring to the Function, `f`.

To figure out what’s wrong, let’s add in the Type Signature for `apply` specialized for `Maybe`:

```
instance applyMaybe :: Apply Maybe where
  apply :: ∀ a b. Maybe (a -> b) -> Maybe a -> Maybe b
  apply mf mx = mf >>= \f -> mx >>= f   -- COMPILER ERROR!!
```

This makes it easier for us to write down all of the Types of our variables paying particular attention to `f`:

```
mf :: Maybe (a -> b)
f  :: a -> b
mx :: Maybe a
```

Can you see what’s wrong now?

Maybe if we write the Type Signature for `bind`, `>>=`, specialized for `Maybe` it will become apparent:

```
bind :: ∀ a b. Maybe a -> (a -> Maybe b) -> Maybe b
```

Look at the Types of our variables and `mx >>= f` to see if you can spot the problem now. Try to figure out the issue before reading on.

We know that that `f` is the problem since the red underline was under the `f`. `f` is the second Parameter to `bind`, which means its Type Signature is supposed to be `a -> Maybe b` but it’s not. Instead, `f`’s Type Signature is `a -> b`.

We can fix this by composing it with `pure` to wrap the `b` that `f` returns in a `Maybe`:

```
instance applyMaybe :: Apply Maybe where
    apply mf mx = mf >>= \f -> mx >>= pure <<< f
```

Okay, so this was a bit of work and not intuitive at all. It’s also hard to read with all of the operators.

So let’s rewrite it using do notation:

```
instance applyMaybe :: Apply Maybe where
    apply mf mx = do
        f <- mf ①
        x <- mx ②
        pure $ f x ③
```

- ① First, extract the Function, `f`.
- ② Then extract the Value, `x`.
- ③ Apply `f` to `x` and wrap it back up into the Context via `pure`.

This is so much easier to read and, therefore, easier to reason about.

Notice how this code is independent of the fact that we’re working with `Maybe`. That’s because we wrote it using `pure` instead of `Just`. That means we can make a helper Function. Let’s call it `ap`:

```
ap :: ∀ a b m. Monad m => m (a -> b) -> m a -> m b ①
ap mf mx = do
    f <- mf
    x <- mx
    pure $ f x
```

① We have to constrain the Context, `m`, to be a `Monad` since we use `>>=` from `Bind` and `pure` from `Applicative`. Remember, `Monad` is a `Bind` and an `Applicative`.

Now we can rewrite `apply` for `Maybe` using `ap`:

```
instance applyMaybe :: Apply Maybe where
    apply = ap
```

Wow, that’s much simpler. By the way, the `ap` Function we wrote already exists in the `Control.Monad` module. Turns out that `ap` is considered so useful, that it’s imported by `Prelude`.

We can use `ap` like this on any Type that is going to be a `Monad`, but realize when you first code it up, the compiler may complain because you haven’t written the `Bind` or `Monad` Instances yet.

## 18.14. Monad Instance for Either

Before we write the Monad Instance for `Either`, let’s look at what we’ve written for `Either` so far:

```
data Either a b = Left a | Right b

instance functorEither :: Functor (Either a) where
  map _ (Left err) = Left err
  map f (Right x) = Right $ f x

instance applyEither :: Apply (Either a) where
  apply (Left y) _ = Left y
  apply (Right f) x = f <$> x

instance applicativeEither :: Applicative (Either a) where
  pure = Right
```

This implementation is very similar to `Maybe`, so writing the `Bind` Instance for `Either` should be equally simple.

First, the instance definition:

```
instance bindEither :: Bind (Either a) where ①
```

① Holding `a` constant.

Next, the error case:

```
instance bindEither :: Bind (Either a) where
  bind (Left y) _ = Left y
  ???
```

And finally, the success case:

```
instance bindEither :: Bind (Either a) where
  bind (Left y) _ = Left y
  bind (Right x) f = f x ①
```

① Remember, `f` will return an `Either` so we don’t have to worry about wrapping it back up.

And writing the Monad Instance is trivial:

```
instance monadEither :: Monad (Either a)
```

We technically should verify the Monad Laws, but since its implementation is analogous to `Maybe` and `Either a` is Isomorphic to `Maybe`, we’ll just assume it doesn’t break any laws. But, if we were so inclined to prove the laws, we could simply substitute `Nothing` with `Left y` and `Just` with `Right` in the proof we did for `Maybe`.

One final thing we can do here is compare `apply` to `bind`:

```
instance applyEither :: Apply (Either a) where
  apply (Left y) _ = Left y
  apply (Right f) x = f <$> x

instance bindEither :: Bind (Either a) where
  bind (Left y) _ = Left y
  bind (Right x) f = f x
```

Once again, we can see that these implementations are more alike than not. They both short-circuit when `Left` is encountered. We could write `apply` in terms of `bind` by using `ap`:

```
instance applyEither :: Apply (Either a) where
  apply = ap
```

You may be wondering if doing this always works. Well, let’s think about it for a second.

Any `apply` implementation SHOULD have the same Semantics, i.e. behavior, as the `bind` implementation. If it does not, it will most likely break the `Apply` or `Monad` Laws. But even if it doesn’t, it would be a terribly designed Type if the `Apply` had different Semantics from `Bind`.

In the case of `Maybe` and `Either`, they short-circuit. And both the `Apply` and `Bind` Instances should exhibit this behavior. With `Maybe`, we have no choice since short-circuiting is intrinsic to the Data Structure. But with `Either`, we made an explicit decision to short-circuit, therefore, we’d want our `apply` and `bind` implementations to both short-circuit.

So, by all reasonable measures, `ap` SHOULD be able to do the work of `Apply` in all cases. While it is possible to create a Type that has inconsistent Semantics and, therefore, `ap` could not be used to produce this nefarious Type, I would advise strongly against ever doing so.

When we return to our Parser, we’ll see that its `Apply` Instance could easily be replaced with `ap`, that is after we write the `Monad` Instance.

## 18.15. Working with Either Monad

We can do computations within the `Either` Monad in nearly identical ways to the `Maybe` Monad with the only discernible difference being that `Left` gives us more information than `Nothing`.

Let’s rewrite our tests from the Maybe Section:

```
import Data.Int.Bits ((.&.))

oddTest :: Int -> Either String Int
oddTest x = if x .&. 1 == 1 then Right x else Left "Number is not odd"

greaterThanTest :: Int -> Int -> Either String Int
greaterThanTest min x =
    if x > min then Right x
    else Left $ "Number is not greater than " <> show min

lessThanTest :: Int -> Int -> Either String Int
lessThanTest max x =
    if x < max then Right x
    else Left $ "Number is not less than " <> show max
```

Now we can rewrite `gauntlet`:

```
gauntlet :: Int -> Either String Int ①
gauntlet x = do
    o <- oddTest x
    let y = o + 1
    void $ greaterThanTest 10 y
    lessThanTest 20 y
```

① `Maybe` was replaced with `Either String`.

What’s interesting is that we only had to change the Type, i.e., once we changed our test Functions. That’s because `gauntlet` was written using `bind`, which is a TypeClass Method.

The `gauntlet` example is pretty contrived. So, let’s use `Either` to do an example that’s a bit more realistic.

Let’s revisit our `fullName` Function from an earlier Chapter:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String
    -> Either String String
fullNameEither first middle last =
    fullName <$> (first `errIfMissing` "First name must exist")
        <*> (middle `errIfMissing` "Middle name must exist")
        <*> (last `errIfMissing` "Last name must exist")
```

Let’s rewrite this using Monadic computation with do notation:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String
    -> Either String String
fullNameEither first middle last = do
    f <- errIfMissing first "First name must exist"
    m <- errIfMissing middle "Middle name must exist"
    l <- errIfMissing last "Last name must exist"
    pure $ fullName f m l
```

Personally, I like the Applicative version better, but when the computation is more complex, I’ll reach for the Monadic version. It really depends.

The Monadic version still suffers from the same problem as our Applicative one does and that is we only get the first error. We have an Applicative called `Validation` that we used to collect all of the errors.

I wonder if we can make that a Monad.

## 18.16. Adding Monad Instance for Validation

Let’s start with what we’ve written so far for `Validation`:

```
newtype Validation err result = Validation (Either err result)
derive newtype instance functorValidation :: Functor (Validation err)

instance applyValidation :: Semigroup err => Apply (Validation err) where
    apply (Validation (Left err1)) (Validation (Left err2))
        = Validation $ Left (err1 <> err2)
    apply (Validation (Left err)) _ = Validation $ Left err
    apply (Validation (Right f)) x = f <$> x
```

Now let’s write the Bind Instance one line at a time:
