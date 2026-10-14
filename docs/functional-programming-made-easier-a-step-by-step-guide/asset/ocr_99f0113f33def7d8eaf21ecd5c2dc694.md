# oneOf

```
oneOf :: forall f g a. Foldable f => Plus g => f (g a) -> g a
```

Combines a collection of elements using the Alt operation.

purescript-foldable-traversable Data.Foldable

oneOf will add the <|> between each element of the Foldable:

```
requestWithTimeout :: Number -> Aff (Maybe Response)
requestWithTimeout timeout =
  sequential $ oneOf
    [ parallel (Just <$> Ajax.get string "https://foo.com")
    , parallel (Nothing <$ delay (Milliseconds timeout))
    ]
```

1 Array is our Foldable.

This code is equivalent to the earlier version that explicitly used <|>.

We can make this Function a bit cleaner by factoring out the parallel:

```
requestWithTimeout :: Number -> Aff (Maybe Response)
requestWithTimeout timeout =
  sequential $ oneOf $ parallel <$>
    [ (Just <$> Ajax.get string "https://foo.com")
    , (Nothing <$ delay (Milliseconds timeout))
    ]
```

1 Factored out parallel and map it over the Array.

To make many calls in parallel and keep the results of all of them, we can write code in an Applicative style like: