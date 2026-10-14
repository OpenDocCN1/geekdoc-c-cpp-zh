In the Javascript case, our Value became a `NaN` which is Isomorphic to `Nothing`. The difference being that the PureScript compiler enforces the use of `Maybe`. And if we use best practices, `Maybe` will show up in our Type Signatures, which will inform us and others to the fact that our Function may fail.

So the Semantics of `Maybe` is something that can fail. In our example, `useAdd` cannot use `add` in the absence of one of the `Ints`.

There are many times were `Maybe` comes in handy:

+   - Search `String` for a `Char` or another `String`.
+   - Get a Value from `Map` (a Key/Value store) using a key.
+   - Get a Value from an `Array` at a particular index.

Each of these Functions have a single *obvious* failure, `Char` or `String` not found, key not found or index out of bounds.

But what if that’s not the case or our Function can fail for multiple reasons. How do we want return an explicit failure reason?

# Either

The `Either` Type is another failure Type, like `Maybe`, except it has the added benefit of having a reason for the failure:

```
data Either a b = Left a | Right b
```

Here Type `a` is used by the `Left` Data Constructor and Type `b` is used by the `Right` Data Constructor. To get a better sense of this, let’s look at an example:

```
data QueryError
  = DatabaseConnectionError String
  | InvalidQuery
  | NotFound

query :: Query -> Either QueryError Int
```

❶ `QueryError` models the different errors we can encounter.

❷ `DatabaseConnectionError` takes a `String` which contains more information about the connection failure.

❸ `query` takes a `Query` (not defined here) and either returns a `QueryError` or an `Int`.

So how would we create the different errors: