
```
```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = f unit -- WRONG!
```
```

This will compile but it won’t defer the evaluation. This is because `f unit` gets evaluated immediately.

The way to get this to be deferred is to create a brand new `Parser` like we’ve done in the past:

```
```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> ???
```
```

Now, we’ll get the Parser out of the Function, `f`, by passing it `unit`:

```
```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> f unit -- COMPILER ERROR!!
```
```

We’re going to get a compiler error since we’re not done yet. So, we’ll ignore it.

Since `f unit` is a `Parser`, we’ll need to run it by using `parse` along with the `String` to parse, i.e. `s`:

```
```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> parse (f unit) s
```
```

Let’s step back for a second and appreciate what we’ve just built. We have a `Parser` that when run will execute another `Parser` and do nothing else. On the surface, the outer `Parser` seems redundant and it is except for the fact that it will DELAY the execution of the inner `Parser` until the outer `Parser` is EXECUTED.

What’s great about the outer `Parser`, is that it’s Functionally equivalent to the inner one, except that it’s NOT identical to the inner one. That means that we can use it as a safe replacement for ANY `Parser` at any time or place and it won’t affect the result of parsing.

But, the only real benefit to using this `Parser` proxy is when we can break a Mutual Recursive definition as we have with `some` and `many`.

By the way, if the `Lazy` Typeclass didn’t exist, we could’ve just written a `Parser` Combinator called `defer` that would have accomplished the same objective:

```
```haskell
defer :: ∀ e a. (Unit -> Parser e a) -> Parser e a
defer f = Parser \s -> parse (f unit) s
```
```

This isn’t as general and, therefore not as nice, as the `Lazy` Typeclass, but will work just the same.

Go ahead and add the following to your code:

```
```haskell
import Control.Lazy (class Lazy)

instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \s -> parse (f unit) s

some :: ∀ e a. Parser e a -> Parser e (Array a)
some p = (:) <$> p <*> many p

many :: ∀ e a. Parser e a -> Parser e (Array a)
many p = some p <|> pure []
```
```

Now, we want to defer the `many` call in the `some` implementation. We’re going to do this by replacing it with a deferred `Parser`:

```
```haskell
import Control.Lazy (class Lazy, defer) ①

some :: ∀ e a. Parser e a -> Parser e (Array a)
some p = (:) <$> p <*> defer \_ -> many p ②
```
```

> ① We need to add `defer` to the import list.
> 
> ② `defer \_ -> many p` is our stand-in `Parser` that’s functionally equivalent to `many p`.

Make this change to your code.

Now, write `some'` and `many'` that return `Parser e String`. You can look back at how we did this with `count'` and `range'`. Do this before moving on.

Here’s the implementations:

```
```scala
some :: V e a f. Unfoldable f => Parser e a -> Parser e (f a)
some p = (:) <$> p <*> defer \_ -> many p   // COMPILER ERROR!!
```
```

+   1. Added `f` to `V`.
+   2. Added `Unfoldable` Constraint on `f`.
+   3. Replaced `Array` with `f`.

We’ve got an error because we haven’t replaced `Array`’s `Cons` Operator, `(:)`, yet.

Let’s do that now:

```
```scala
some :: V e a f
     " Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (f a)
some cons p = cons <$> p <*> defer \_ -> many p   // COMPILER ERROR!!
```
```

An additional Parameter was added for the cons-like Function.

The compiler is complaining about the following:

![](img/8c0e9b687c62642e828ccb5481e11313_839_0.png)

Notice that it’s underlined the call to `many`. That’s because we haven’t changed `many`, yet.

Let’s do that now:

```
many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a) ①
-> Parser e a
-> Parser e (f a)
many cons p = some cons p <|> pure [] -- COMPILER ERROR!! ②
```

① Same changes we made to the Type Signature for some.

② The only reason we need the cons Parameter is because some needs it.

Now we have to replace [] with none:

```
many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
many cons p = some cons p <|> pure none ①
```

① Replaced [] with none.

Now many compiles but some has a new error:

```
some :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
some cons p = cons <$> p <*> defer \_ -> many p -- COMPILER ERROR!!
```

Here’s that error:

![](img/8c0e9b687c62642e828ccb5481e11313_840_0.png)

When the compiler looked at the first Parameter of our call to `many`, it found a `Parser`, `p`, but expected a `Function`. That’s because we added the `cons` Parameter to `many` but forget to add it to our call.

Let’s fix that now:

```
some :: ∀ e a f
     . Unfoldable f
     => (a -> f a -> f a)
     -> Parser e a
     -> Parser e (f a)
some cons p = cons <$> p <*> defer \\_ -> many cons p ①
```

> ① Added `cons` as `many`’s first Parameter.

Now, the compiler is making a similar complaint about `many`, which we’ll fix in a similar way:

```
many' :: ∀ e. Parser e Char -> Parser e String
many' p = fromCharArray <$> many (:) p ①
```

> ① Added the `(:)` Operator as our cons-like Function.

We might as well fix `some'` before the compiler complains about it too:

```
some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <$> some (:) p ①
```

> ① Added the `(:)` Operator as our cons-like Function.

At this point we could stop, but stepping back and looking over the code we’ve written, we can see that `some` will never return an empty `Unfoldable` since it’s supposed to parse 1 or more.

How can we change it to reflect this restriction?

Do you remember `NonEmpty`? Here’s it’s definition:

```
data NonEmpty f a = NonEmpty a (f a)
```

We can use this on `some` but NOT `many` since it can be empty, since `many` is 0 or more. This means that when `many` calls `some`, we’ll have to convert the `NonEmpty` that we get back to something that can be empty.

Okay, so one problem at a time. Let’s first modify `some` to return `NonEmpty`:

```
```haskell
import Data.NonEmpty (NonEmpty, (:|))

some :: V e a f
  :| Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (NonEmpty f a)
some cons p = (:|) <$> p <*> defer \\_ -> many cons p
```
```

+   1. Added this import Statement.
+   2. `f a` changed to `NonEmpty f a`.
+   3. Replaced the first `cons` with the `NonEmpty` Cons Operator but left the second `cons` alone since `many` need to use it.

Now, the compiler is complaining about `many`:

![](img/8c0e9b687c62642e828ccb5481e11313_842_0.png)

From the error and red underline, it should be clear that it’s complaining because we haven’t converted `some`’s return value, i.e. a `NonEmpty` to something that’s NOT `NonEmpty`, which is what `many` returns.

We need a way to convert a `NonEmpty f a` to `f a`. Searching `Pursuit` for `NonEmpty f a -> f a` produces nothing useful. Searching `Pursuit` for `NonEmpty` displays all the `NonEmpty` Functions, which, if you browser through carefully, will reveal a possible candidate called `fromNonEmpty`.

Here’s it’s Type Signature:

```
```haskell
fromNonEmpty :: ∀ a r. (a -> f a -> r) -> NonEmpty f a -> r
```
```

The Type Signature isn’t what we searched for, but if we replace `r` with `f a` then it’s exactly what we want. We just have to give it a `cons` Function, which, luckily, we have.

Let’s use `fromNonEmpty` to convert the return Value from `some` in `many`:

```
import Data.NonEmpty (NonEmpty, (:|), fromNonEmpty) ①

many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none ②
```

① Added fromNonEmpty to import list.

② We map fromNonEmpty cons over some.

And now, we get an error on some':

![](img/8c0e9b687c62642e828ccb5481e11313_843_0.png)

The error says that it got a NonEmpty Array when it expected Array. Looks like we need to convert the return value here too:

```
some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <<< fromNonEmpty (:) <$> some (:) p ①
```

① Composed fromNonEmpty (:) with fromCharArray, which gets mapped over some's return Type, i.e. NonEmpty Array Char.

And the compiler is finally quiet.

Here's our final generalized code:
