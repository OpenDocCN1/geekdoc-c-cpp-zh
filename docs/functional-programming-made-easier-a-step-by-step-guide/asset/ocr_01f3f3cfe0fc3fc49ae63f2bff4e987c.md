Notice that a single Nothing in the List, short-circuits and produces Nothing.

Just in case this still seems like Black Magic, we’re going to look at a simpler version of this example one step at a time.

Here’s our function:

```
combineList :: ∀ a f. Applicative f => List (f a) -> f (List a)
combineList Nil      = pure Nil ①
combineList (x : xs) = Cons <$> x <*> combineList xs ②
```

We’re going to do Algebraic Substitution and Function Application to see how each step of the computation process works:

```
combineList (fromFoldable [Just 1, Just 2])                 -- Given
combineList (Just 1 : Just 2 : Nil)                         -- Apply fromFoldable
Cons <$> Just 1 <*> combineList (Just 2 : Nil)              -- Substitute into ②
Just (Cons 1) <*> combineList (Just 2 : Nil)                -- Apply $<>
Just (Cons 1) <*> (Cons <$> Just 2 <*> combineList Nil)     -- Substitute into ②
Just (Cons 1) <*> (Just (Cons 2) <*> combineList Nil)       -- Apply $<>
Just (Cons 1) <*> (Just (Cons 2) <*> pure Nil)              -- Substitute into ①
Just (Cons 1) <*> (Just (Cons 2 Nil))                       -- Apply <*>
Just (Cons 1 (Cons 2 Nil))                                  -- Apply <*>
Just (1 : 2 : Nil)                                          -- Rewrite with :
```

Now let’s look at Either:

```
import Data.List (fromFoldable)

combineList (fromFoldable [Right 1, Right 2, Right 3])
  -- (Right (1 : 2 : 3 : Nil))
combineList (fromFoldable [Right 1, Left "err", Right 3, Left "err2"])
  -- (Left "err")
```

And we see that the FIRST Left short-circuited to produce Left "err". The rest of the List was effectively ignored.

It’s important to understand that it was still processed since PureScript is a Strict language. In Haskell, a Lazy language, this would NOT be the true making Haskell more efficient in this case.