```
```purescript
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findLastIndex _ Nil = Nothing
findLastIndex pred l = go Nothing 0 l where
  go :: ∀ a. Maybe Int -> Int -> List a -> Maybe Int
  go fi _ Nil = fi
  go fi i (x : xs) =
    go (if pred x then Just i else fi) (i + 1) xs -- COMPILER ERROR!!
```
```

① Here’s an **a**.

② And here’s another **a**.

If we look back on the error message, we can see that the compiler error occurred on the **x**. We can see this by the red underline under the **x**, but what gives?

The problem is that `pred` is defined in terms of the first **a** and **x** in terms of the second one.

When we say ∀ **a** in a local Function, we’re telling the compiler that the **a** is a new INDEPENDENT **a**. Sure we named it **a**, but it’s NOT the same **a** as in the main Function:

```
```purescript
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findLastIndex _ Nil = Nothing
findLastIndex pred l = go Nothing 0 l where
  go :: ∀ a. Maybe Int -> Int -> List a -> Maybe Int
  go fi _ Nil = fi
  go fi i (x : xs) =
    go (if pred x then Just i else fi) (i + 1) xs -- COMPILER ERROR!!
```
```

① Main Function’s **a**.

② INDEPENDENT **a**.

But we don’t want the **a**’s to be different from one another. So how do we fix this?

That’s easy. We just remove the ∀ **a** from `go`’s Type Signature:

```
```purescript
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findLastIndex _ Nil = Nothing
findLastIndex pred l = go Nothing 0 l where
  go :: Maybe Int -> Int -> List a -> Maybe Int
  go fi _ Nil = fi
  go fi i (x : xs) = go (if pred x then Just i else fi) (i + 1) xs
```
```

① The **a** in `List a` is now the same **a** as in `findLastIndex`’s Type Signature.