```
type FiberM a = ReaderT Config (StateT State Aff) a
```

From this, we can see that we need to run ReaderT first, since it’s on the top of our Stack:

```
import Control.Monad.Reader.Trans (ReaderT, runReaderT) ①

runFiberM :: FiberM Unit -> Aff ?x
runFiberM = ??? <<< flip runReaderT { bus } ②
```

① Added runReaderT to the import list.

② We pass a Config that contains our bus.

We’re passing a Bus into the runReaderT Function, but where are we getting this from?

The only place we can get this from is from whoever calls us. So let’s add it:

```
runFiberM :: BusRW String -> FiberM Unit -> Aff ?x ①
runFiberM bus = ??? <<< flip runReaderT { bus } ②
```

① Added BusRW String.

② Added bus Parameter.

We could’ve also passed Config instead of BusRW String. In this case, it’s six of one, half a dozen of the other since Config only has 1 field. But if it had multiple fields, then passing Config would’ve been a much better choice.

Realize that runReaderT returns it’s underlying Monad. We can see this from its Type Signature:

```
runReaderT :: ∀ r m a. ReaderT r m a -> r -> m a ①
```

① Removed the redundant Parentheses that are present in the Pursuit documentation.

Notice the return Type is m a. But what Type is m?

To figure that out we have to look at FiberM:

```
--          ReaderT   r       m       a
type FiberM a = ReaderT Config (StateT State Aff) a ①
```

① m is StateT State Aff.

So runReaderT’s return Type, i.e. m a, in our case will be StateT State Aff.