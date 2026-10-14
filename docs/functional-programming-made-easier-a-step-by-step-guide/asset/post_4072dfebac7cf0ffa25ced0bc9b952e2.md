
And finally, let’s look at an HTTPure.Request:

```
type Request =
  { method :: Method.Method
  , path :: Path.Path
  , query :: Query.Query
  , headers :: Headers.Headers
  , body :: String ①
  , httpVersion :: Version.Version
  }
```

① Our API JSON will be in the body. This is the String each Handler will process.

Study these pieces of information before you begin adding code to router in the Main module. Then add a bit of code to use oneOf and get a Handler into a Variable called handler.

Don’t go any further than that in your coding. Still return HTTPure.notFound for now so that our code will still compile. Then read on when you get stuck or hit an insurmountable compiler error.

The first step is to destructure the Request to get to the body since handle needs the JSON request:

```
router :: Request -> ResponseM
router { body } = HTTPure.notFound
```

Now, we’re going to add oneOf with a list of Handlers, of which we only have 1 at the moment:

```
import Data.Foldable (oneOf) ①
import Handler.Api.Logon (Logon)
import Handler.Class.ApiHandler (handle)
import Type.Proxy (Proxy(..))

router :: Request -> ResponseM
router { body } =
  -- COMPILER ERROR!!
  let handler = oneOf [handle body (Proxy :: _ Logon)] in ②
  HTTPure.notFound
```

① Added these imports.

② We use Proxy to define which handle Method to use.

Even though this has a compiler error, take the time to update your code to look like this.

Here’s the error:

![](img/8c0e9b687c62642e828ccb5481e11313_1402_0.png)

Can you see what’s wrong? It’s not obvious.

It turns out that oneOf from Data.Foldable has a Plus Constraint on our Functor, i.e. Either. Remember that Plus is just a Monoid for Types with 2 Type Parameters.

That means that it needs an empty value for Either. This is because its possible to pass oneOf an empty Array. In that case, it’ll use empty from Plus as it’s choice.

But, there is no Plus Instance for Either. When we talked about Plus, we saw how it’s impossible to write a Plus instance for Either. That means we cannot use oneOf. Well, not this oneOf.

Instead, we’ll have to use oneOf from Data.NonEmpty, which has no such restriction since it cannot get an empty Array. And since it cannot get an empty Array, this version of oneOf can always pick something:

```
oneOf :: ∀ f a. Alternative f => NonEmpty f a -> f a ①
```

① Here f is the Alternative, which is a Functor. In our case, it’s an Array.

Modify router to use Data.NonEmpty’s version of oneOf before you read any further.

First, delete:

```
import Data.Foldable (oneOf)
```

And make these changes:

```
import Data.NonEmpty (oneOf, (:|)) ①

router :: Request -> ResponseM
router { body } =
  let handler = oneOf $ (handle body (Proxy :: _ Logon)) :| [] in ② ③
  HTTPure.notFound
```

① Replaced the import of oneOf from Data.Foldable with this one. Also, included the Binary Operator for constructing a NonEmpty.

② Construct a NonEmpty Array using : |.

③ Ignore the warning about not using handler.

Now that we have handler, realize that it’s going to be an Either. And when it’s a Left it’ll be the error from the last thing that is in the Array.

We don’t really care about the errors of the last Handler. It’s of no use to us or the client. We’re just going to return an HTTP error code 400, which is Bad Request.

So, change your code to deal with just the error case of oneOf call. Realize that your code won’t compile after that.

Here’s that change:

```
router :: Request -> ResponseM
router { body } =
  case oneOf $ (handle body (Proxy :: _ Logon)) :| [] of ①
    Left _ -> HTTPure.badRequest body ②
    ???
    HTTPure.notFound
```

① Changed the code from a let to a case.

② We don’t care about the error details here. We just respond with badRequest, i.e. HTTP status of 400.

The next question we should ask ourselves is what Type is in the Right? How can we figure that out?

Well, we can simply look at Handler’s definition:

```
type Handler = ReaderT HandlerEnv Aff Response
```

This shows us that we have a ReaderT that needs to be run. But we don’t have any read-only Value to pass to runReaderT yet.

We’ll need to get that from main. So our code will compile while we work on main, comment out the case expression and we’ll return to this in a minute:

```
```haskell
router :: Request -> ResponseM
router { body } =
  -- case oneOf $ (handle body (Proxy :: _ Logon)) :| [] of ❶
  --   Left err -> HTTPure.badRequest body
  HTTPure.notFound
```
```

❶ Commented out just for now.

Now, let’s turn our attention to `main`:

```
```haskell
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
```

We need to startup the Account Manager and then use the `accountsVar` that it returns to pass to our `router` so it can call `runReaderT` with it.

Add the code to `main` to startup the Account Manager before reading on.

The first problem we encounter is that the code in `main` is running in `Effect` but not `Aff` like the rest of our program.

So, that’s the first change to make:

```
import Effect.Aff (launchAff_)
import Effect.Class (liftEffect)

main :: Effect Unit
main = launchAff_ do
  liftEffect $ do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    let shutdownServer = do
      log "Shutting down server..."
      shutdown $ log "Server shutdown."
    onSignal SIGINT shutdownServer
    onSignal SIGTERM shutdownServer
```

① Added these imports.

② Run this do block in Aff.

③ Lift this do block, which runs in Effect, into Aff.

Now we make a call to startup

```
import Manager.Account as AccountManager

main :: Effect Unit
main = launchAff_ do
  accountsAvar <- AccountManager.startup []
  liftEffect $ do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    let shutdownServer = do
      log "Shutting down server..."
      shutdown $ log "Server shutdown."
    onSignal SIGINT shutdownServer
    onSignal SIGTERM shutdownServer
```

① Full qualify the Account Manager.

② Used an empty account list for now. We really need to get this from the Account Handler.

Make sure your code is up to date with this and then add code to call the Account Handler to load the accounts. Don’t forget that this will create the file if need be.

Once you do, take the accounts that it loaded and replace our [] with them. Give this a go before reading on.

Here’s that change:

```
import Handler.Account as AccountHandler ①

main :: Effect Unit
main = launchAff_ do
  accounts <- AccountHandler.loadAccounts ②
  accountsAvar <- AccountManager.startup accounts -- COMPILER ERROR!! ③
  liftEffect $ do
    shutdown <- HTTPure.serve port router
    $ log $ "Server up running on port: " <> show port
    let shutdownServer = do
      log "Shutting down server..."
      shutdown $ log "Server shutdown."
  onSignal SIGINT shutdownServer
  onSignal SIGTERM shutdownServer
```

① Import Handler.Account qualified as AccountHandler.

② Load the accounts from the Account Handler.

③ Startup the Account Manager with accounts.

Here’s the compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1406_0.png)

Looks like I forgot that loadAccounts can have errors:

```
loadAccounts :: Aff (Either ParseError (Array Account))
```

So, we’ll fix my mistake:

```
main :: Effect Unit
main = launchAff_ do
    loadResults <- AccountHandler.loadAccounts
    case loadResults of
        Left err -> log $ "Cannot load accounts: " <> show err
        Right accounts -> do
            accountsAVar <- AccountManager.startup accounts
            liftEffect $ do
                shutdown <- HTTPure.serve port (router { accountsAVar }) ①
                $ log $ "Server up running on port: " <> show port
            let shutdownServer = do
                log "Shutting down server..."
                shutdown $ log "Server shutdown."
            onSignal SIGINT shutdownServer
            onSignal SIGTERM shutdownServer
```

① Partially apply HandlerEnv to router, which returns a Function of Type Request -> ResponseM, which is exactly what HTTPure.server expects as its first Parameter.

At this point, router has enough information to call runReaderT. Uncomment the code in router and then finish the case expression by calling the ReaderT that the Right case gets back. Then read on.

Here’s that change:

```
import Control.Monad.Reader (runReaderT) ①
import Data.Either (Either(..))

router :: HandlerEnv -> Request -> ResponseM
router env { body } =
    case oneOf $ (handle body (Proxy :: _ Logon)) :| [] of
        Left _ -> HTTPure.badRequest body -- COMPILER ERROR!!
        Right handler -> runReaderT handler env ② ③
```

① Added these imports.

② Call runReaderT with the HandlerEnv. This will return an Aff Response, which is a ResponseM.

③ Removed HTTPure.notFound.

And the compiler error is as follows:
