
# 14.10. Homomorphisms

*Homo* means *same* and *morph* means *shape*. And a *Homomorphism* is a morphism that preserves shape or structure.

Functors are Homomorphisms since they preserve the Categorical Structure. But what does it mean to "preserve Categorical Structure"? The question really is what is meant by "Categorical Structure".

Recall that a Category has Objects and potentially zero or more Morphisms between those Objects.

Also, remember that every Object has at least one *Endomorphism* (*Endo* means *internal*) called the Identity Morphism.

And the other thing a Category has is Composition. This too must be preserved after mapping to the other Category.

So "Preserving Categorical Structure" means that the Functor must map all Objects and Morphisms to the new Category while maintaining the SAME Morphisms between those Objects.

For example, if there’s a Morphism between Objects a and b in the Source Category, the Functor must maintain that Morphism between their counterparts in the Target Category.

## 14.11. Natural Transformations

Natural Transformations are simply morphisms between Functors. They too are Homomorphisms.

The symbol, η is used to represent Natural Transformations since it sort of looks like an N, I guess. It’s actually the lowercase of H called Eta in the Greek alphabet.

Let’s use the following diagram to help us understand Natural Transformations:

![](img/8c0e9b687c62642e828ccb5481e11313_491_0.png)

Let’s look at this diagram on piece at a time.

On the left, we have Category C. The Morphism, f, maps from a to b.

On the right, we have Category D. Functor F maps a, b and f from Category C to Category D.

We also have Functor G, which maps the same.

Now, let’s add Morphisms between our Functors, F and G:

![](img/8c0e9b687c62642e828ccb5481e11313_492_0.png)

These Morphisms between Functors are Natural Transformations if and only if, the following is true:

- 1. The Morphism, η x : F x → G x exists in Category D for every Object, x, in Category C.
- 2. For every Morphism, f : a → b in Category C, η b ∘ F f = G f ∘ η a in Category D.

Notice how requirement #1 deals with the mapping of Objects from C to D and #2 deals with mapping of Morphisms. Not surprising since Functors map BOTH.

Another thing to note here is that the above diagram in Category D commutes.

> A Commutative Diagram is a diagram where all directed paths with the same start and endpoints lead to the same result.

It’s important to note that the above diagram is for Covariant Functors called Functors in PureScript.

If we wanted to represent Contravariant Functors, we would need to reverse all Vertical Arrows in our diagram. The Natural Transformation requirements for Contravariant are:

- 1. The Morphism, η x : F x → G x exists in Category D for every Object, x, in Category C. Same as Covariant
- 2. For every Morphism, f : b → a in Category C, η a ∘ F f = G f ∘ η b in Category D. a and b have swapped

Let’s look at a real-world example, a Homomorphism from Maybe to Either Unit:

```
hom :: Maybe ~> Either Unit
 hom Nothing = Left unit
 hom (Just x) = Right x
```

① ~> is the PureScript symbol for Natural Transformation.

We could’ve just as easily written the Type Signature as:

```
hom :: ∀ a. Maybe a -> Either Unit a
```

① Equivalent to η a : F a -> G a where Maybe is F and Either Unit is G.

We don’t have to prove that requirement #1 for Natural Transformation holds since our function compiles and our Type Signature is basically that requirement.

For requirement #2 for Covariant:

```
f : a -> b
hom ∘ (mMap f) = (eMap f) ∘ hom
```

① mMap is map from Maybe, i.e. Functor F.

② eMap is map from Either Unit, i.e. Functor G.

Starting on the left side of the 2nd equation, if we first use Maybe’s map mMap f and then transform to an Either hom, it’s the same as if we first transform to an Either hom and then map using Either’s map eMap f.

We can confidently reason that the equation holds true thanks to the Functor laws.

If you are still in doubt, check out the Functor implementations for Maybe and Either a where a is Unit for our example:

```
instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
  map f (Just x) = Just $ f x

instance functorEither :: Functor (Either a) where
  map _ (Left x) = Left x
  map f (Right y) = Right $ f y
```

Can you see the similarities?

If you’re still not convinced, simply do Algebraic Substitution. Here’s hom again:

```
```haskell
hom :: Maybe ~> Either Unit
hom Nothing  = Left unit ⑤
hom (Just x) = Right x ⑥
```
```

First, the Nothing case:

```
```text
(hom ∘ (mMap f)) Nothing = ((eMap f) ∘ hom) Nothing        — Given
hom Nothing = ((eMap f) ∘ hom) Nothing                       — Substitute into ❶
Left unit = ((eMap f) ∘ hom) Nothing                         — Apply on left side ⑤
Left unit = (eMap f) (Left unit)                              — Apply on right side ⑤
Left unit = Left unit                                         — Substitute into ❸
```
```

Now the Just x case:

```
```text
(hom ∘ (mMap f)) (Just x) = ((eMap f) ∘ hom) (Just x)       — Given
hom (Just $ f x) = ((eMap f) ∘ hom) (Just x)                — Substitute into ❷
Right $ f x = ((eMap f) ∘ hom) (Just x)                     — Apply on left side ⑥
Right $ f x = (eMap f) (Right x)                             — Apply on right side ⑥
Right $ f x = Right $ f x                                    — Substitute into ❹
```
```

## 14.12. Monoid Homomorphisms

Functions in Math map elements from their input Set called the Domain into their output Set called the Codomain:

![](img/8c0e9b687c62642e828ccb5481e11313_495_0.png)

And Monoids are Sets with Binary Operators and certain restrictions:

- 1. Binary Operator must be Closed over the Set. Magma
- 2. Binary Operator must be Associative. Semigroup
- 3. Set must have an Identity Element. Monoid

It’s possible to have a Function whose input Set Domain is from a Monoid, M. But there’s no guarantee that the output Set Codomain will also be a Monoid. It depends on the function.

Here we’re using the equivalent of the identity function:

```
idHom :: ∀ m. Monoid m => m -> m
idHom x = x
```

It should be obvious that this preserves the Monoidal Structure, i.e. this function had no effect on the input and therefore, it’s result is still a Monoid.

And here’s another example, which is just the equivalent of const mempty:

```
constHom :: ∀ m. Monoid m => m -> m
constHom _ = mempty
```

This too preserves the Monoidal Structure since it’s a Set that contains only mempty, which meets all the

requirements of a Monoid:

```
mempty <> mempty = mempty                 Closed      Magma
(mempty <> mempty) <> mempty = 
    mempty <> (mempty <> mempty)   Associative  Semigroup
mempty <> mempty = mempty                Identity     Monoid
```

We can also write a function that destroys that structure:

```
always123 :: String -> String
always123 _ = "123"
```

This function maps every String in our String Monoid to "123". The resulting Set, the Codomain, is NOT a Monoid. In fact, it’s not even a Magma:

```
"123" <> "123" = "123123"          NOT CLOSED
```

But so far, we’ve only seen contrived, simple examples. There is, however, a common function that we’ve all used many times that is a Monoid Homomorphism, length, the String length function. It maps Strings to Ints.

But before we verify that length is a Monoid Homomorphism, it might be good to give the formal definition for Monoid Homomorphism:

A function, h : M -> N, which maps elements from Monoid M to Monoid N, is a Homomorphism if:

```
h (m1 • m2) = h(m1) * h(m2)
```

In other words, first combining m1 and m2 in M and then mapping to N is equal to first mapping m1 and m2 to N and then combining in N.

Notice that combining in M uses M’s Binary Operator •, while combining in N uses N’s, *. These Binary Operators are different in the case of the length Homomorphism, but are the same when using idHom or constHom.

Here we can see that in action:
