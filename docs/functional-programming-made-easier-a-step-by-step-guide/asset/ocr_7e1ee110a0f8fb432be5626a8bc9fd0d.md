# But what’s `Unfoldable`?

Back when we talked about Folds, I mentioned Unfolds and how they were **Anamorphisms**, i.e. Functions that build up structure as opposed to Folds which are **Catamorphisms** that break down structure. Well, `replicate` starts with a seed, in our case a `Parser`, and it produces a bunch of them in an `Array` or `List` or some another `Unfoldable` from that one `Parser`.

So, we probably can use this since `Array` and `List` have `Unfoldable` instances. You can see this fact in Pursuit, but you’ll have look in different places for each. Since `Array` is a base Type in PureScript, the `Unfoldable` Typeclass code implements it. In the case of `List`, which is not a base Type, it’s implemented in the same Module as `List`.

Remember Orphaned Instances? Well, that’s why you’ll find these in those 2 different places. Those are the only valid places one can put instances.

So let’s add the import for `replicate`, the `Unfoldable` version:

```
```purescript
import Data.Unfoldable (replicate)

count
  :: ∀ e a f
   . Plus f
  => Traversable f
  => Int
  -> Parser e a
  -> Parser e (f a)
count n p
  | n <= 0     = pure empty
  | otherwise = sequence (replicate n p) -- COMPILER ERROR!!
```
```

Once again, the compiler is complaining: