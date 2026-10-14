```
type State = { count :: Int }
```

Now, make a Type Alias called `FiberM`, since this represents the Monad Stack that our Fibers will run in. Put `ReaderT` on the top of the Stack and `Aff` on the bottom of the Stack.

Do this before reading ahead.

Let’s start slowly:

```
import Control.Monad.Reader.Trans (ReaderT)
import Control.Monad.State.Trans (StateT)

type FiberM a = ReaderT r? m? a
```

❶ Import `ReaderT` and `StateT`.

❷ The `r?` and `m?` are placeholders until we figure out what Monomorphic Types to put here.

We need to replace `r?` with `Config`:

```
type FiberM a = ReaderT Config m? a
```

Next, we should replace `ReaderT`’s underlying `Monad, m?`, with `StateT`:

```
type FiberM a = ReaderT Config (StateT s? m?) a
```

❶ The `s?` and `m?` are placeholders until we figure out what Monomorphic Types to put here.

Now we need to replace `s?` with `State`:

```
type FiberM a = ReaderT Config (StateT State m?) a
```

And last, we replace `StateT`’s underlying `Monad, m?`, with `Aff` since it’s at the base of the Stack:

```
type FiberM a = ReaderT Config (StateT State Aff) a
```

When you see a nested Type that represents a Monad Stack, realize that the outer most or leftmost Monad, in this case `ReaderT`, is on top of the Stack. The next Monad, going from left to right is the next highest in the Stack and so on. In our case, the second from the top of the Stack is `StateT`. And finally, we have the base of the Stack containing `Aff`.