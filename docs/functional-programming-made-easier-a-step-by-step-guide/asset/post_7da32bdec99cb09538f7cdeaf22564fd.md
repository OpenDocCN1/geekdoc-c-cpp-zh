
Here’s that implementation:

```
```haskell
import Capability.Log (class Log)
import Effect.Class.Console as Console
import Effect.Now (nowDateTime)

instance logAppM :: Log AppM where
  logEntry level message =
    liftEffect nowDateTime >>= pure <<< { level, message, timestamp: _ }
  log = Console.log <<< show -- COMPILER ERROR!!
```
```

+   1. Added these imports.
+   2. Fully qualify as `Console` since `log` will conflict with our Instance Method, `log`.
+   3. `liftEffect` on `nowDateTime` so it’ll run in `AppM`,
+   4. `bind` to an Anonymous Function to create `LogEntry` and then compose with `pure` to wrap it in `AppM`. You can look at the `_` as the space where the timestamp goes. It the Value returned from `nowDateTime`.
+   5. `show` the `LogEntry` Record.

And we have a compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1680_0.png)

Looks like `LogLevel` isn’t showable. Add the code to make it so before reading any further.

Here are the lines of code to add to `Capability.Log`:

```
```haskell
import Data.Generic.Rep (class Generic)
import Data.Show.Generic (genericShow)

derive instance genericLogLevel :: Generic LogLevel _

instance showLogLevel :: Show LogLevel where
  show = genericShow
```
```

And now return to `AppM.purs` and save the File to see if it compiles.

And it does.

## 30.6. Router Component

Let’s look back on our implementation of Navigate:

```
instance navigateAppM :: Navigate AppM Route where
  navigate = liftEffect <<< setHash
    <<< RouteDuplex.print Route.routeCodec
```

We’re setting the Browser’s Hash value, but no one is listening to the change.

We could use addEventListener:

```
addEventListener
  :: EventType
  -> EventListener
  -> Boolean
  -> EventTarget
  -> Effect Unit
```

And then we’d have to use the following Functions to be able to handle Hash change events:

```
hashchange :: EventType
eventListener :: ∀ a. (Event -> Effect a) -> Effect EventListener
toEventTarget :: Window -> EventTarget
```

But, as it turns out Routing.Hash has already done all of the hard work for us in a Function called matchesWith, which allows us to pass in our own parser:

```
matchesWith
  :: ∀ f a
    . Foldable f
  => (String -> f a) ①
  -> (Maybe a -> a -> Effect Unit)
  -> Effect (Effect Unit)
matchesWith parser cb = ... ②
```

① The parser must return a Foldable. This may seem to be a problem since RouteDuplex’s parser returns an Either, but as it turns out, Either has a Foldable Instance.

② The implementation is not important here.

Our plan will be to use `matchesWith` in our `main` and the use `H.mkTell` to let our Top-level Component know that the Hash has changed. `H.mkTell` is used when telling a Top-level Component.

This Top-level Component will be our Router Component:

![](img/8c0e9b687c62642e828ccb5481e11313_1682_0.png)

Each Page will be a Child Component of the Router Component. It will decide which Child to render depending on the current `Route`.

For now, let’s build the Router Component. We’ll stub out the `render` Function to display a message based on the page that’s supposed to be displayed for now.

Make a Folder called `Component` under `src` then make a File called `Router.purs` under `src/Component`.

Use your `halo` Application as a reference guide to help you as you write the code for `Router`.

As with any Halogen Component, we’ll have to define Types for the following:

+   - `Input` (from Parent)
+   - `Output` (to Parent)
+   - `State`
+   - `Action` (events from EventListeners)
+   - `Query` (`H.tell` or `H.request` from Parent)
+   - `Slots` (for Children)

Define `Input` for `Router` before reading on.

There isn’t any input from the Application, i.e. the Top-level’s "Parent", so we’ll make it `Unit`:

```
import Prelude ①

type Input = Unit
```

① Added import for Unit.

Nothing in our specification for Router tells us that we need Input yet. We may discover that this needs to change, but for now, we’ll just make it Unit. Remember, Parent Components always provide Input to their Child Components. This is why we cannot make this Void.

Next, define Output, then read on.

There is no useful information to communicate to the Application so we’ll just make it Void:

```
type Output = Void
```

Notice how we made Output equal to Void but we didn’t make Input a Void. Why not?

It turns out that we always have to pass an Input to the Top-level or Child Component, so it must exist. Since we’re never going to call H.raise, we have no such requirement for the Output.

Next, we should define the State. This will help us define Action and Query. Do this and then keep reading.

At the moment there’s no real need to keep track of anything in our Router:

```
type State = {}
```

And now, define Action and then return back here.

Once again, there’s no will be no EventSources in our Router. There will only be Child Components which are the Pages of our Application:

```
type Action = Void
```

And now define Query keeping in mind that we’re going to get route changes from the Application. This will be done with H.mkTell to let us know that the Hash changed requiring us to Route to the new page.

Also, refer to our halo Application, especially the Query definition in the Counter Component.

Once you’re done, continue reading.

Here’s our definition:

```
import Data.Route (Route) ①

data Query a = Navigate Route a ② ③
```

① Added this import.

② The a is the rest of the computation and is required of the Query API by Halogen.

③ Route is the route to navigate to.

And finally, we have to define the Slots for all of the Child Components which will be our individual Pages. Once again refer to the halo Application. Return back here once you’re done.

Here’s the Row definition:

```
import Data.Const (Const) ①
import Halogen as H

type PageSlot = H.Slot (Const Void) Void Unit ② ③

type Slots =
  ( logon :: PageSlot
  , logoff :: PageSlot
  , users :: PageSlot
  , changePassword :: PageSlot
  )
```

① Added imports.

② Convenience Type for a Slot that’s just a Page. Note the Unit to uniquely distinguish Children of the same Type. There will never be more than one Page as a Child so Unit is enough to uniquely identify the one and only.

③ Since there is no communication from the Pages to the Top-level Component, the query is set to Const Void and output is Void.

Next, let’s add the Symbol Proxies for the Child Slots:

```
import Type.Proxy (Proxy(..)) ①

_logon = Proxy :: Proxy "logon"
_logoff = Proxy :: Proxy "logoff"
_users = Proxy :: Proxy "users"
_changePassword = Proxy :: Proxy "changePassword"
```

① Added this import.

At this point, we're ready to create the Component. Write the component Function and just stub out the render and handleQuery Functions. Once again, use the halo Application as a reference.

Return here when you're ready to move on.

First, we'll code the component Function:

```
import Effect.Aff.Class (class MonadAff) ①
import Halogen.HTML as HH

component
  :: ∀ m
  . MonadAff m ②
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> {} ③
  , render
  , eval: H.mkEval H.defaultEval {
      handleQuery = handleQuery ④
    }
  }
where
???
```

① Added these imports.

② The Monad m runs in Aff. If you look at AppM.purs, you'll see that we derived MonadAff for AppM.

③ Our input to the Lambda is Unit, so we use _. We return an empty Record for our State.

④ We only need to implement handleQuery all other values are defaulted thanks to H.defaultEval. This is an easy thing to forget. From time to time, you will test your Component and it won't work. And you'll look at your code and scratch your head. When that happens, check here to make sure you've added handleAction, handleQuery, receive, etc.

Next, we'll add our stubbed out Functions:

```
import Data.Maybe (Maybe(..)) ①

-- ABOVE CODE REDACTED
where
  handleQuery
    :: ∀ a
      . Query a
    -> H.HalogenM State Action Slots Output m (Maybe a)
  handleQuery _ = pure Nothing

  render :: State -> H.ComponentHTML Action Slots m
  render _ = HH.text ""
```

① Added this import.

This should compile.

The next step is to flesh out our stubbed out Functions. We’ll start with handleQuery.

Ultimately, we’re going to want to make sure the user’s logged on before we honor Navigate. If the user is NOT logged on, then we’ll redirect them to the Logon Page.

But for now, we’re ONLY going to save the route and let the render Function render the appropriate Child Component.

That last statement should make it clear that our State definition is deficient. We’ll need to save the route in our State.

So first, add route to State. Then finish handleQuery to save the route to the State. Later on, we’ll check to make sure that the user is logged on.

Don’t forget to use the halo Application code we wrote to remind yourself how to modify State in our Component code. Also, make sure you look at how to properly return a value from handleQuery.

Once you’ve completed that task, return here.

First step is to add route to State:

```
type State = { route :: Route }
```

Note that this is not a Maybe Route. We have a reasonable inital Value to give this when we initialize the State. We’ll set it to Logon since the user can’t possibly be logged on when the Router Component is initialized.

Next, we need to change initialize:
