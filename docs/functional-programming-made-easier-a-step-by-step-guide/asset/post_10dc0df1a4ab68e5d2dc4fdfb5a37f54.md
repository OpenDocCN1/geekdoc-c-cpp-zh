
And we’ll also write ap without the do:

```
ap :: ∀ a b m. Monad m => m (a -> b) -> m a -> m b
ap ff fx = ff >>= (\f -> fx >>= (\x -> pure $ f x))
```

① Redundant Parentheses have been added to segregate the Functions passed to m’s bind, i.e. >>=.

And we’re going to need pure from our Parser:

```
instance applicativeParser :: Applicative (Parser e) where
  pure x = Parser \s -> pure $ Tuple s x
```

We’ll start with ap and replace the bind implementation from Parser one step at a time to see the final computation.

This is going to be a daunting task. Not because it’s difficult, but because there’s so many symbols. So, go through this slowly:

```
p >>= f = Parser \s -> parse p s >>=
    (\(Tuple s1 x) -> parse (f x) s1)  -- infix `bind` for reference

pure v = Parser \s -> pure $ Tuple s v -- `pure` for reference
------------------------------------------------------------
ff >>= (\f -> fx >>= (\y -> pure $ f y)) ①

p1 >>= (\f -> p2 >>= (\y -> pure $ f y)) ②

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse ((\f -> p2 >>= (\y -> pure $ f y)) x) s1) ③

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse (p2 >>= (\y -> pure $ x y)) s1) ④

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse (Parser \s -> parse p2 s >>=
    (\(Tuple s2 z) -> parse ((\y -> pure $ x y) z) s2)) s1) ⑤

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse (Parser \s -> parse p2 s >>=
    (\(Tuple s2 z) -> parse (pure $ x z) s2)) s1) ⑥

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse p2 s1 >>=
    (\(Tuple s2 z) -> parse (pure $ x z) s2)) ⑦

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse p2 s1 >>=
    (\(Tuple s2 z) -> parse (Parser \s -> pure $ Tuple s $ x z) s2)) ⑧

Parser \s -> parse p1 s >>=
    (\(Tuple s1 x) -> parse p2 s1 >>=
    (\(Tuple s2 z) -> pure $ Tuple s2 $ x z)) ⑨
```

① ap’s implementation with x renamed to y to avoid name confusion.

② Renamed ff to p1 and fx to p2 since we’re working with Parsers.

③ Substituted the whole formula into bind where p1 is bound to p and (\f -> p2 >>= (\y -> pure $ f y)) is bound to f.

④ Applied x to (\f -> p2 >>= (\y -> pure $ f y)) binding it to f. Note that, in this case, x is actually a Function. Remember that we’re working with apply where the first Parameter is a Function in a Context.

## 19.6. Coding with Monadic Parsers

Let’s take some of the `Parsers` we wrote using the Applicative-style and rewrite them using the `do` syntax.

First, we’ll take a look at `twoChars`:

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = Tuple <$> char <*> char
```

`twoChars` parses 2 characters and returns them in a `Tuple`. Rename the old version to `twoCharsA` to denote it’s the Applicative version. Then recode it using `bind`, i.e. `>>=`, and call it `twoCharsB`.

Only advance once those steps have been completed.

We’ll start with the Type Signature, which is unchanged:

```
twoCharsB :: ∀ e. Parser e (Tuple Char Char) ❶
```

> ❶ Don’t forget to call it `twoCharsB`.

This Parser is Polymorphic in `e` meaning that it’ll work with any error Type.

Next, we’ll call the `Parser`, `char`, once and capture it’s return value:

```
twoCharsB :: ∀ e. Parser e (Tuple Char Char)
twoCharsB = char >>= \c1 -> ???
```

And we’ll need to do it again to get the second character:

```
twoCharsB :: ∀ e. Parser e (Tuple Char Char)
twoCharsB = char >>= \c1 -> char >>= \c2 -> ???
```

And now we can return the characters in the `Tuple`. We must be careful to place them in the same order as `twoCharsA`, i.e. the first character in the first position of the `Tuple`:

```
twoCharsB :: ∀ e. Parser e (Tuple Char Char)
twoCharsB = char >>= \c1 -> char >>= \c2 -> pure $ Tuple c1 c2 ❶
```

> ❶ Don’t forget to wrap the `Tuple` in a `Parser` since that’s the Type that we’re returning. We do this by using `pure`.

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

```
threeChars :: ∀ e. Parser e String
threeChars =
  (\c1 c2 c3 -> fromCharArray [c1, c2, c3]) <$> char <*> char <*> char
```

Rename this to threeCharsA and write it again but this time use the do syntax. Call this new Function threeChars. Don’t read on until you’ve finished.

So as usual, we start with the Type Signature, which doesn’t change:

```
threeChars :: ∀ e. Parser e String
```

Next, we’ll start the Function with do:

```
threeChars :: ∀ e. Parser e String
threeChars = do
  ???
```

Next, we’ll call char 3 times capturing the characters into Variables:

```
threeChars :: ∀ e. Parser e String
threeChars = do
  c1 <- char
  c2 <- char
  c3 <- char
  ???
```

Then we can just return the final String:

```
threeChars :: ∀ e. Parser e String
threeChars = do
  c1 <- char
  c2 <- char
  c3 <- char
  pure $ fromCharArray [c1, c2, c3]
```

① Don’t forget to use pure to wrap the final String in a Parser.

Here we’re coding in the Parser Monad. This is why we need to return a Parser. Remember, Parsers must be run using parse. All we’ve done here is build a complex composition of Parsers each of which contains their own parsing Function.

```
satisfy :: ∀ e. ParserError e => (Char -> Boolean) -> Parser e Char
satisfy pred = char >>= \c -> if pred c then pure c else Parser \s -> ???
```

The next problem to solve is what does the parsing Function return?

We know it must be an Either and we also know that it’s an error so we’ll need a Left:

```
satisfy :: ∀ e. ParserError e => (Char -> Boolean) -> Parser e Char
satisfy pred = char
    >>= \c -> if pred c then pure c else Parser \_ -> Left ??? ①
```

① It’s clear that we’re not going to use the String Parameter to the Parser function. It’s been renamed from s to _.

Now all we need is a good error Value. Let’s look at our existing errors to see if we already have one:

```
data PError
    = EOF
```

Well, that’s underwhelming. Okay, let’s add an error that makes sense for satisfy:

```
data PError
    = EOF
    | InvalidChar String ①
```

① This has a String to allow there to be a message for what was expected.

But this error is needed by our library Function, satisfy, and the library won’t know about our PError Type because that’s defined in our Application. Well, not really, since we’re working in a single file here for learning purposes, but we’ve made satisfy general by constraining the error Type to be ParserError. So it could be moved out into another module or into a library.

If we want to use InvalidChar from satisfy, we’ll have to add it to the ParserError Typeclass:

```
class ParserError e where
    eof :: e
    invalidChar :: String -> e
```

And now we’ll have to update the ParserError Instance for PError:

```
```haskell
instance parserErrorPError :: ParserError PError where
  eof = EOF
  invalidChar = InvalidChar
```
```

① This was added.

Now we can use it:

```
```haskell
satisfy
  :: ∀ e
  .  ParserError e
  => String
  -> (Char -> Boolean)
  -> Parser e Char
satisfy expected pred = char >>= \c ->
  if pred c then pure c else Parser \_ -> Left $ invalidChar expected
```
```

① Added `String` Parameter in case there’s an error. It’ll be what was expected, hence, the Variable name expected.

Okay, but this isn’t great. I had to construct a Parser on the fly just to return an error. Blech!

Write a Function called `fail`, that will return a Parser that always fails. Give it a try and then continue reading.

Here’s fail’s Type Signature:

```
```haskell
fail :: ∀ e a. ParserError e => e -> Parser e a
```
```

Once again, we need the Constraint because this Parser will fail. In fact, it ALWAYS fails.

If you got stumped writing the Type Signature, stop now and see if you can finish the Function. Then read on.

We write the right-hand side first:

```
```haskell
fail :: ∀ e a. ParserError e => e -> Parser e a
fail e = ???
```
```

Here e is the error.

Next, we’ll write the left-hand side:
