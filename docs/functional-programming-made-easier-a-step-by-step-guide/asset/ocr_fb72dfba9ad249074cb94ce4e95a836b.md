❹ We using `const` to discard the `unit` returned from `pure unit`.

But wait. Look at `const Nothing <$> pure unit`. Can you see how we can reduce this?

Since `const Nothing <$> pure unit` applies `const Nothing` to the `unit` in the `Applicative`, we can just do `pure Nothing`:

```
```haskell
accountParser :: AccountParserT (Array Account)
accountParser =
  -- COMPILER ERROR!!
  (Just <$> accountParser <|> pure Nothing)
    `sepBy` char '\n' <#> fromFoldable
```
```

❶ Use `pure Nothing`, which is a `AccountParserT (Maybe a)`.

We expected the compiler error since now we have an `AccountParserT (Array (Maybe Account))`. We need to get rid of the `Maybes` in our `Array` while throwing away the `Nothings`.

Do you remember a Function that does that?

Go search `Pursuit` for `Array (Maybe a) -> Array a`.

Here’s why I found:

```
```haskell
catMaybes :: ∀ a. Array (Maybe a) -> Array a
```
```

This is exactly what we need. Go ahead add this to your code then keep reading.

Here’s that final change:

```
```haskell
import Data.Array (many, some, (:<), fromFoldable, catMaybes)

accountParser :: AccountParserT (Array Account)
accountParser =
  (Just <$> accountParser <|> pure Nothing)
    `sepBy` char '\n' <#> catMaybes <<< fromFoldable
```
```

❶ Added `catMaybes` to the import list.

❷ `catMaybes` AFTER we’ve converted the `List` to an `Array`. Thanks to the Functor Laws, we can save a call to map by composing.

Now, run your server and see what happens.

If your code is like mine, then your server should be running.