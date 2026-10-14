
import Prelude ①

class Monad m <= Log m where

① Added this import to get Monad definition.

And next, the logEntry Type Signature:

```
class Monad m <= Log m where
  logEntry :: LogLevel -> String -> m LogEntry ① ②
```

① The timestamp will be calculated in the implementation of this Method.

② Since getting the timestamp will involve running in Effect, this is a Monadic computation, hence m LogEntry.

And finally, we’ll add the log Type Signature:

```
class Monad m <= Log m where
  logEntry :: LogLevel -> String -> m LogEntry
  log :: LogEntry -> m Unit ①
```

① By design, the expectation for implementations of this Typeclass is that log will leverage the log that runs in Aff.

And now, add the HalogenM instance for this Typeclass like we did for Navigate so we won’t have to lift calls to log or logEntry in HalogenM Functions, i.e. handleAction and handleQuery.

Then return here when that’s complete.

Here’s that implementation:

```
import Control.Monad.Trans.Class (lift) ①
import Halogen (HalogenM)

instance logHalogenM
  :: Log m
  => Log (HalogenM state action slots output m) where
logEntry level = lift <<< logEntry level ②
log = lift <<< log
```

① Added these imports.

② This is written as Point-free as is possible since these Functions take 2 Parameters.

These Capabilities seem sufficient for our Application at the moment. We may need to add more as we go along, but this is a good starting point.

## 30.5. Capability Implementations

We defined our Capabilities and now it’s time to implement them. They will be implemented by the Monad that our Components run in. This is typically referred to as m, for example:

```
component
  :: ∀ m
  . MonadAff m
  => MonadAsk Env m
  => H.Component Query Input Output m
```

In our Application the m here is AppM, which means that we’re going to have to make the following AppM Instances:

```
LogonRoute
Navigate
Log
```

We’ll start with LogonRoute. Since our learning application is so limited, we don’t really have too many places to go when a user logs on.

In a real application, we may decide that administrators route first to the admin section of the app, whereas, normal users would go to a dashboard or a some special landing page.

For us though, we’re going to route everyone to Users with no User selected EXCEPT when the password needs to be changed. In that case, we’ll route them to a dummy page where they COULD change their password.

Since our overly simplified server doesn’t support password changes, we’ll just have a button on the dummy page that when clicked will navigate the user to the Users page.

First, add ChangePassword as a Route to Route.purs and then write the instance for LogonRoute in App.purs to abide by the above specifications before reading further.

Here’s the change to Route:

```
data Route
  = Logon
  | Logoff
  | Users (Maybe String)
  -- | Users (Maybe UserId)
  | ChangePassword ①
```

① Added new Route Data Constructor for the Change Password Page.

And now, the compiler is telling us that something is wrong with routeCodec. It should be clear that we’re missing the entry for ChangePassword:

```
routeCodec :: RouteDuplex' Route
routeCodec = root $ sum
  { "Logon": path "logon" noArgs
  , "Logoff": path "logoff" noArgs
  , "Users": "users" / (optional $ userId segment)
  , "ChangePassword": path "change-password" noArgs ①
  }
```

① This Route entry is simply /change-password with no arguments.

Now, here’s the instance implementation in AppM:

```
import Capability.LogonRoute (class LogonRoute, PasswordType(..)) ①
import Data.Maybe (Maybe(..))
import Data.Route (Route)
import Data.Route as Route

-- COMPILER ERROR!!
instance logonRouteAppM :: LogonRoute Route where
  logonRoute _ PasswordPermanent = Route.Users Nothing ②
  logonRoute _ PasswordTemporary = Route.ChangePassword ③
```

① Added these imports.

② Users with permanent passwords will route to the Users Page.

③ User with temporary passwords will route to the Change Password Page.

Now there are 2 issues with this. First, we have a compiler error. We’ll fix that soon enough. But notice how we’re not using the UUID Parameter.

Seems as if that was a bad initial design decision. Let’s fix that by removing it from the Typeclass and our

Instance implementation.

Make those changes before reading further.

Here are those changes. First, the one in `Capability.LogonRoute`:

```
class LogonRoute route where
  logonRoute :: PasswordType -> route
```

> Removed UUID Parameter, which warranted the removal of the import of Data.UUID.

Also, removed:

```
import Data.UUID (UUID)
```

And now, here’s the change to our instance implementation:

```
-- COMPILER ERROR!!
instance logonRouteAppM :: LogonRoute Route where
  logonRoute PasswordPermanent = Route.Users Nothing
  logonRoute PasswordTemporary = Route.ChangePassword
```

> Removed the first Parameter.

Okay, now let’s look at that pesky compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1677_0.png)

We have an Orphaned Instance since we’re coding in `AppM.purs`, which is not where Route is defined.

My first mistake was not putting an m in the Typeclass. We can fix that by doing the following:

```
-- COMPILER ERROR!!
class LogonRoute m route where
  logonRoute :: PasswordType -> route
```

But now the compiler is complaining that logonRoute doesn't have a an m:

![](img/8c0e9b687c62642e828ccb5481e11313_1678_0.png)

We could simply fix this with a Functional Dependency:

```
-- NOT A GOOD IDEA!!
class LogonRoute m route | route -> m where
  logonRoute :: PasswordType -> route
```

This compiles but still requires us to put the Typeclass instance in Route. This is bad since we want to add the Capability Constraint to the Component for m. There is no Route Parameter for our Components.

So, we could reverse the Functional Dependency:

```
-- COMPILER ERROR!!
class LogonRoute m route | m -> route where
  logonRoute :: PasswordType -> route
```

And now the compiler is complaining about not have an m again in the Type Signature of logonRoute.

So, we'll simply have to change this Pure Function into a Monadic one:

```
import Prelude ①

class Monad m <= LogonRoute m route where ②
  logonRoute :: PasswordType -> m route ③
```

+   ① Added to get Monad.
+   ② Made Monad a Superclass.
+   ③ Changed return Type from route to m route.

Update your definition. Then change your AppM Instance to add pure to the return Value:

```
instance logonRouteAppM :: LogonRoute AppM Route where ①
  logonRoute PasswordPermanent = pure $ Route.Users Nothing
  logonRoute PasswordTemporary = pure Route.ChangePassword
```

❶ Added `AppM` for `m`.

Now add a Halogen Instance for `LogonRoute` using what we did with `Navigate` and `Log` as references, then return here when you’re done.

Here’s that change:

```
import Control.Monad.Trans.Class (lift) ❶
import Halogen (HalogenM)

instance logonRouteHalogenM
  :: LogonRoute m route
  => LogonRoute (HalogenM state action slots output m) route where
  logonRoute = lift <<< logonRoute
```

❶ Added these imports.

The next Capability to implement in `AppM` is `Navigate`. Look up `setHash` from `Routing.Hash` in Pursuit before attempting to code this Instance. Also, look up `print` in `Routing.Duplex`. Give it a try before reading on.

Here’s the implementation:

```
import Capability.Navigate (class Navigate) ❶
import Effect.Class (class MonadEffect, liftEffect)
import Routing.Duplex as RouteDuplex
import Routing.Hash (setHash)

instance navigateAppM :: Navigate AppM Route where
  navigate = liftEffect <<< setHash
    <<< RouteDuplex.print Route.routeCodec ❷ ❸ ❹
```

+   ❶ Added these imports.
+   
+   ❷ Written Point-free with the `Route` being the unnamed Parameter.
+   
+   ❸ First we take our `Route` and run it through our Codec to produce a `String` that we then give to `setHash` to change the Browser’s Hash value.
+   
+   ❹ Had to `liftEffect` since `setHash` runs in `Effect`.

And finally, write the code for the `Log` Instance. Look up, in Pursuit, `Effect.DateTime` to find a Function that will get the current time into a `DateTime`.

When you implement `log` make sure you log the whole Record to the console.

Return here when you’re done.
