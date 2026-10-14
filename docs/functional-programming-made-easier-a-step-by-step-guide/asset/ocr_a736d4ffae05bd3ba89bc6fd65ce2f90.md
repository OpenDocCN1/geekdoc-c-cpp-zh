Notice that we start with `mempty`. There are two reasons for this. First, because our `List` could initially be empty and second, because we want an initial value that won’t affect the result of the append operation. Much like multiplying by `1` or adding `0`.

We could not do this with just a `Semigroup` Constraint since Semigroups do not have Empty Elements.

But what if we wanted to write a version where we could also allow Semigroups? We could start with the first element instead of the Empty Element. But there’d be no first element if the `List` is empty.

We need a way to guarantee that the list isn’t empty and we can do this by using the `NonEmpty` Type.

Let’s write a similar function but for NON-Empty `Lists`:

```
import Data.List (List)
import Data.NonEmpty (NonEmpty(..))

combineNEListOfSemigroups :: ∀ a. Semigroup a => NonEmpty List a -> a
combineNEListOfSemigroups (NonEmpty x xs) = go x xs where
  go c Nil = c
  go c (y:ys) = go (c <> y) ys
```

+   1. It’s common practice to keep your imports in alphabetical order. That’s why `Data.List` is before `Data.NonEmpty`.
+   2. We need to import the constructors so we can destructure the Non-empty `List`.
+   3. Now that we disallow empty `Lists`, we can relax our requirements on `a` and allow `Semigroups`.
+   4. We now have to start with the head of the `NonEmpty` since we no longer have `mempty`. But since the `List` is guaranteed by the `NonEmpty` Type to always have at least 1 element, we can get the `head` with no fear of failure.

The body of the code is very similar to `combineListOfMonoids`. But this `NonEmpty` Type is new to us, so let’s take a closer look.

Here is the definition of `NonEmpty`:

```
data NonEmpty f a = NonEmpty a (f a)

infixr 5 NonEmpty as :|
```

Binary Operator for constructing a `NonEmpty`. Notice that it’s very similar to `List`’s Cons operator, `:`.

Notice how `NonEmpty` takes 2 Type Parameters. `f` is the collection Type and `a` is the element Type. It could’ve been define as: