coercing the Aff Unit to ParAff Unit.

Then sequential actually runs the computation in its own Fiber. Not much of a computation here, but realize that sequential is doing some magic Fiber stuff under the covers.

Now, let’s imagine we’re doing 2 Ajax calls to different APIs. We can do them in serial, i.e. make one API call and then when that finishes, we can make the second.

Or we can do them in parallel:

```
import Affjax as Ajax
import Control.Parallel (parallel, sequential) ①

type Response = Either Ajax.Error (Ajax.Response String)

twoRequests :: Aff (Tuple Response Response)
twoRequests =
  sequential $
    Tuple <$> parallel (Ajax.get string "https://foo.com")
        <*> parallel (Ajax.get string "https://bar.com")
```

① Import parallel and sequential.

The 2 different parallel calls will run in their own Fibers and their results will be combined via map and apply to Tuple. But this won’t happen until sequential is called.

What if we want to make an Ajax call with a timeout. What we need is a way to race 2 parallel computations and pick the winner, i.e. the one that finishes first.

Let’s revisit the ParAff docs: