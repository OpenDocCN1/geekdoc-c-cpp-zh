
```
```scala
shutdown :: Effect Unit -> Effect Unit
```
```

It’s a function that takes code written in `Effect` and produces an `Effect`. The means that `shutdown` can take a `do` block and that the return Value of that call can then be passed to `onSignal`’s second Parameter:

```
```scala
onSignal :: Signal -> (Effect Unit -> Effect Unit) ❶
```
```

> ❶ Added redundant Parentheses to help us see that the Parenthetical is the same Type Signature for `shutdown`.

Okay, based on all of this research, add SIGINT code to `main` that calls `shutdown` with clean up logic in a `do` block. We don’t have any clean up work to do yet, so we’ll just log a message to the console that we’ve shutdown the server. Once you’re done coding, return here.

The first thing to do is to include `onSignal`:

```
```purescript
import Node.Process (onSignal) -- COMPILER ERROR!!
```
```

This compiler error lets us know that we’re going to have to include some package in `spago.dhall`. Use Pursuit to see what package `Node.Process` is in, then add it to your `spago.dhall` if you haven’t already. Then read on.

Here’s the change to `spago.dhall`:

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
[ "aff"
, "arrays"
, "console"
, "effect"
, "foreign-generic"
, "httpure"
, "maybe"
, "node-process" ①
, "prelude"
, "psci-support"
, "uuid"
]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① Added here to maintain alpha order.

Run:

```
npx spago build
```

The next change to make is to setup the signal handler:

```
main :: Effect Unit
main = do
  shutdown <- HTTPure.serve port router
  $ log $ "Server up running on port: " <> show port
  onSignal SIGINT do ①
    ???
    pure unit
```

① We pass a do block to onSignal.

We’ll log that the server is shutting down. This is useful if the shutdown takes long:

```
main :: Effect Unit
main = do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    onSignal SIGINT do
        log "Shutting down server..." ①
        ???
        pure unit
```

① Log before we call shutdown.

For now, we’re just logging that we’re shutting down. In the future, we may want to do some other clean up in the do block.

And finally, we’ll call shutdown to shutdown the HTTP server:

```
main :: Effect Unit
main = do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    onSignal SIGINT do -- COMPILER ERROR!! ①
        log "Shutting down server..."
        shutdown $ log "Server shutdown."
```

① We don’t need pure unit anymore since onSignal returns Effect Unit.

From the compiler error, we can see that we need to import the SIGINT Data Constructor. If you haven’t done this yet, figure out what to import from Pursuit before reading any more.

According to Pursuit, Signal is in Data.Posix.Signal:

```
import Data.Posix.Signal (Signal(SIGINT)) ①
```

① Include SIGINT Data Constructor. We could have also imported Signal(...).

Add this import and make sure you code matches main above.

Also, add posix-types to spago.dhall.

Now, before you run this, there’s something you’ll need to know. Our SIGINT handler will NOT work if we run our server with:

```
npx spago run
```

With this command, npx is run, which, in turn, runs node as a child process. So when Ctrl-C is pressed at the command line, it goes to the parent process, which is npx and not node. Upon receipt of SIGINT, npx will terminate causing our program to terminate. Before that happens though, your program will be sent SIGTERM, which we aren’t handling at the moment.

We can get around this problem by running our program like:

```
npx spago build && node -e "require('./output/Main/index').main()" ① ②
```

① The && is a way to run a second command if the first one succeeds. You can also manually run these commands one right after the other.

② node -e "require('./output/Main/index').main()" came from the Spago documentation as the one extra command that’s run for spago run compared with spago build.

Now, when you hit Ctrl-C, node will get the SIGINT, which will cause your signal handler to be called.

Go ahead and run your program this new way and once it’s up and running, hit Ctrl-C and see what happens.

It should print out:

```
Server up running on port: 3000
^CShutting down server...
Sever shutdown.
```

We can also support SIGTERM instead of SIGINT or better yet, we support both since we’re not always going to run our server using npx.

Another good reason to handle SIGTERM is if you’re going to run your server in a Container like Docker. If you run your server as the main app in a Docker container, then, by default, Docker will send your server a SIGTERM before the Container is shutdown.

Many times, servers need to do real clean up tasks and trapping this signal is advantageous.

Change your code to handle the both the SIGINT and SIGTERM signals before reading any further.

First, we’ll add SIGTERM to our imports:

```
import Data.Posix.Signal (Signal(SIGINT, SIGTERM)) ①
```

① If we had included all Data Constructors with (..), we wouldn’t have to do this. But in this rare case, I like having them listed out explicitly since it lets us know that these are the ONLY 2 signals that are supported.

Next, we’ll factor out the shutdown code:

```
main :: Effect Unit
main = do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    let shutdownServer = do
        log "Shutting down server..."
        shutdown $ log "Server shutdown."
    onSignal SIGINT shutdownServer
```

① Factored out the do block as shutdownServer.

② Removed do block and using shutdownServer.

And finally, we handle SIGTERM:

```
main :: Effect Unit
main = do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    let shutdownServer = do
        log "Shutting down server..."
        shutdown $ log "Server shutdown."
    onSignal SIGINT shutdownServer
    onSignal SIGTERM shutdownServer
```

① Added SIGTERM handler.

Now, we’re ready to continue adding features. But before we do, we should consult our diagram:

When I'm implementing an API, I like to build the code in the order that it'll most likely be called in, e.g. we should code Logon before Logoff. By doing it this way, I can test my code as I write it.

Imagine, instead, that we coded Logoff before Logon. In that case, we wouldn't be able to confidently test Logoff until Logon was done.

So, we might as well, code in the general order the API calls will be made. And that means that Logon is first.

We already have modules where we modeled our API Requests and Responses, e.g. Api.Logon. We could put our Handler code in those modules, or we could keep them as just our model definitions and put our Handler code in their own modules.

Which do you think we should do and why?

My thought is that if I put too much into those files, I may regret it in the future and need to refactor then. The Separation of Concerns up front is nice, but will require a little bit of rearranging at the moment.

I'm on the fence, but will error on the side of overly separating. So, let's do that.

Add a new folder under src called Data and then move the Api folder under it by dragging and dropping it.

Next change each file's module definition to start with Data.Api now that they're in a new location.

Then comment out every line of Test.purs except for the module declaration. Test.purs has outlived its usefulness and we don't want future changes we make to break our build since it most likely will no longer compile. We're commenting instead of deleting it so that we can keep if for reference.

Since, Logon is the first API call we will have to make, let's code that up and then we can test it.

First, create a Folder under src called Handler and then create a Folder under src/Handler called Api.

Then in that directory create a file called Logon.purs with the following:

```
module Handler.Api.Logon where
```

Before we start coding the Logon Handler, let's look at our router, which will need to decode the response and then dispatch it to the appropriate Function:

```
router :: Request -> ResponseM
router _ = HTTPure.notFound
```

Okay, so our router is a bit anemic at the moment. We need it to decode the Request and then based on what it decoded, call the appropriate Handler.

What's the best way to do this? What do you think?
