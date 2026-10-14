```
type State =
  { userName :: String
  , password :: String
  , admin :: Boolean
  , firstName :: String
  , lastName :: String
  , errorMessage :: Maybe String
  , postModalAction :: Maybe Action ①
  }

-- ABOVE CODE REDACTED
component = H.mkComponent
  { initialState: \_ ->
      { userName: ""
      , password: ""
      , admin: false
      , firstName: ""
      , lastName: ""
      , errorMessage: Nothing
      , postModalAction: Nothing ②
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      }
  }
-- BELOW CODE REDACTED
```

① Added postModalAction. Don’t forget that it’s optional.

② Initialized our new field.

Now, write the code to display an error message in a Modal and setup to route to the Logon Page AFTER the Message Modal is close. Put the code in place of the pure unit where the TODO comment is in the following line of code:

```
loggedOnUser' # maybe (pure unit {- TODO -}) \{ authToken } -> do
```

Return here once completed.

Here are those changes: