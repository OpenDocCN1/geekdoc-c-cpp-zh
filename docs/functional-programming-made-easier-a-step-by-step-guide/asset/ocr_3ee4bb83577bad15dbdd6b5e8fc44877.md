We’ll want to test boundary conditions. There are 3. One, when we pass a count of 0 or less. Two, when we can’t parse anything. And three, when we could parse more but stop because we’ve hit the max.

Before we write those tests, let’s write a version of `atMost` called `atMost'` that returns `Parser e String`. Look to `count'` to see how to do this. Write that Function before reading on.

Here’s that Function:

```
atMost' :: ∀ e. Int -> Parser e Char -> Parser e String
atMost' n p = fromCharArray <$> atMost n p
```

The reason we’re writing our `Parsers` to be `Parser e a` is for the greatest flexibility. We may want to use our `Parser` in a non-text scenario. But, generally speaking, we’re mostly going to use it with `Strings`, which is why we’re writing the prime versions, e.g. `atMost'`.

Now add the following to your test code and run it to make sure `atMost'` works:

```
log $ show $ parse' (atMost' (-2) alphaNum) "a1b2c3" ❶
log $ show $ parse' (atMost' 2 alphaNum) "$_$" ❷
log $ show $ parse' (atMost' 2 alphaNum) "a1b2c3" ❸
```

+   ❶ Prints `(Right (Tuple "a1b2c3" ""))`.
+   
+   ❷ Prints `(Right (Tuple "$_$" ""))`.
+   
+   ❸ Prints `(Right (Tuple "b2c3" "a1"))`.

If that prints out what we expect then we’re good to go on to `range`.

But... before that, we promised ourselves that we’d generalize `atMost` later. It’s really easy to just look at it and decide that it’s fine the way it is, since it was difficult to write in the first place. If you’re feeling that way now, maybe it’s a good time to take a break and return here when you’re ready.

I think it’s worth making any library Function as flexible as possible. And, `atMost`, is clearly a general purpose `Parser`. So it’s worth looking at it in that light.

Here’s our current version:

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0    = pure []
  | otherwise = optional [] $ p >>= \c -> (c : _) <$> atMost (n - 1) p
```

We could change `Array` to an `Unfoldable` like we did in `count`. That worked out nicely. So, copy this Function and comment out one of the copies. We’ll keep it around in case our experiment goes awry.