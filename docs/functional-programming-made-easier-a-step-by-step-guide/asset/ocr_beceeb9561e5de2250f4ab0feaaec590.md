+   - Morphisms compose
+   - There is an Identity Morphism for every Object, i.e. 1ₓ: x → x
+   - Composition is Associative: if f: a -> m b, g: b -> m c, and h: c -> m d then h ∘ (g ∘ f) = (h ∘ g) ∘ f

Notice the last law is slightly modified from what we saw for Hask earlier in the book. Now Functions return m b, m c and m d instead of b, c and d respectively. That’s because we’re going to be using Kleisli Composition.

As a point of reference, we should also look at the Semigroupoid and Category Instances for Function:

```
instance semigroupoidFn :: Semigroupoid (->) where
    compose f g x = f (g x)

instance categoryFn :: Category (->) where
    identity x = x
```

We’ve proven that Functions compose by implementing compose. We also have shown that an Identity Morphism exists by creating identity. And we know that Function Composition in Functional Programming is Associative, so we know that the Associativity Law is upheld.

And so, PureScript Functions along with the Types they operate on form a Category known as Hask.

Let’s do the same thing except for Kleisli.

To do this, we first need to model Kleisli Arrows. These are Morphisms in the Kleisli Category and are analogous to Functions.

To help us, we’ll model Arrows in Hask first:

```
newtype Function a b = Function (a -> b)
```

This definition models the fact that an Arrow from Object a to Object b in the Hask Category is represented by the Type Function a b. The Data Constructor takes a Function with the Type a -> b.

And now, we’ll do the analogous thing for Kleisli Arrows:

```
newtype Kleisli m a b = Kleisli (a -> m b)
```

This definition models the fact that a Kleisli Arrow from Object a to Object b in the Kleisli Category is represented by the Type Kleisli m a b. The Data Constructor takes a Function with the Type Signature a -> m b.