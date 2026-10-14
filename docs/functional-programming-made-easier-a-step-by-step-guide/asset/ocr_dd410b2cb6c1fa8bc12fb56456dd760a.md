+   - Call server to query users
+   - Update State accordingly

Now, write the code for Initialize to query the backend for users and initialize the State. Steal code from what we did on the Logon Page to make API calls to the backend.

Use the same alertError Function for now for errors. We'll replace this in the next section when we create a Modal Dialog Component.

Then return here when you're stuck or ready to move on.

We'll start coding with:

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    ???
```

And now, we need to check the LoggedOnUser, which we can get from the ReaderT environment:

```
import Control.Monad.Reader.Class (class MonadAsk, ask) ①
import Effect.Ref as Ref
import Env (Env)

component
  :: ∀ m
  . MonadAff m
  => MonadAsk Env m ②
  => Navigate m Route
  => H.Component Query Input Output m
-- BELOW CODE REDACTED

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask ③
    loggedOnUser' <- H.liftEffect $ Ref.read userRef ④
    ???
```

① Added these imports.

② Added this Constraint so we can call ask.

③ Get userRef from environment.