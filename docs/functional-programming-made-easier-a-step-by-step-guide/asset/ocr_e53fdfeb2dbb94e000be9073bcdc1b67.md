```
instance monadEither :: Monad (Either a)
```

We technically should verify the Monad Laws, but since it’s implementation is analogous to Maybe and Either a is Isomorphic to Maybe, we’ll just assume it doesn’t break any laws. But, if we were so inclined to prove the laws, we could simply substitute Nothing with Left y and Just with Right in our proof we did for Maybe.

One final thing we can do here is compare apply to bind:

```
instance applyEither :: Apply (Either a) where
  apply (Left y) _ = Left y
  apply (Right f) x = f <$> x

instance bindEither :: Bind (Either a) where
  bind (Left y) _ = Left y
  bind (Right x) f = f x
```

Once again, we can see that these implementations are more alike than not. They both Short-circuit when Left is encountered. We could write apply in terms of bind by using ap:

```
instance applyEither :: Apply (Either a) where
  apply = ap
```

You may be wondering if doing this always works. Well, let’s think about it for a second.

Any apply implementation SHOULD have the same Semantics, i.e. behavior, as the bind implementation. If it does not, it will most likely break the Apply or Monad Laws. But even if it doesn’t, it would be a terribly designed Type if the Apply had different Semantics from Bind.

In the case of Maybe and Either, they Short-circuit. And both the Apply and Bind Instances should exhibit this behavior. With Maybe, we have no choice since Short-circuiting is intrinsic to the Data Structure. But with Either, we made an explicit decision to Short-circuit, therefore, we’d want our apply and bind implementations to both Short-circuit.

So, by all reasonable measures, ap SHOULD be able to do the work of Apply in all cases. While it is possible to create a Type that has inconsistent Semantics and, therefore, ap could not be used to produce this nefarious Type, I would advise strongly against ever doing so.

When we return to our Parser, we’ll see that its Apply Instance could easily be replaced with ap, that is after we write the Monad Instance.