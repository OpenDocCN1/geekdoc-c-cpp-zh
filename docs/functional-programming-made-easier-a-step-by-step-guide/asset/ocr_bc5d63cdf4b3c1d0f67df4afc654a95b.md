will always be picked removing any ambiguity.

But now `decapitateArray` will NEVER be picked because `List` will always match:

```
ta :: Maybe (Array String) -- COMPILER ERROR!! ①
ta = genericTail ["abc"]

tl :: Maybe (List String)
tl = genericTail ("abc" : Nil)
```

① Could not match type `List` with type `Array`.

On the surface, it may appear that Functional Dependencies don’t work well and require a lot of work. But in practice, they are usually the easiest and best solution.

The example with non-Unicode and Unicode `Strings` both needing to be an instance of the same Class is pretty rare and quite contrived to demonstrate some problems you’ll run into and some possible solutions.

And in the rare case where Functional Dependencies fail us due to crazy requirements, we can always use `Proxy` to force the compiler to pick the instance we want.