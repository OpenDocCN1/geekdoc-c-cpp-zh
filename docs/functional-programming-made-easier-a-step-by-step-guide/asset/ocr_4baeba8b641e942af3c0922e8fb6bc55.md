returns something other than an Effect. Well, it turns out that you cannot.

And now, you’re probably wondering what ServerM is:

```
type ServerM = Effect (Effect Unit -> Effect Unit)
```

It’s a Type Alias for Effect, which means that our main is returning an Effect. But what is the Function it returns?

Well, it’s a Callback to shutdown the server. This shutdown Function can never be called since we’re returning it from main.

Hit Ctrl-C in the Terminal window to kill the server.

Change your main to take advantage of this Callback as such:

```
import Data.Time.Duration (Milliseconds(..)) ①
import Effect (Effect)
import Effect.Aff (launchAff_)
import Effect.Class (liftEffect)

main :: Effect Unit ②
main = do
  shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port ③
  launchAff_ do ④
    delay (Milliseconds 2000.0) ⑤
    log "Shutting down server..."
    liftEffect $ shutdown $ log "Server shutdown" ⑥
```

+   ① Add these imports.

+   ② Main now returns Effect Unit.

+   ③ Create the server and capture the shutdown Function.

+   ④ Start a separate process that runs under Aff to eventually shutdown the server.

+   ⑤ Delay 2 seconds.

+   ⑥ Shutdown the server.

The shutdown Function runs in Effect as we can see from its Type Signature, Effect Unit -> Effect Unit. But, since we’re calling shutdown in Aff, we have to use liftEffect.

Then remove the following imports: