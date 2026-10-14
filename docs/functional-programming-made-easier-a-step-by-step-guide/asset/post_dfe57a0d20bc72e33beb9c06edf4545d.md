
hasty mistake:

```
instance applyReaderT :: Apply m => Apply (ReaderT r m) where
  apply (ReaderT fmf) (ReaderT fmx) = ReaderT \r -> fmf r <*> fmx r
```

Of course, we can always cheat with ap, but for learning, coding it by hand is far better.

And now, we can embark on the Applicative Instance:

```
instance applicativeReaderT
  :: Apply m => Applicative (ReaderT r m) where ①
```

① Proactively adding Apply Constraint since our Superclass has that Constraint. But, this time, I’ll keep in mind that this Constraint may change based on our code.

Now we can code the left-hand side:

```
instance applicativeReaderT
  :: Apply m => Applicative (ReaderT r m) where
  pure x = ???
```

And now our pattern:

```
instance applicativeReaderT
  :: Apply m => Applicative (ReaderT r m) where
  pure x = ReaderT \r -> ???
```

And now we need to think a little harder. We need to return an m a where m is the underlying Monad. And all Monads are also Applicatives. So why not do what we’ve done before and pass the buck to the underlying Monad?

Since it’s worked for us before, let’s try it, but this time remembering to adjust the Constraint on m:

```
instance applicativeReaderT
  :: Applicative m => Applicative (ReaderT r m) where ①
  pure x = ReaderT \r -> pure x ②
```

① Changed the Constraint on m from Apply to Applicative, since we’re using the underlying Monad’s pure implementation.

② Delegating to the underlying Monad’s pure.

via a do block. So let’s start there even though it may prove to be a dead end or overkill. We’ll find out soon enough either way:

```
instance bindReaderT :: Apply m => Bind (ReaderT r m) where
  bind (ReaderT fmx) f = ReaderT \r -> do
    ???
```

And if history is any help here, we can expect to use runReaderT at some point. If you remember, we needed runWriterT in WriterT’s implementation of bind.

We also have learned that fmx is a Function that needs to be called with r. This means that fmx r will give us a Monadic Value, which we can extract with >>= or <- since we’re using do notation.

Let’s do that first:

```
instance bindReaderT :: Apply m => Bind (ReaderT r m) where
  bind (ReaderT fmx) f = ReaderT \r -> do
    x <- fmx r ①
    ???
```

What Type is x here?

If you’re having trouble figuring that out, here’s the definition of ReaderT to help:

```
newtype ReaderT r m a = ReaderT (r -> m a)
```

fmx is the contained Function and we’ve passed an r to it. That means that x is of Type a, which is the exactly the Type that bind’s Function, f, wants.

This means that we can just apply f to x, which will give us a ReaderT that we’ll use runReaderT on, so that we can get a Value in the underlying Monad.

And at that point, we’ll be done. So there’ no need to extract and rewrap the Value. We can just end with the runReaderT call:

```
instance bindReaderT :: Apply m => Bind (ReaderT r m) where
  bind (ReaderT fmx) f = ReaderT \r -> do
    x <- fmx r -- COMPILER ERROR!
    runReaderT (f x) r
```

Oh, no. Can you guess what I forgot to do? Don’t look at the following compiler error just yet and see if you can see it.

It’s a good thing we have the compiler to keep us honest. Here’s the error:

![](img/8c0e9b687c62642e828ccb5481e11313_923_0.png)

I used bind for the underlying Monad, m, but forgot to constrain it to Bind. It’s only constrained to be an Apply. Even though I tried to remember, I still forgot.

So, let’s change the Constraint to Bind:

```
instance bindReaderT :: Bind m => Bind (ReaderT r m) where
  bind (ReaderT fmx) f = ReaderT \r -> do
    x <- fmx r
    runReaderT (f x) r
```

And the compiler is content. But looking closely at the do block reveals that it’s only 2 lines long. This means we could’ve written it more tersely using >>=.

Let’s do that:

```
instance bindReaderT :: Apply m => Bind (ReaderT r m) where
  bind (ReaderT fmx) f = ReaderT \r -> fmx r >>= \x -> runReaderT (f x) r
```

Take a second to see how these 2 forms are equivalent.

I like the >>= version better, but you may like the do syntax better. This is an aesthetic choice.

And now it’s time for the easiest instance:

```
instance monadReaderT :: Monad m => Monad (ReaderT r m)
```

One important thing to notice is that we’ve been thinking of m as the underlying Monad. But we’ve never needed to constrain m to be a Monad until now.

That’s because a Monad is both a Bind and an Applicative, and in our Applicative, we constrained m to be an Applicative and in our Bind, we constrained m to be a Bind. The combinational effect of both of those Constraints is a Monad Constraint.

## 20.9. Making ReaderT Easier to Use

Our ReaderT is a Monad Transformer but it’s not easy to use. We don’t have a way to lift another Monad into the ReaderT and we haven’t made any instances for the common Monad APIs.

In this section, we’ll do that. First, we’ll write lift one line at a time. But, don’t forget, lift is a Typeclass Method from MonadTrans. So, we’ll need to make an instance of MonadTrans, which has only one Method, lift:

```
class MonadTrans t where
  lift :: ∀ m a. Monad m => m a -> t m a
```

Let’s start one line at a time:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where ① ②
```

① We hold all Type Parameters, except the rightmost, constant.

② Notice that t in the Typeclass definition is ReaderT r. That’s because t takes 2 Type Parameters, m and a. ReaderT r is missing 2 of its Type Parameters, m and a.

Next, we’ll write the left-hand side of the equal sign:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ??? ①
```

① The name mx reminds us that we’re dealing with a Monadic Value, i.e. a Value in a Context, but not just any Context. This is a Value in ReaderT’s underlying Monad’s Context.

Now, we’ll start with our pattern on the right-hand side:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT \r -> ???
```

Now, we have to stop and think about what ReaderT’s Function returns. Let’s look back at the ReaderT

definition:

```
newtype ReaderT r m a = ReaderT (r -> m a)
```

From this, we can see that it has to return a Value of Type `a` in a Context, `m`. We have exactly that in `mx`, so we can just return that:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT \\r -> mx
```

Now, since we’re not using `r`, we can eliminate it:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT \\_ -> mx
```

And now we can replace `\\_ -> mx` with `const mx`:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT $ const mx
```

And now we can compose the Data Constructor, `ReaderT`, with `const`:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = (ReaderT <<< const) mx
```

And finally, ETA-reduce, i.e. cancel `mx` on the right-hand side on both sides of the equal sign:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift = ReaderT <<< const
```

And we’re done.

But wait. The right-hand side of the equal sign seems awfully familiar. Didn’t we have something like that when we wrote `pure`?

Let’s look at `pure`:

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
