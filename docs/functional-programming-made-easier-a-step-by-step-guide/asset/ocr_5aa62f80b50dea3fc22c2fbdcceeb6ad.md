Look back at the bind implementation to see what we did before reading on.

Did you notice that we just called runStateT?

Since it worked there to give us a Monadic Value in the underlying Monad, it'll work here:

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
    catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
    catchError (StateT fmx) f = StateT \s ->
        catchError (fmx s) \e -> runStateT (f e) ???
```

Now here's the kicker. runStateT wants a State for its second Parameter, but where can we get a State from?

The only State we have is the SAME one we passed to fmx. So that's the only one we can use. And so we will:

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
    catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
    catchError (StateT fmx) f = StateT \s ->
        catchError (fmx s) \e -> runStateT (f e) s
```

Go ahead and make sure to add this to your code before reading on.

Notice that we passed the SAME State to fmx and to f. This is very different than what we did everywhere else when dealing with State in multiple places in a Function.

Typically, we captured the MODIFIED State from the first Function that uses State and passed that modified version to the next Function that needs a State.

We cannot do that here and so the best we can do is use the SAME State. That means that any changes that fmx makes to the State will be lost if fmx calls throwError.

We'll look at this issue in more detail later.

# 21.4. Testing our StateT Implementation

We'll want to test out our newly minted Monad Transformer to see if it behaves correctly. To do this, we're going to steal the ideas and some of the code we saw in the previous Chapter.

Let's start with the Application Stack definition: