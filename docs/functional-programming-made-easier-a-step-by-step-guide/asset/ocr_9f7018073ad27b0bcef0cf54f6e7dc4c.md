H.raise.

And finally, we’re going to handle when the user clicks on Logoff:

```
import Capability.Navigate (class Navigate, navigate) ①
import Data.Route as Route ②

-- ABOVE CODE REDACTED
where
handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) iOutput m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output output -> H.raise output
  Logoff -> navigate Route.Logoff ③
```

① Added navigate to the import list.

② Fully qualify Route so Logoff won’t be ambiguous, since it could represent a Route or an Action.

③ Navigate to the Logoff Page.

Now, we’re ready to code handleQuery. This just needs to delegate the call to the Inner Component.

Take a look at the halo Application to see how we wrote the Type Signature for handleQuery there. Remember, our Types have Polymorphic Parameters, e.g. State in the halo Application should be replaced with State iInput here.

Stop reading and see if you can write just the Type Signature. Return here once you’ve completed that task to see how you did.

Here’s the Type Signature for handleQuery:

```
-- ABOVE CODE REDACTED
where
-- handleAction REDACTED
handleQuery
  :: ∀ a
  . iQuery a
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) iOutput m (Maybe a)
```

Now, write the implementation, but delegate it to the Inner Component using H.query. Once again, look to