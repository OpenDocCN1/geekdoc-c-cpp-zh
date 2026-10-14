
```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int
  | RaiseParent

handleAction
  :: Action
  -> H.Halogen State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> log "Initialize"
  Finalize -> log "Finalize"
  Increment -> H.modify_ \s -> s { count = s.count + 1 }
  Decrement -> H.modify_ \s -> s { count = s.count - 1 }
  FromChild c -> log $ "Received from Child: " <> show c
  RaiseParent -> H.get >>= \{ count } -> H.raise count
```

① Added this Data Constructor.

② Handle `RaiseParent` by getting the State via `H.get` and then binding to a Function that’ll destructure the `count` and send it to the Parent.

Now, rerun your server, refresh your browser and you should have a screen like:

![](img/8c0e9b687c62642e828ccb5481e11313_1610_0.png)

Now, make sure your console is open. You should have the following:

![](img/8c0e9b687c62642e828ccb5481e11313_1610_1.png)

This shows that all 4 Counters initialized. Chrome will display a count next to lines that have been contiguously logged multiple times with the exactly same message.

Now click `Raise` under the Counter that has a value of 2. It should log:

```
Received from Child: 2
```

Now click on the `+` button 3 times on that same Counter. It should now read 5. Now click again on the `Raise`

```
import Effect.Class (liftEffect) ①
import Effect.Class.Console (log)
import Halogen.Subscription as HS

main :: Effect Unit
main = do
  HA.runHalogenAff do
    body <- HA.awaitBody
    io <- runUI (Counter.component 3) 0 body ②
    void $ liftEffect $ HS.subscribe io.messages \currentCount -> ③
      log $ "Received Count from Top-level Counter: "
        <> show currentCount ④
```

① Added these imports.

② Capture the return from runUI, i.e. io, which is of Type HalogenIO.

③ Subscribe to an Emitter that takes a Function whose first and only Parameter is a Value of Type output from a Top-level Component. In this case, the Top-level Component is a Counter and it's Output Type is an Int.

④ Log the current Counter Value.

Update your main accordingly and rerun the server. Ooops:

```
[info] Build succeeded.
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- halogen-subscriptions
```

We need to add halogen-subscriptions to spago.dhall

Rerun the server, refresh the browser and then click the Top-level Counter's Raise button and see what is printed in the console.

Here's what I get:

```
Received Count from Top-level Counter: 0
```

Now, let's set a Child Counter to 123 whenever it sends us Output. To query a Child, we use either H.tell or H.request.

We use `H.tell` when we’re simply telling the Child to do something. We use `H.request` when we expect something to be returned from the Child.

Since we’re going to set the Child’s Value using `SetValue`, we’re going to use `H.tell`:

```
tell
  :: V state action output m label slots query output' slot _1
  . Row.Cons label (Slot query output' slot) _1 slots
  => IsSymbol label
  => Ord slot
  => Proxy label
  -> slot
  -> Tell query
  -> HalogenM state action slots output m Unit
```

This is a daunting Type Signature. But, we just care about the Parameters, which are `Proxy label`, `slot` and `Tell query`.

That means we’ll write something like:

```
H.tell _counter someSlotNumber ...
```

Here `someSlotNumber` is the slot number that identifies our Child.

And `_counter` is our `Proxy` for the label in our `Slots` Type:

```
type Slots = ( counter :: H.Slot Query Output Int ) ❶
```

❶ Here `Int` is the Type of the Value that uniquely identifies a particular `slot` that a Child occupies.

`H.tell` is how you tell a Child to perform a Procedure, i.e. do something with no return Value, as opposed to `H.request` that tells the Child to perform a Function, i.e. compute something returning a Value.

Here’s the rest of the `H.tell` call:

```
H.tell _counter someSlotNumber $ SetCount 123
```

The problem is that we still have to figure out what `slot` the Child is in that called `H.raise`, i.e. what number to put in place of `someSlotNumber`.

Looking at the `FromChild` Data Constructor, we can see that we have no information regarding that:

```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int ①
  | RaiseParent
```

① This Int is the count Value NOT which Child.

We’ll need to add another Parameter to FromChild that contains the slot Value.

Go ahead and change the FromChild Data Constructor to have another Parameter for slot, then change handleAction code to set the Child’s count Value to 123 in FromChild keeping the existing log functionality and finally update the render Function where FromChild is used to map Child Outputs to Actions to include the Child’s slot identifier, i.e. it’s slot number.

Then return here.

First, we’ll add another Int to FromChild.

```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int Int ①
  | RaiseParent
```

① The first Int is the slot number since we’re going to Partially Apply this in the render Function.

Those 2 Int Parameters to FromChild are confusing. Which Int is which again? Let’s fix that:

```
type SlotNum = Int ①
type CounterValue = Int

data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild SlotNum CounterValue ②
  | RaiseParent
```

+   1 Create Type Aliases to distinguish the different Ints.
+   2 Use the new Type Aliases.

Next, we’ll update FromChild in handleAction:

```
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> log "Initialize"
  Finalize -> log "Finalize"
  Increment -> H.modify_ \s -> s { count = s.count + 1 }
  Decrement -> H.modify_ \s -> s { count = s.count - 1 }
  FromChild slot c -> do ① ②
    void $ H.tell _counter slot $ SetCount 123 ③
    log $ "Received from Child: " <> show c ④
  RaiseParent -> H.get >>= \{ count } -> H.raise count
```

+   1 Added slot Parameter as the first Parameter.
+   2 Added a do block since we’re doing multiple steps now.
+   3 We query the slot of the Child who sent us Output and tell it to SetCount to 123. We had do use void since this returns a Maybe Unit.
+   4 We still log like we did before.

And finally, we need to Partially Apply FromChild in render with the slot number:

```
-- ABOVE CODE REDACTED
where
  children = if numChildren == 0 then [] else
    [ HH.div [
        HC.style do
          display flex
          paddingLeft (rem 1.0)
          paddingTop (rem 1.0)
          paddingBottom (rem 1.0)
      ] $
      range 0 (numChildren - 1) <#\n ->
        HH.slot _counter n (component 0)
        (n + 1) (FromChild n) ] ①
```

+   1 Pass the slot number, i.e. n, as the first Parameter to FromChild.

Now, rerun your server and refresh your Browser. Then click on the third Child Counter’s `Raise` Button. It should change its value to `123` and log the following:

```
Received from Child: 3
```

Fix this message so it also displays which Child it received from, e.g. `Received from Child 2: 5`. Then continue reading.

Here’s that change:

```
·· ABOVE CODE REDACTED
   FromChild slot c -> do
      void $ H.tell _counter slot $ SetCount 123
      log $ "Received from Child " <> show slot <> ": " <> show c
·· BELOW CODE REDACTED
```

❶ Added the slot info to the log output.

Re-testing should now log:

```
Received from Child 2: 3
```

That can be confusing since humans don’t count starting at zero. Change the code to add `1` to the `slot`:

```
·· ABOVE CODE REDACTED
   FromChild slot c -> do
      void $ H.tell _counter slot $ SetCount 123
      log $ "Received from Child " <> show (slot + 1) <> ": " <> show c
·· BELOW CODE REDACTED
```

❶ Added `1` to `slot`.

Now it displays:

```
Received from Child 3: 3
```

Now, request the counter value in `FromChild` right AFTER we change it to `123`. Use `H.request` and `GetCount`. Realize that `H.request` will return a `HalogenM` state action slots output m (Maybe a).

Once you have that value, then log it to the console.

Add that code before returning here.
