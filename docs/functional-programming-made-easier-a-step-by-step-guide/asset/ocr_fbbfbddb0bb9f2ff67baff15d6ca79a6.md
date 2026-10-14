```
(+) <$> Just 3 <*> Just 9      -- Just 12
flip (+) <$> Just 9 <*> Just 3      -- Just 12

(-) <$> Just 3 <*> Just 9      -- Just -6
flip (-) <$> Just 9 <*> Just 3      -- Just -6

(+) <$> Just 3 <*> Nothing      -- Nothing
flip (+) <$> Nothing <*> Just 3 -- Nothing

(+) <$> Nothing <*> Just 4      -- Nothing
flip (+) <$> Just 4 <*> Nothing -- Nothing
```

① Notice that <*> is Commutative even though (-) is not. This is because we flipped BOTH the Parameters and the Function.

But this test fails for Either:

```
(+) <$> Left "err1" <*> Left "err2"      -- Left "err1"
flip (+) <$> Left "err2" <*> Left "err1"      -- Left "err2"
```

And it fails for Array (or List) too:

```
(+) <$> [2,3] <*> [7, 13]      -- [9,15,10,16]
flip (+) <$> [7, 13] <*> [2,3]      -- [9,10,15,16]
```

# 16.13. Traversables

Let’s consider a common scenario that we will encounter from time to time. First, we have an Array of Ints that we want to map over with what is called an Effectful function, i.e. a function that does NOT produce a Pure Value, but a Value in a Context:

```
half :: Int -> Maybe Int

 half x = if even x then Just (x `div` 2) else Nothing

map half [2, 4, 6]      -- [Just 1, Just 2, Just 3]

map half [2, 3, 4]      -- [Just 1, Nothing, Just 2]
```

① A non-effectful version of half would simply return Int.

But we don’t want an Array of Maybes. We want the Ints but ONLY if we had no failures. Sound familiar?