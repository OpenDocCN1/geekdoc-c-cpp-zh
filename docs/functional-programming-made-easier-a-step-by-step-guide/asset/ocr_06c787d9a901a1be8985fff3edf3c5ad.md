+   ⑤ The `List` instance where we leverage `List`’s `uncons` function. `a` is the element of our `List`.

+   ⑥ The `String` instance where we leverage `String`’s `uncons` function. `Char` is the element of our `String`.

`collection` and `element` are the Type Parameters to the `Decapitate` Typeclass. `collection` is the Type of collection and `element` is the Type of each element within that collection.

`decapitate` removes the head of the `collection` and returns it and the remaining elements in a `Record`. Since this can fail, it returns a `Maybe`.

The `List` instance is said to be **Polymorphic** in 2nd Type Parameter, i.e. Type `a`. Remember that **Poly** means **many** and **morph** means **shape**:

```
instance decapitateList :: Decapitate (List a) a where
  decapitate = List.uncons
```

The 2nd Type Parameter, `a`, can take on many shapes, i.e. `a` can unify with many Types.

In contrast, the `String` instance is **Monomorphic** in the 2nd Type Parameter, i.e. `Char`. Remember that **Mono** means **one** and **morph** means **shape**:

```
instance decapitateString :: Decapitate String Char where
  decapitate = String.uncons
```

The 2nd Parameter, `Char`, is a single, fixed Type.

# 6.13. Functional Dependency

Returning to our `String` instance for `Decapitate`:

```
import Data.String.CodeUnits as String

instance decapitateString :: Decapitate String Char where
  decapitate = String.uncons
```

This is the non-Unicode version of `String`. But what if we want to support Unicode also: