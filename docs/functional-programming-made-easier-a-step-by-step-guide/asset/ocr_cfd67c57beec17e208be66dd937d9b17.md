```
```haskell
pad :: Boolean -> Char -> Int -> String -> String
pad rightSide padCh size s = ...

padLeft :: Char -> Int -> String -> String
padLeft = pad false

padRight :: Char -> Int -> String -> String
padRight = pad true

zeroPad :: Int -> String -> String
zeroPad = padLeft '0'

spacePad :: Int -> String -> String
spacePad = padRight ' '

dotPad :: Int -> String -> String
dotPad = padRight '.'
```
```

If you look at `pad`, you’ll notice that the `size` Parameter comes before `s`, the `String` we want to pad. This is because we may want to write the following Function:

```
```haskell
dotPad20 :: String -> String
dotPad20 = dotPad 20
```
```

Now, we can pass a bunch of `Strings` to `dotPad20`. The `String` we want to pad is the thing that will change the most and, therefore, should be dead last in our Parameter List.

All of the other Parameters can be thought of as Configuration Parameters to tell `pad` how to pad whereas `s` is what to pad and since it will change the most, it’s the rightmost Parameter.

Sometimes you’ll have 2 Parameters that always change and, in that case, just make sure that they are last. Their respective order won’t matter.