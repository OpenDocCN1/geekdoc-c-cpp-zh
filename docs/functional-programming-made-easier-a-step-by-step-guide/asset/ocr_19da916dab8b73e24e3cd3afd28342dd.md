```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    Tuple s1 f <- parse p1 s ①
    ???
```

① f represents the Function that's returned from the Parser. Remember, the first Parser in an Apply returns a Function and the second Parser returns a Value.

The next thing we did in our old code was to check for errors. We do NOT need to do that since it's handled by the Either Monad.

After that, we executed p2. Let's add that and capture its successful results:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    Tuple s1 f <- parse p1 s
    Tuple s2 x <- parse p2 s1 ①
    ???
```

① x represents the Value that's returned from the Parser. Remember, the first Parser in an Apply returns a Function and the second Parser returns a Value.

The next thing our old code did was to check for errors from the second Parser, but, once again, we don't have to check for errors in the Either Monad. That's bind's job. And, even though the do syntax obscures the use of bind, it is being used between each line of code in the do block.

And the final thing our old code did was to apply the returned Function, from p1, to the returned Value, from p2, and wrap everything up in a Tuple in an Either:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    Tuple s1 f <- parse p1 s
    Tuple s2 x <- parse p2 s1
    pure $ Tuple s2 $ f x ①
```

① You may still not be used to this syntax, i.e. all the $'s. It's used quite often in idiomatic PureScript and Haskell. It's equivalent to pure $ Tuple s2 (f x).

We use pure here instead of Right. Technically, you can use Right but by using pure, we can swap out Monads, if, for example, parse changes to return something other than Either, and our code will still work. This is because the compiler will use the new Monad's implementation for pure.

We saw this when we changed fullNameEither, which we eventually renamed to fullNameValid. It went from returning an Either to returning a State and later a Writer. The final line in the do block used pure