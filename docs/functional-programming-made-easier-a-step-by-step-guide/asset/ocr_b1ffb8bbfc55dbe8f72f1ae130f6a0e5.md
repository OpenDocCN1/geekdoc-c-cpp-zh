![](bbox=[0.322, 0.061, 0.677, 0.302])

What we need a way to lift WriterT into StateT. We can imagine a Function that lifts any Monad, not just WriterT:

```
liftIntoStateT :: ∀ s m a. Monad m => m a -> StateT s m a ①
```

① This imaginary Function takes any Monad, m a, and lifts it into StateT.

And here’s a Function that lifts any Monad into ReaderT:

```
liftIntoReaderT :: ∀ r m a. Monad m => m a -> ReaderT r m a ①
```

① This imaginary Function takes any Monad, m a, and lifts it into ReaderT.

We should stop right here and make a Typeclass for this since we have the classic condition for a Typeclass, i.e. same Function for multiple Types.

We’ll call it MonadTrans to represent Monads that can transform other Monads:

```
class MonadTrans t where
  lift :: ∀ m a. Monad m => m a -> t m a
```

Here t is the Monad Transformer and m its underlying Monad. lift will take a Value, a, in a Context, m, and lift it into itself, t m a.

Now we just have to make instances for our Monad Transformers, which will actually just wrap the underlying Monads. This will effectively move them up one slot in our Monad Stack.

Here’s an example of lifting WriterT into StateT, i.e. one layer up in the following Stack: