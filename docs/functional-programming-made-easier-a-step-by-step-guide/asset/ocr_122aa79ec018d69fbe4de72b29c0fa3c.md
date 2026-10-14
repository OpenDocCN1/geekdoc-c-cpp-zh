Do just this much for now and then return here once you’re done.

First, we’re going to make a `router` stub starting with the Type Signature:

```
router :: Request -> ResponseM
```

This takes a `Request` and then runs in or, more accurately, returns the `Response` Monad.

Next, we’ll just ignore the `Request` and return `404`:

```
router :: Request -> ResponseM
router _ = HTTPure.notFound
```

That’s our stub.

Next, we’ll create our `main`’s Type Signature:

```
main :: Effect Unit
```

And now we’ll run in the `Effect` Monad:

```
main :: Effect Unit
main = do
  ???
```

And we’ll start the server capturing the shutdown Callback:

```
main :: Effect Unit
main = do
  shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
```

> ① We’ll use `shutdown` later.
> 
> ② Don’t miss the third Parameter to `HTTPure.server`, i.e. the Effect to run AFTER the server is running.

And finally, we’ll return `pure unit` for now to keep the compiler happy: