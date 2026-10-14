
answered by looking at an example.

First in Javascript:

```
const x = 10;
const y; ①
const add = (x, y) => x + y -- z = NaN ②
```

① We did not initialize y.

② Here we try to use y in a computation and wind up with NaN. Now any computation that uses z will be NaN.

Now in PureScript:

```
add :: Int -> Int -> Int
add x y = x + y

useAdd :: Int
useAdd =
  let x :: Int
      x = 10

      y :: Maybe Int
      y = Nothing ①
  in
  add x y -- COMPILER ERROR!! ②
```

① We have no value for y and it's EXPLICITLY defined to be a Maybe Int.

② The compiler complains because we tried to add an Int with a Maybe Int.

The compiler save us from using an incompatible Type. So how do we fix this?

We could try to make the Types compatible:

```
```purescript
add :: Int -> Int -> Int
add x y = x + y

useAdd :: Int
useAdd =
  let x :: Int
      x = 10

      y :: Int
      y = Nothing  -- COMPILER ERROR!!
  in
  add x y
```
```

① If we try to make `y` an `Int` but set it to `Nothing`, the compiler will complain since our types don’t match (`Int ≠ Maybe Int`).

② The compiler doesn’t complain here because we defined `y` to be of Type `Int` which is fine for adding to another `Int`.

Once again the Type system saves us from assigning a `Maybe Int` to an `Int`. But how do we fix this now?

We could just initialize `y` to some Value:

```
```purescript
add :: Int -> Int -> Int
add x y = x + y

useAdd :: Int
useAdd =
  let x :: Int
      x = 10

      y :: Int
      y = 42
  in
  add x y
```
```

Now everything works. But this example is too simplistic. What would happen if `useAdd` got passed `y`:

In the Javascript case, our Value became a `NaN` which is Isomorphic to `Nothing`. The difference being that the PureScript compiler enforces the use of `Maybe`. And if we use best practices, `Maybe` will show up in our Type Signatures, which will inform us and others to the fact that our Function may fail.

So the Semantics of `Maybe` is something that can fail. In our example, `useAdd` cannot use `add` in the absence of one of the `Ints`.

There are many times were `Maybe` comes in handy:

- Search `String` for a `Char` or another `String`.
- Get a Value from `Map` (a Key/Value store) using a key.
- Get a Value from an `Array` at a particular index.

Each of these Functions have a single *obvious* failure, `Char` or `String` not found, key not found or index out of bounds.

But what if that’s not the case or our Function can fail for multiple reasons. How do we want return an explicit failure reason?

## Either

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

You can think of Left and Right as Tagging the Int so that we can tell whether it represents an error or a success. This is why Sum Types are also known as Tagged Unions.

## Maybe vs Either

Maybe and Either can both represent error results, but only Either gives us a reason. Maybe, on the other hand, can represent an optional Value.

Just for fun, let’s look at the inhabitants of both:

```
data Maybe a = Just a | Nothing

data Either a b = Left a | Right b
```

Remember that Maybe is a Sum Type, so we need to add the inhabitants of all of the Data Constructors. The inhabitants of Maybe is a for Just a and 1 for Nothing, therefore the number of inhabitants is a + 1.

And for Either, which is also a Sum Type, we have a for Left and b for Right or a + b inhabitants.

```
Maybe:    a + 1
Either:    a + b
```

That was a mildly interesting exercise, but there’s actually something more interesting if we try to make Maybe and Either have the same inhabitants, which would make them Isomorphic.

There’s 2 ways we can do that.

First, we choose a Type for b such that it has only 1 inhabitant:

```
Maybe:    a + 1
Either:    a + 1        (b = 1)
```

One thing to note here is that an a in the Maybe Type is independent of an a in the Either Type. So, an easy way to make them have the same number of inhabitants, is to simply choose the same Type for both a’s. We also could’ve picked 2 different Types with equal Inhabitants.

Let’s choose Boolean for both a’s and Unit for b (we need b to have 1 inhabitant):

```
Maybe Boolean ≅ Either Boolean Unit ①
```

① The symbol ≅ stands for is Isomorphic to.

Notic that our Either has an error Value but no success Value. While they’re technically Isomorphic,

Either Boolean Unit doesn’t make sense with the Semantics of Maybe Boolean. That’s because the Boolean in Maybe is the success Type, whereas the Boolean in Either is the error Type.

The second way to make them Isomorphic is to swap the Either types:

```
Maybe Boolean ≅ Either Unit Boolean
```

Now our Either has a success Value but no error Value, which is exactly like Maybe. It too only has a success Value. Semantically, this Isomorphism makes sense. Boolean in both types is the success Type.

So we have 3 inhabitants for each of the following:

```
Maybe Boolean ≅ Either Boolean Unit ≅ Either Unit Boolean
```

Let’s list them:

```
Maybe Boolean
_____________
Just true
Just false
Nothing

Either Boolean Unit
____________________
Left true
Left false
Right unit

Either Unit Boolean
____________________
Left unit
Right true
Right false
```

While this was slightly more interesting, you may be wondering what this has to do with using these Types. In turns out that there are times we want to convert between Maybe and Either and when they’re Isomorphic we can easily do this:

```
to :: Maybe Boolean -> Either Unit Boolean
to (Just b) = Right b
to Nothing  = Left unit

from :: Either Unit Boolean -> Maybe Boolean
from (Right b) = Just b
from (Left _)  = Nothing ①
```

① We can use _ to represent a Variable that we don’t care about naming. This is common pattern when working with unit.

But, let’s be real, we’re never going to have an Either where one of the Type Parameters is of Type Unit. We’re just going to use a Maybe.

So how do we convert between them when they’re not Isomorphic?

Looking at to and from above gives us some clues.

When we went from Maybe to Either, we had to make up data for the Nothing case. We did that by using unit. When we went from Either to Maybe, we threw out data for the Nothing case. We threw out the unit.

If we want to convert between any Maybe and Either, we’ll need to do something similar:

```
hush :: Either a b -> Maybe b
```

Notice there is no a in the Maybe result. That’s should tell us that hush "throws away" the error Type on the left side of the Either.

Let’s look at the rest of the Function:

```
hush :: ∀ a b. Either a b -> Maybe b ①
hush (Left _)  = Nothing ② ④
hush (Right x) = Just x ③ ④
```

① When defining Polymorphic Type Parameters for Functions, you must explicitly define them using the keyword forall or you can optionally use the symbol, ∀. I use the symbol because it’s easier to read.

② _ is used since we aren’t going to use the a from Left.

③ We destructure the Right to get to the x, which is of Type b, and then we construct a Maybe using Just.

④ In PureScript, we can write different versions of Functions. The compiler matches the Parameters passed in to determine which version to call. Unlike languages that support overloading, they MUST have the same Type Signatures.
