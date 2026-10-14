This tells us that the next thing we need to do is to run StateT:

```
import Control.Monad.State.Trans (StateT, runStateT)

runFiberM :: BusRW String -> FiberM Unit -> Aff ?x -- COMPILER WARNING!!
runFiberM bus = flip runStateT { count: 10 }
    <<< flip runReaderT { bus }
```

① Added runStateT to the import list.

② Pass in our read-write State. We could also pass this in to the Function, but for now, we’re just going to hardcode it here.

Now we have the following warning:

![](bbox=[0.146, 0.345, 0.854, 0.58])

So, we can now just copy and paste our Type Hole, changing `{ count Int }` to State:

```
import Data.Tuple (Tuple)

runFiberM :: BusRW String -> FiberM Unit -> Aff (Tuple Unit State)
runFiberM bus = flip runStateT { count: 10 } <<< flip runReaderT { bus }
```

① Import Tuple.

② The Type Alias, State, is used here instead of the Type { count :: Int } from the compiler warning.

And another Technological Hurdle falls.

# 23.2.5. Making a Bus

We’ve made a Bus in the previous Chapter, but let’s assume for a moment that you’re coding and you don’t have this book handy and you want to figure out how to create a Bus.