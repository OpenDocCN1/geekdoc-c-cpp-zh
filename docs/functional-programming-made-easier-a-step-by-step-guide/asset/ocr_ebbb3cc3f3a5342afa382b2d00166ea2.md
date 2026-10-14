the start is greater than the end or not.

This can be done with an inline if expression to help reduce your code complexity.

# 5.32.2. Code for range

We start as always with the Type Signature:

```
range :: Int -> Int -> List Int
```

Next, the base-case:

```
range :: Int -> Int -> List Int
range start end  | start == end  = singleton start ①
                 | otherwise     = ??? ②
```

① Create a List with start as the one and only element.

② This is where the recursive case will go.

Notice that we’re using Guards and that’s because Pattern Matching doesn’t handle Boolean logic.

The recursive case is:

```
range :: Int -> Int -> List Int
range start end
  | start == end = singleton start
  | otherwise    =
      start : range (start + (if start < end then 1 else (-1))) end ① ②
```

① Place start at the head and recurse with a incremented/decremented start. If start is less than end then we are incrementing else decrementing.

② Make sure to import (<) and otherwise from Prelude.

# 5.33. Optimizing range

You might have written range as follows: