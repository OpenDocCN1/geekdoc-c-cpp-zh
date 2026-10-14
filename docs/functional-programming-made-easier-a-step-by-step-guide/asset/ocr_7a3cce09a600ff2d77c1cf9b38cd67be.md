```
data NonEmpty collection element = NonEmpty element (collection element)
```

This would have been pretty verbose to look at, so it makes sense why single letters where used. But it’s not clear as to why f was used.

We’re used to seeing a, but why f and a instead of a and b, for example?

It turns out that all collections of elements, at least every collection I can think of, are also Functors. We haven’t learned about Functors yet, but clearly the author of this Type understands Functors and so used f to represent the Functor.

Here is our Type Signature for combineNEListOfSemigroups:

```
combineNEListOfSemigroups :: ∀ a. Semigroup a => NonEmpty List a -> a
```

Notice how we specified the f as List. That’s the collection or Functor Type. The second Type Parameter is a, which is the element Type.

Now let’s look at the Constructor for NonEmpty, which is also called NonEmpty:

```
data NonEmpty f a = NonEmpty a (f a) ①
```

① Constructor is on the right-hand side of the equals sign.

Notice how we MUST have a value of a AND a value of f a to construct a NonEmpty. That’s the magic ingredient in this Type. Without both parts, you cannot hope to construct a NonEmpty, which is why it can guarantee that the collection, or List in our case, is NOT empty. It’s constructor REQUIRES at least 1 element.

There is a helper function to convert NonEmpty to List:

```
newtype NonEmptyList a = NonEmptyList (NonEmpty List a) ①
toList :: NonEmptyList ~> List
```

① NonEmptyList is a newtype that has only one Type Parameter, the element Type.

Remember that ~> is the Natural Transformation from one Functor to another. (Functors are coming. I promise.) It’s shorthand for:

```
toList :: ∀ a. NonEmptyList a -> List a
```