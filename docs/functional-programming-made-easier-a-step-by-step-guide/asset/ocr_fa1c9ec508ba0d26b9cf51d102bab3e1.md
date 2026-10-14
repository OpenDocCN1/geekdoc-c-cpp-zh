The problem is that we’re still using a hardcoded Initial State, which is the Additive Identity for Numbers. And we know that if we change it to 0, the Additive Identity for Ints, we’ll still get a similar error.

What we need is the Additive Identity for any Semiring. Luckily, the Semiring Typeclass has the very thing we need. It’s called zero.

The compiler will pick the appropriate zero for Ints or Numbers or any Type that has a Semiring instance.

Let’s review the Semiring definition:

```
class Semiring a where
  add :: a -> a -> a ①
  zero :: a ②
  mul :: a -> a -> a
  one :: a

infixl 6 add as + ③
infixl 7 mul as *
```

① Here’s the add function.

② This is the Additive Identity.

③ The Operator Alias for add is +.

Armed with this refresher, we can fix our compiler error by replacing the 0.0 with zero:

```
import Data.Semiring (class Semiring, zero) ①

sum :: ∀ a. Semiring a => List a -> a
sum = foldl (+) zero
```

① Added zero to the import list.

The compiler will chose the appropriate zero for the Semiring. When the Semiring is Int, it’ll use 0 and when it’s Number, it’ll use 0.0.

And this will work for ANY Semiring.

The compiler will also choose the appropriate add for the Semiring. Remember, each Semiring has its own implementation for add.

Now we’ve greatly improved our sum function because it isn’t limited to just Ints.

But... We’re not finished. We can do better. Can you see what the next improvement should be?