```
instance applicativeReaderT
  :: Applicative m => Applicative (ReaderT r m) where
  pure = ReaderT <<< const <<< pure
```

Looks like we can replace ReaderT <<< const with lift:

```
instance applicativeReaderT
  :: Applicative m => Applicative (ReaderT r m) where
  pure = lift <<< pure
```

This makes sense. To create a ReaderT from a Pure Value, we first create the underlying Monad, m, from that Pure Value and then just lift that.

Next, we’re going to write the MonadAsk Instance. Here’s its definition:

```
class Monad m <= MonadAsk r m | m -> r where
  ask :: m r
```

① The | m -> r is the Functional Dependency that states if we know the Monad, m, we can determine the read-only Value, r since there can be ONE AND ONLY ONE r for this m. This helps remove potential ambiguities.

② ask returns the read-only Value in the Context of this Monad. In our case, m is going to be ReaderT r m.

Let’s start with ReaderT’s Instance one step at a time:

```
instance monadAskReaderT :: MonadAsk r (ReaderT r m) where
```

Next, we’ll write the specialized Type Signature for ask, to help us see how to write the code:

```
instance monadAskReaderT :: MonadAsk r (ReaderT r m) where
  ask :: (ReaderT r m) r
```

① The redundant Parentheses is there to help us see how m, in the Typeclass definition, is replaced by ReaderT r m.

Next, we’ll write the left-hand side: