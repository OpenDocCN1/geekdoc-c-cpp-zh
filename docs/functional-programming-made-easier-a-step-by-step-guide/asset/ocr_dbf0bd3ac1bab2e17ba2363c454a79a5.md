have to check for errors. The `Either` Monad does that for us in the `bind` implementation.

Don’t read any further until you’re finished coding.

Let’s use the current implementation as our reference and note what each step does:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> case parse p1 s of ❶
    Left err -> Left err ❷
    Right (Tuple s1 h) => case parse p2 s1 of ❸
      Left err -> Left err ❹
      Right (Tuple s2 x) -> Right $ Tuple s2 (h x) ❺
```

+   ❶ Execute first `Parser`, `p1`.
+   
+   ❷ Check for errors.
+   
+   ❸ Execute second `Parser`, `p2`.
+   
+   ❹ Check for errors.
+   
+   ❺ Apply the returned Function, from `p1`, to the returned Value, from `p2`, and wrap everything up in a `Tuple` in an `Either`.

Let’s start with this:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    ???
```

`apply` returns a `Parser`, which contains a Function that takes a `String`, `s` and returns an `Either`, represented by the `do` block.

The first thing we did in our old code was to execute `Parser`, `p1`. Let’s add that:

```
instance applyParser :: Apply (Parser e) where
  apply p1 p2 = Parser \s -> do
    ??? <- parse p1 s
```

We just need to capture what it returns. But, remember, when we code in the Either Monad, we code JUST the Happy Path. So, if `parse p s` SUCCEEDS, then it returns a Value of Type `ParserState a`, which is `Tuple String a`. This is the `Right` side of the `Either` since we’re only concerned with the Happy Path.

Let’s add that: