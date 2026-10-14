
--> H.HalogenM State Action Slots (InnerOutput Output) m Unit
errorMsg = H.modify_ <<< errorMsg'

handleQuery ⑤
  :: ∀ a
  . InnerQuery Query a
  -> H.HalogenM State Action Slots (InnerOutput Output) m (Maybe a)
handleQuery = case _ of
  AffirmativeClicked a -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    case loggedOnUser' of
      Nothing -> H.modify_ $ errorMsg' "Session has timed out"
        <<< _ { postModalAction = Just RouteToLogon }
      Just { authToken } -> do
        { userName, password, admin, firstName, lastName } <- H.get
        createResponse <- apiCall (CreateUserRequest
          { authToken
          , user:
            { userName
            , password
            , admin
            , firstName
            , lastName
            , temporaryPassword: true
            }
          })
        case createResponse of
          Left err -> H.modify_ _ { errorMessage = Just err }
          Right CreateUserResultsSuccess -> H.raise $ PassThroughOutput
            $ User
            { userName
            , admin
            , firstName
            , lastName
            , temporaryPassword: true
            }
          Right (CreateUserResultsFailure { reason }) -> case reason of
            NotAuthorized ->
              errorMsg "You're not authorized to create a new user."
            NotAuthenticated ->
              H.modify_ $ errorMsg' "Your session just timed out."
                <<< _ { postModalAction = Just RouteToLogon }
            AlreadyExists ->
errorMsg "A user with that User Name already exists."
FileIOError err -> errorMsg
$ "A fatal error on the Accounts File occurred: "
<> err
pure $ Just a ⑥
_ -> pure Nothing ⑦

① Added (..) to InnerQuery to import Data Constructors.

② Deleted CreateUser Data Constructor.

③ Cut code for CreateUser and pasted it to make handleQuery.

④ Moved these 2 helper Functions out from the where section under handleAction to the same level as handleAction so that handleQuery could also use them. Also, added Type Signatures.

⑤ Created from code cut from handleAction.

⑥ Don’t forget to return Just a as the last step of the AffirmativeClicked case so that our Query processing will be honored.

⑦ Don’t care about any other Queries since we don’t need to do anything for NegativeClicked and PassThroughQuery will never happen since our Query is Void.

And we don’t want to forget to evaluate handleQuery:

```
component = H.mkComponent
{ initialState: \_ ->
{ userName: ""
, password: ""
, admin: false
, firstName: ""
, lastName: ""
, errorMessage: Nothing
, postModalAction: Nothing
}
, render
, eval: H.mkEval H.defaultEval
{ handleAction = handleAction
, handleQuery = handleQuery ①
}
}
```

① Added this.

Now, rebuild the Application and create a user called test with a first name of Test and a last of Test, then go to the server and check the accounts.csv. Then return back here.

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
  handleAction = case _ of
  -- CODE REDACTED
    CreateUserModal output -> case output of
      Modal.Affirmative -> H.modify_ _ { creatingUser = false }
      Modal.Negative -> H.modify_ _ { creatingUser = false }
      Modal.InnerOutput _ -> pure unit ①
  -- BELOW CODE REDACTED

① Here is the Output from the Inner Component.

We can see that we aren’t doing anything with the Output from Component.Modal.CreateUser, which is a User.

Write the code in Component.Users to handle this. It should add the User, which is the first Parameter of InnerOutput, to our State’s User Map, i.e. users.

Return here when that code is complete.

Here’s that change:

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
  handleAction = case _ of
  -- CODE REDACTED
    CreateUserModal output -> case output of
      Modal.Affirmative -> H.modify_ _ { creatingUser = false }
      Modal.Negative -> H.modify_ _ { creatingUser = false }
      Modal.InnerOutput user@(User { userName }) -> ①
        H.modify_ \s ->
          s { users = Map.insert userName user s.users } ②
  -- BELOW CODE REDACTED
```

① Destructure User to get to the Record we’re calling user.

② Inserting User user into the map with the key being user.userName. Notice we’re Constructing User from the Record, user.

Now, rebuild the app and create a new user to see if it shows up in our list. This time call the user test2 with first and last names as Test. Then return here.

When I do this, it doesn’t work, i.e. our new user isn’t added to the list. It may work for you, but let’s move forward assuming it doesn’t.

Now’s a good time to step back for a moment and think of what’s happening when we click the Create Button.

Let’s look at the code starting at the `Modal` since it’s the button owner. The button click turns into an `Action`. So look to `handleAction` to see what we’re currently doing when we get `AffirmativeClickInternal` then read on.

This is what I find:

```
— ABOVE CODE REDACTED

AffirmativeClickedInternal -> do
    void $ H.tell _inner unit AffirmativeClicked
    H.raise Affirmative

— BELOW CODE REDACTED
```

+   1. First, we query/tell our Inner Component that the button was clicked.
+   2. Second, we let our Parent know the button was clicked.

Now, ask yourself, what happens in the Inner Component when it gets `AffirmativeClicked`. Go look at `Component.Modal.CreateUser`, which is our Inner Component, and see what it does.

When I look, I see that it calls the API on the `server`.

Next, ask yourself, what happens in the Parent when it gets `Affirmative`. Go look at the Users Page to see, i.e. `Component.Users`.

When I look, I see that it clears the `creatingUser` flag:

```
— ABOVE CODE REDACTED

CreateUserModal output -> case output of
    Modal.Affirmative -> H.modify_\_ { creatingUser = false }
    Modal.Negative -> H.modify_\_ { creatingUser = false }
    Modal.InnerOutput user@(User { userName }) -> do
        H.modify_\_ $ s ->
            s { users = Map.insert userName user s.users }

— BELOW CODE REDACTED
```

+   1. Clear `creatingUser` on `Affirmative`.

This will trigger a re-render, which will NOT render the `CreateUser` Modal anymore. This destroys the Modal BEFORE we have a chance to handle the return call from the `server`.

I suspect we have a classic race condition and `CreateUser` is sometimes losing the race. This is why it may be working for you. But it may not ALWAYS work. If the communication between our Application and the server is slow, then there will be no Component to handle the response since the Parent has long since destroyed it by not rendering it.

Let’s prove that’s the case by going to `Component.Modal` and commenting out the line that notifies the

```haskell
-- ABOVE CODE REDACTED
createResponse <- apiCall (CreateUserRequest
  { authToken
  , user:
    { userName
    , password
    , admin
    , firstName
    , lastName
    , temporaryPassword: true
    }
  }) ❶
-- BELOW CODE REDACTED
```

❶ No explicit Type.

So, the compiler has to infer the Type from how we’re using it. Here’s how we’re using it:

```haskell
-- ABOVE CODE REDACTED
case createResponse of
  Left err -> H.modify_ { errorMessage = Just err }
  Right CreateUserResultsSuccess -> do ❶
    H.raise $ PassThroughOutput
      $ User
        { userName
        , admin
        , firstName
        , lastName
        , temporaryPassword: true
        }
  Right (CreateUserResultsFailure { reason }) -> case reason of ❷
    NotAuthorized ->
      errorMsg "You're not authorized to create a new user."
    NotAuthenticated ->
      H.modify_ $ errorMsg "Your session just timed out."
        <<< _ { postModalAction = Just RouteToLogon }
    AlreadyExists ->
      errorMsg "A user with that User Name already exists."
    FileIOError err -> errorMsg
      $ "A fatal error on the Accounts File occurred: "
      <> err
-- BELOW CODE REDACTED
```
