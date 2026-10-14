```
asks :: ∀ r. (r -> a) -> Reader r a

```

asks takes a Function that will take the full read-only Value, r, and return some or all of it, a.

And now the right-hand side of the equal sign:

```
asks :: ∀ r. (r -> a) -> Reader r a
asks f = ???
```

Next, let’s add our common pattern, since we’re returning a Reader:

```
asks :: ∀ r. (r -> a) -> Reader r a
asks f = Reader \\r -> ???
```

Now the only thing that we can do is apply f to r:

```
asks :: ∀ r. (r -> a) -> Reader r a
asks f = Reader \\r -> f r
```

And that concludes the API:

```
ask :: ∀ r. Reader r r
ask = Reader identity

asks :: ∀ r. (r -> a) -> Reader r a
asks f = Reader \\r -> f r
```

Here’s a diagram that illustrates how ask bridges the gap between the Pure Computation and the Monadic one: