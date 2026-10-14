```
fgh :: ∀ a d. a -> Maybe d
fgh x = applyH h $ g $ f x
```

But what if we wanted g to also return a reason for the failure:

```
g :: ∀ b c. b -> Either String c
```

Now we have to write another function to apply h that works with Either String. Bells should be going off in your head at this point. This is going to be a problem for ALL Higher-kinded Types.

We would like to solve this problem in a more general fashion and, as it turns out, Category Theory gives us just the right solution, the Functor.

Here’s the definition of a Functor in PureScript:

```
class Functor f where ①
  map :: ∀ a b. (a -> b) -> f a -> f b ②

infixl 4 map as <$> ③
```

① When we used NonEmpty, it used f in its Type Signature. That stood for Functor and we use the same variable name here. This is common in PureScript and Haskell. Another use of f as a Type Parameter is for Foldable. But typically when you see f it represents a Functor.

② Notice how f is a Higher-kinded Type here since it takes a Single Type Parameter, which means it has the Kind Type -> Type.

③ Mapping over Functors is so common that there’s an Operator Alias for it. Notice how it mirrors the Function Application Operator, $. Also, realize our applyH is just the map Method for Maybe where f is Maybe.

The map Method allows us to Apply the function a -> b to the a within the Context of f and modify it WITHOUT changing the Context. This is an important point. When we examine the Functor Laws, we’ll see why this is true.

It’s unfortunate that the function is called map since this is an overloaded term, e.g. Maps are key/value stores and functions map from the Domain to the Codomain. So while the function is called map, many times we say map over, e.g. we want to map f over the List.

Let’s write the Functor instance for Maybe: