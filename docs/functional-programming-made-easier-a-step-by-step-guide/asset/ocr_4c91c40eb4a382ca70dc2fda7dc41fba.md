```
```haskell
instance altParser :: Alt (Parser e) where
  alt p1 p2 = Parser $\\s -> case parse p1 s of
    Left _ -> parse p2 s
    Right x -> Right x
```
```

In the success case, we just return the success value, which has a Type of `Either`.

Now, this code is forever concealed in this instance code and we can leverage it by using `<|>`.

Now, add `alphaNum` to your code:

```
```haskell
alphaNum :: ∀ e. ParserError e => Parser e Char
alphaNum = letter <|> digit
```
```

So, what will be the error if `alphaNum` fails to parse?

It’ll be `invalidChar "digit"`.

And what if we were to rearrange the order of `Parsers`?

```
```haskell
alphaNum :: ∀ e. ParserError e => Parser e Char
alphaNum = digit <|> letter
```
```

Now it’ll be `invalidChar "letter"`.

Neither of these are accurate. They just happen to be the last error. What we’d like the error to be is `invalidChar "alphaNum"`.

So, modify `alphaNum` to return `invalidChar "alphaNum"` as its error before reading on.

Here’s how we do that:

```
```haskell
alphaNum :: ∀ e. ParserError e => Parser e Char
alphaNum = letter <|> digit <|> fail (invalidChar "alphaNum")
```
```

We use a `Parser` which always fails, i.e. `fail`. By putting it last, it’ll be the error that this `Parser` returns if the previous 2 fail.

At this point, we should test our `Parsers`, but before we do, write a version of `count` that will return a `String`. Call it `count'`. It should delegate to `count`, which we wrote in an earlier Chapter.

Hint: Look at how you converted `Array Char` to `String` in your existing test code.