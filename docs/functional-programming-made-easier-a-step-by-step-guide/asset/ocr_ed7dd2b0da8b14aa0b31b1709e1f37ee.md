We can generalize this by stating that `Functors` of Values will apply mapping Functions IMMEDIATELY, whereas `Functors` of Functions will DEFER their execution until the `Functor` is "run", e.g. `runReader`, `runState` or `parse`. We’ve recently seen mapping Functions deferred in `Reader`, `State` and now `Parser`.

Understanding this can help us think about the following code in 2 equally valid ways, abstractly or concretely:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = Tuple <$> char <*> char
```

Thinking abstractly, we can say: `Tuple` is mapped over the first `Parser`, `char`, to produce a `Parser` of Type `Parser e (a -> Tuple Char a)`. Then that `Parser` will be applied to the second `Parser`, `char`, to produce a `Parser` of `Parser e (Tuple Char Char)`.

Thinking concretely, we can say: The result of running the first `Parser`, `char`, will be mapped over by the `Tuple` Data Constructor, which will be short 1 Parameter. This Value will supplied by running the second `Parser`, `char`, to produce a final result of Type `Tuple Char Char`.

Either way is good. But, the second way really explains what’s going on under the hood and hopefully, lessens that feeling of magic or of confusion, which is caused by the fact that so much of the `Parser` code is hidden from our everyday view thanks to `<$>`, `<*>`, `>>=` and the `do` notation.

We have to keep in mind that we’ve written a lot of code that’s hidden in those instance implementations.

Now, let’s look at `apply`:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    Tuple s1 f <- parse p1 s
    Tuple s2 x <- parse p2 s1
    pure $ Tuple s2 $ f x
```

And let’s compare it against `Maybe`:

```
instance applyMaybe :: Apply Maybe where
  apply Nothing  _ = Nothing
  apply (Just f) x = f <$> x
```

Once again, we can see that `Maybe`’s implementation applies the mapping Function immediately, whereas, in `Parser`, the Function is deferred until the `Parser` is executed.

This is why we think of these mapping Functions as operating on what the `Parser` *returns*, i.e. if you have a `Parser e (Array Char)` and you map `fromCharArray` over it, you get a `Parser` that returns a `String`.