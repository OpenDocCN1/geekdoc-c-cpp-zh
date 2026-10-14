Now, before reading any further, rewrite this Function using do notation. Call it twoChars.

We’ll start with the exact same Type Signature as before:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
```

Next, we’ll add the do:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = do
  ???
```

Next we’ll call char and capture the character it’ll return:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = do
  c1 <- char
  ???
```

And now we’ll do it again:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = do
  c1 <- char
  c2 <- char
  ???
```

And finally, we’ll return the result in a Tuple:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = do
  c1 <- char
  c2 <- char
  pure $ Tuple c1 c2 ❶
```

> ❶ Again, don’t forget to wrap the Tuple in a Parser since that’s the Type that we’re returning.

You should be able to test using our old test code, if you like.

Here’s another Parser we wrote using Apply: