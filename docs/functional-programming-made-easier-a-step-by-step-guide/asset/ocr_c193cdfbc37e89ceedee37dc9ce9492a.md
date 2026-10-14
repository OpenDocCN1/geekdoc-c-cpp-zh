Let’s do this one step at a time. First, let’s refactor what we wrote. Even though it’s wrong, refactoring will help us see how to `map` the `Cons` Operator.

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0     = pure []
  | otherwise = p >>= \c -> (c : _) $ atMost (n - 1) p
  -- COMPILER ERROR!!
```

We’re still applying `Cons` to a `Parser`, so we haven’t fixed anything. This refactoring step is just to help you see what to do next.

But before you do, take a minute to see how `c : []` is the same as `(c : _) $ []`.

Now, instead of Function Application, `$`, we’re going to change the code to use `map`, `<$>`:

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0     = pure []
  | otherwise = p >>= \c -> (c : _) <$> atMost (n - 1) p
```

Now, this compiles. But does it work?

Let’s look at what it does. First, it’s a `Parser`. And that `Parser` will first parse using `p` and if that succeeds then... Wait. What happens if `p` fails?

If `p` fails, then `atMost` fails. That means that the whole `Parser` fails. And since we recurse with `atMost`, if at any point that fails then the whole thing fails.

We never want `atMost` to fail. We want it to OPTIONALLY parse no more than the specified number of elements. So `atMost` should ALWAYS succeed.

Okay, so this code won’t work as it stands. We need to handle the cases where `p` or `atMost (n − 1) p` fails, or the combination of them fails.

We could add of bunch of checks inside `atMost` but that’ll be a mess. So, we’re going to factor it out.

We’re going to write a `Parser`, called `optional`, that takes another `Parser` and if it fails, it defaults with a default Value.

Go ahead and write just the Type Signature. Then read on.

Here’s the Type Signature for `optional`: