And now a new compiler error that tells us that we cannot compare `Maybe` for equality. But that’s easy enough to fix and I’ll let you fix that one.

Go ahead and make it so `Maybes` can be compared for equality and run this test before proceeding.

First step is to add `Eq` Instance for `Maybe`:

```
```haskell
import Data.Eq (class Eq) ❶

derive instance eqMaybe :: Eq (Maybe a) — COMPILER ERROR!!
```
```

❶ We could’ve also imported this from Prelude.

The compiler error should look familiar. See if you can solve it before reading on.

Once again, if we want to compare `Maybe a` for equality, we have to be able to compare `a` for equality, which means we need an `Eq` Constraint:

```
```haskell
import Data.Eq (class Eq)

derive instance eqMaybe :: Eq a => Eq (Maybe a)
```
```

But now we STILL have trouble:

```
```text
log $ show $ "Maybe Identity for Nothing: "
  <> show ((identity <$> Nothing) == Nothing) — NEWER COMPILER ERROR!!
```
```

This time the error is telling:

```
```text
No type class instance was found for

  Data.Eq.Eq t1

The instance head contains unknown type variables. Consider adding a type annotation
```
```

And we’ve seen this before. The compiler cannot figure out if `a` has an `Eq` Instance since it cannot figure out what `a` is. So, like so many times before, we’re going to give it an `a`, viz. `Unit`, the simplest Type:

```
```text
log $ show $ "Maybe Identity for Nothing: "
  <> show ((identity <$> Nothing) == (Nothing :: Maybe Unit)) ❶ ❷
```
```