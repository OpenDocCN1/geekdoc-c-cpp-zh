
```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
          "http://localhost:3000/"
          $ Just $ RequestBody.String
          $ encodeJSON $ QueryUsersRequest { authToken }
        let queryResponse = do
              { body } <- lmap Ajax.printError ajaxResult
              lmap show $ runExcept
                $ decodeJSON body :: _ QueryUsersResponse
        case queryResponse of
          Left err -> alertError err
          Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
            ???
          Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) -> do
            ???
```

And now, for the failure case, we’ll alert with an error:

```
-- ABOVE CODE REDACTED
    case queryResponse of
      Left err -> alertError err
      Right (QueryUsersResponse
        (QueryUsersResultsFailure { reason })) ->
        alertError $ "Query Users: " <> case reason of ①
          NotAuthorized -> "Not Authorized"
          NotAuthenticated -> "Not Authenticated"
      Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) -> do
        ???
```

① We have 2 possible Values for QueryUsersFailureReason.

Next, we update the State on the success case:

```
-- ABOVE CODE REDACTED
    case queryResponse of
        Left err -> alertError err
        Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
        alertError $ "Query Users: " <> case reason of
            NotAuthorized -> "Not Authorized"
            NotAuthenticated -> "Not Authenticated"
        Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) ->
            H.modify_ _ { authorized = true, users = users }
```

① Removed the do since this is only 1 line of code.

② We already checked to make sure they were authorized to see this page, so authorized is true.

③ Set users.

And finally, we copy and paste alertError since we’re going to ultimately throw it away:

```
import Web.HTML.Window (alert) ①
import Web.HTML (window)

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string ②
          "http://localhost:3000/"
          $ Just $ RequestBody.String
          $ encodeJSON $ QueryUsersRequest { authToken }
        let queryResponse = do
            { body } <- lmap Ajax.printError ajaxResult
            lmap show $ runExcept
              $ decodeJSON body :: _ QueryUsersResponse ③
        case queryResponse of
          Left err -> alertError err
          Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
            alertError $ "Query Users: " <> case reason of
              NotAuthorized -> "Not Authorized"
              NotAuthenticated -> "Not Authenticated"
          Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) ->
            H.modify_ _ { authorized = true , users = users }
  where
  alertError :: String -> H.HalogenM State Action Slots Output m Unit ④
alertError msg = H.liftEffect $ window >>= alert msg
```

① Added these imports.

② The beginning of our copy/paste block.

③ The ending of our copy/paste block.

④ Copied from 'Logon'.

Now, let’s address our aggregreious copy/paste operation of a large portion of this Function. Factor out the code that we copied from the Logon Page into a Function called apiCall.

Write apiCall without a Type Signature and let the compiler help you determine it. Return here when you’re ready to move forward.

We’ll start by just copying and pasting the code block from handleAction:

```
apiCall = do
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken }
    -- COMPILER ERROR!!
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
```

The compiler error tells us that we need to return something:

```
apiCall = do
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken } -- COMPILER ERROR!!
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
    pure queryResponse ①
```

① We’re returning the response for now.

The new compiler error tells us that we need to pass in authToken:

```
-- COMPILER WARNING!!
apiCall authToken = do ①
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken }
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
    pure queryResponse
```

① Added authToken Parameter.

Now, this compiles. But before we work on the Type Signature, we can simplify the return code. Notice that

we’re defining a Variable called `queryResponse` only to return it via `pure queryResponse`. Let’s eliminate that Variable:

```
— COMPILER WARNING!!
apicall authToken = do
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON $ QueryUsersRequest { authToken }
pure do ❶
  { body } <- lmap Ajax.printError ajaxResult
  lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
```

> ❶ Remember that this `do` block is an `Either`.

The compiler warning is telling us what our Type Signature should be, so we’ll add it:

```
import Data.UUID (UUID) ❶

apiCall :: ∀ t132
  . Bind t132
  => MonadAff t132
  => UUID
  => t132 (Either String QueryUsersResponse)
— BELOW CODE REDACTED
```

> ❶ Added this import.

Looks like `t132` is a Monad. Your number may vary. We’ll remove `Bind` since `MonadAff` requires `t132` to be a Monad. We’ll also rename it to `m`:

```
apiCall :: ∀ m
  . MonadAff m
  => UUID
  => m (Either String QueryUsersResponse)
```

At this point, we can see that this function is not Polymorphic enough. It’ll only work with `QueryUsersRequest`. Let’s fix that:

```
apiCall :: ∀ request response m ①
  . MonadAff m
  => UUID
  -> request ②
  -> m (Either String response) ③
apiCall authToken request = do ②
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON request -- COMPILER ERROR!! ④
  pure do
    { body } <- lmap Ajax.printError ajaxResult
    lmap show $ runExcept $ decodeJSON body :: _ response ⑤
```

① Added request and response.

② Added request Parameter.

③ Changed the Monomorphic Type Parameter from QueryUsersResponse to the Polymorphic Type response.

④ Encode the passed in request.

⑤ The decode Type is now the Polymorphic Type, response.

The compiler error is because we don’t have an Encode Instance for request. So, we’ll require it by using a Constraint:

```
import Foreign.Generic.Class (class Encode) ①

apiCall :: ∀ request response m
  . MonadAff m
  => Encode request ②
  => UUID
  -> request
  -> m (Either String response)
apiCall authToken request = do
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON request
  pure do
    { body } <- lmap Ajax.printError ajaxResult
    -- COMPILER ERROR!!
    lmap show $ runExcept $ decodeJSON body :: _ response
```
