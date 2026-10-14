Can you remember a Monad like that? If you can't remember, then can you remember a Function that does nothing?

identity has no effect on its input. We can think of it as a Function that does nothing and, in the same vein, the Identity Monad has no Side-effect and can also be thought of as a Monad that does nothing.

So, let's use Identity in place of our ???:

```
type Nested r s w a = ReaderT r (StateT s (WriterT w Identity)) a
```

Now our definition terminates.

And once we write these transformer versions of these Monads, we'll be able to easily recreate RWS. And, as it turns out, we can also create Reader from ReaderT by using our do-nothing Monad, Identity. Think of it as ReaderT combined with a do-nothing Monad:

```
type Reader r a = ReaderT r Identity a
```

And we can ETA-reduce this by canceling the a on both sides of the equal sign:

```
type Reader r = ReaderT r Identity
```

And we can do the same for Writer and State:

```
type Writer w = WriterT w Identity
type State s = StateT s Identity
```

Looks like we don't need the version of Reader, Writer and State that we wrote earlier. We just need these transformer versions.

Now what about that magical wrapping function? How do we take a StateT and wrap it into a ReaderT? Or, worse yet, how do we wrap a WriterT into a StateT and then wrap that into a ReaderT?

Let's look at our nested Monads as a Stack: