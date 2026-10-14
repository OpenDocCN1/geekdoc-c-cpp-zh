```
instance applyMaybe :: Apply Maybe where
  apply (Just f) x     = f <$> x
  apply Nothing _      = Nothing
```

We cannot apply a Function we don’t have, so we all we can do is return Nothing. This is in keeping with the Semantics of Maybe.

Next, we’ll write the Applicative Instance one line at a time:

```
instance applicativeMaybe :: Applicative Maybe where
```

We use Maybe here and not Maybe a for the same reasons we did for Apply.

And since Applicative only has a single Method, pure, we only need to write that. But before we do, let’s think about what pure should be.

Remember, that pure takes a Pure Value or a Pure Function (which technically is a Value) and wraps it in the Context. This is helpful when we want to use it with Functions that expect values in a particular Context, e.g. <*> expects this.

So we have to options for implementing pure. We could make pure return Nothing or Just x (where x is our Pure Value). If we were to pick Nothing, we would NEVER be able to use Pure Values with Contextual ones since we would annihilate the value. That’s a hugely undesirable limitation.

Also, if we use Nothing, we’d break the Identity Laws for Applicative, which if we think about, is in place so we don’t do something destructive like use Nothing.

So the only reasonable, law-abiding and useful option is to use Just:

```
instance applicativeMaybe :: Applicative Maybe where
  pure = Just ①
```

① Written in Point-free Notation.

Test your code to see if it prints out the expected results.

# 17.3. Writing Applicative Instance for Either

We’re going to write the Applicative Instance for Either in exactly the same way we did with Maybe except our test code is going to verify the Applicative Laws (which include the Apply Laws). So we’ll need to add the Eq instance to Either.

But instead of writing Eq and Functor, we’re going to derive it and let the compiler do some work for us.