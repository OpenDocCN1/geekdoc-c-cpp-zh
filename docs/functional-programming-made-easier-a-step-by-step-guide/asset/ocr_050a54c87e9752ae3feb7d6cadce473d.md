![](bbox=[0.28, 0.06, 0.72, 0.28])

When we do this we get:

```
m (Tuple a w)          -- runWriterT
m (Tuple (Tuple a w) s)  -- runStateT
m (Either e (Tuple (Tuple a w) s))  -- runExceptT
```

After unwrapping:

```
Either e (Tuple (Tuple a w) s)
```

With this Stack, we also lose State, s, if an error occurs. In fact, with ExceptT at the bottom of our Transformer Stack, which is not including the base Monad, Identity, we lose everything when an error occurs.

# 20.5. Coding with Monad Transformers

Let’s write some code that operates within a Monad Stack.

To do so, we’re going to pick a Stack that has ExceptT at the top of the Stack so we don’t lose any information: