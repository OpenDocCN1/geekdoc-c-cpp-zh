```
(add3 1) 2 :: Int -> Int
```

y gets bound to 2. Calling that resulting Function with one Parameter:

```
((add3 1) 2) 3 :: Int
```

z gets bound to 3. The Function is now *Fully Applied* and returns a value of 6, which is of Type Int.

# 2.5.1. Partial Application

Returning to our zeroPad Function:

```
zeroPad :: Int -> String -> String
zeroPad = padLeft '0' ① ②

padLeft :: Char -> Int -> String -> String
padLeft padCh size s = ... ③
```

① padLeft is given only 1 of the many Parameters it will need to produce a final result.

② We have partially applied padLeft.

③ We’re not concerned with padLeft’s implementation at the moment.

> *Partial Application* is when a Function is called with fewer than all of its Parameters.

When we think of Functions having multiple Parameters, then Partial Application makes sense. However, when we think of Curried Functions, there is no such thing as Partial Application since there’s only one Parameter.

The power of Partial Application may not be immediately apparent but consider a simple example: