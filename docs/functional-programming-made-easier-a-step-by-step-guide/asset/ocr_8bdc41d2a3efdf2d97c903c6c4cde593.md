```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred = go Nil where
  go nl Nil       = nl
  go nl (x : xs)  = if pred x then go (x : nl) xs else go nl xs
```
```

❶ Remember, we don’t have to pass `pred` to `go` since it’s in `go`’s scope.

❷ If `x` passes `pred`’s requirement, then we first add it to our new `List`, `nl` and then recurse with the remainder of the `List`, `xs`. Otherwise, we just continue with `xs`. Now that we’re `Cons`-ing first, our function is Tail Recursive.

But now we have a big problem. We’re adding the elements to our new list **backwards**. The first element goes onto the head of the list and then the next element goes onto the head and so forth. This will result in reversing our results compared to their original order.

How do we fix this?

Since we can only add to the head of a `List` **and** we want this version to be Tail Recursive, we only have one choice and that’s to reverse the list at the end.

We can do that with the `reverse` Function we wrote, but before we do, we should make sure that `reverse` is Tail Recursive otherwise there’s no point in writing `filter` Tail Recursive if `reverse` is going to overflow our Stack:

```
```purescript
reverse :: List ~> List
reverse Nil = Nil
reverse ol = go Nil ol where
  go rl Nil       = rl
  go rl (x : xs)  = go (x : rl) xs
```
```

❶ It recurses by calling `go` and nothing else. So this is Tail Recursive.

Now that we can see that `reverse` is Tail Recursive, we can add it to `filter`:

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred l = reverse $ go Nil l where
  go nl Nil       = nl
  go nl (x : xs)  = if pred x then go (x : nl) xs else go nl xs
```
```

❶ We are now reversing the results of `go`.

❷ Notice I had to put back the `l` Parameter that I removed when I was making this Point-free.

To make this version Point-free again, we need to use Function Composition, `<<<`, instead of Function Application, `$`.