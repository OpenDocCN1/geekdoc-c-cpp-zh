```
component
  :: ∀ m
    . MonadAff m
  => MonadAsk Env m
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> ①
      { authorized: false
      , selectedUser: Nothing
      , users: []
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , receive = Just <<< SelectedUserName ②
      , initialize = Just Initialize
      }
  }
```

① We’re currently throwing away the Input we get initially since we have no users. We’ll need to fix this.

② Input from our Parent produces the Action, SeletedUserName.

Notice that initialState isn’t using the userName that it gets from its Parent, i.e. the Router Component.

We cannot look up the user here since we don’t have any users yet since we haven’t called the backend yet to get them.

We’ll need to store this Value in the State so when we do get the users from our server API, we can then select the current user, if there is one.

Make that change to the code to simply store the initial username calling our new field initUserName before reading on.

Here’s that change: