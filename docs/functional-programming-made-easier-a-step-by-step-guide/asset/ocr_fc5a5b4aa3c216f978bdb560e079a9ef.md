Now we’ll write a Function to run the returned Stack:

```
runStateLayer
  :: ∀ s w a
    . StateT s (WriterT w Identity) a
  -> WriterT w Identity a ①
runStateLayer nested = runStateT nested { count: 0 } ②
```

① Returns a Stack with WriterT on the top.

② We pass some Initial State, i.e. { count: 0 }.

And finally, we’ll write a Function to run that returned Stack:

```
runWriterLayer
  :: ∀ w a
    . WriterT w Identity a
  -> Identity a
runWriterLayer nested = runWriterT nested
```

And we can use unwrap from Data.Newtype to get our Pure Computation, since Identity has a Newtype Instance:

```
runIdentityLayer
  :: ∀ a
    . Identity a
  -> a
runIdentityLayer nested = unwrap nested
```

Notice how each Function, ran the topmost Layer of the Stack and returned all of the Layers below. We used that smaller Stack as the input to the next Function, which ran the topmost Layer and returned a smaller Stack and so on from Function to Function until we exhausted the Stack. Then all we had to do was unwrap to get our final result.

We did this with many Functions to show what’s happening at each step of the process, but it’s far better to write a single Function that runs the whole Stack: