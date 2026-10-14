```
instance bindRWS :: Bind (RWS r w s) where
  bind (RWS g) f = ???
```

We destructrue the RWS to get to its Function.

And now we’ll start on the right-hand side with our pattern:

```
instance bindRWS :: Bind (RWS r w s) where
  bind (RWS g) f = RWS \rws -> ???
```

We cannot use f at this point since it wants an a and we have nothing of that Type, at least not yet. We can get an a if we pass rws to g, but it’ll be buried in a Tuple:

```
instance bindRWS :: Bind (RWS r w s) where
  bind (RWS g) f = RWS \rws -> g rws # \(Tuple x rws') -> ??? ①
```

① We are destructuring the result of g rws to get the Value, x, which is of Type a.

Now that we have a Value of Type a, i.e. x, we can call f with it:

```
instance bindRWS :: Bind (RWS r w s) where
  bind (RWS g) f = RWS \rws -> g rws # \(Tuple x rws') -> f x ???
```

Are we done? Please try to answer that question. How did you determine your answer?

The way to know if we’re done is by knowing the Type of f x. We know, from the Data Constructor, that this Function must return Tuple a (RWSResult r w s):

```
newtype RWS r w s a = RWS (RWSResult r w s -> Tuple a (RWSResult r w s))
```

And now we have to ask ourselves what Type is f x? We know x’s Type is a, but what’s f’s Type?

Let’s look at bind’s Type Signature to see:

```
bind :: ∀ a b. m a -> (a -> m b) -> m b
```

And now, we can specialize that for RWS by replacing m with RWS r w s. Notice that we’re using RWS r w s and NOT just RWS. That’s because RWS r w s was what we specified when we defined the Bind Instance: