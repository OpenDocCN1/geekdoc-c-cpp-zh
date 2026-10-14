```
newtype ReaderT r m a = ReaderT (r -> m a)
```

Can you see where I went wrong?

I returned an a not an m a. Let’s fix that. But how? We need to put the a into Context m. How do we do that?

We do that by using pure, which we can do since m is a Monad and all Monads are Applicatives:

```
instance monadAskReaderT :: MonadAsk r (ReaderT r m) where
  ask :: ReaderT r m r
  ask = ReaderT \r -> pure r
```

And now we can ETA-reduce \r -> pure r to simply pure:

```
instance monadAskReaderT :: MonadAsk r (ReaderT r m) where
  ask :: ReaderT r m r
  ask = ReaderT pure
```

That compiles. So, now on to MonadTell. Here’s its definition:

```
class Monad m <= MonadTell w m | m -> w where
  tell :: w -> m Unit
```

① Same Functional Dependency definition as we saw in MonadAsk. This is usually put in to help the compiler when there’s ambiguity doing Type Inference. Without this, we’d find ourselves having to be explicit about our Types when we use tell.

② tell takes a Monoid, w, and appends it to its internal log. Notice how it returns a Value of Type Unit. That’s because we’re calling tell for its Side-effect not to have it compute something.

Now ReaderT’s instance:

```
instance monadTellReaderT :: MonadTell w (ReaderT r m) where
```

And now the left-hand side of the implementation:

```
instance monadTellReaderT :: MonadTell w (ReaderT r m) where
  tell w = ???
```

On the right-hand side, we’ll start with our usual pattern: