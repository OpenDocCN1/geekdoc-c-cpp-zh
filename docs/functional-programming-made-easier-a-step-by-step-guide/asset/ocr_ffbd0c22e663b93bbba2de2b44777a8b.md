```
import Data.Traversable (class Traversable, sequence) ①

count :: ∀ e a f. Traversable f => Int -> Parser e a -> Parser e (f a) ②
```

① We added class Traversable to the import list.

② We’ve abstracted Array with our Type Parameter f. Now f can stand for List or Array, and even MyTree (assuming your tree has a Traversable Instance).

Next, we should recode the Function. First the error case:

```
count :: ∀ e a f. Traversable f => Int -> Parser e a -> Parser e (f a)
count n p
  | n <= 0 = ???
```

Now we’re stuck. We need an empty value here. How can we get an empty value when we don’t know what type f is?

If you’re screaming out Monoid, you’re on the right track. But I’m going to save you the compiler errors by mentioning that f’s Kind is Type -> Type, but Monoid’s Type is just Type. So that won’t work.

We need a Monoid for Type -> Type. Do you remember what that’s called?

Did you say Plus? I thought so.

So let’s add that constraint and use empty from Plus:

```
import Control.Plus (class Plus, empty) ①

count
  :: ∀ e a f
    . Plus f
    => Traversable f
    => Int
    -> Parser e a
    -> Parser e (f a)
count n p
  | n <= 0 = pure empty ②
  ???
```

① We’re going to need to explicitly import these.

② We return an empty value here, e.g for List it’s Nil and for Array it’s [].

Now we’re ready to write the valid case: