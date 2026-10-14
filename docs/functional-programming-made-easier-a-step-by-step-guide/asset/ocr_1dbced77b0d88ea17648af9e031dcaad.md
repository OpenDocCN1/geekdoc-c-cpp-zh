```
newtype ExceptT e m a = ExceptT (m (Either e a)) ①
```

① In our Stack, as defined by AppM, m is WriterT w (StateT s Identity), which is passed its final Type Parameter, i.e. Either e a.

And then WriterT give StateT its a:

```
newtype WriterT w m a = WriterT (m (Tuple a w)) ①
```

① m here is State s Identity, which is passed Tuple a w as its final Type Parameter.

And finally, WriterT gives Identity its a:

```
newtype StateT s m a = StateT (s -> m (Tuple a s)) ①
```

① m here is Identity, which is passed Tuple a s as its final Type Parameter.

Now that we understand AppM’s definition, we can begin writing our Application:

```
type AppM e w s a = ExceptT e (WriterT w (StateT s Identity)) a

app :: AppM String String Int Unit
app = do
    pure unit
```

This is a good starting point. Now let’s add logging:

```
type AppM e w s a = ExceptT e (WriterT w (StateT s Identity)) a

app :: AppM String String Int Unit
app = do
    tell "Starting App..." ①
    pure unit
```

① Remember, there is no need to call lift here since we’re running in the ExceptT Monad and it has a MonadTell instance.

It would be nice to have line endings automatically added to the end of our log. Let’s write a Function called log that will do that for us: