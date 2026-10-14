```
component
  :: ∀ m route
    . MonadAff m
  => MonadAsk Env m
  => Navigate m route
  => LogonRoute m route
  => Log m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ ->
    { userName: ""
    , password: ""
    , errorMessage: Nothing ①
    }
  , render
  , eval: H.mkEval H.defaultEval
    { handleAction = handleAction
    }
  }
where
-- BELOW CODE REDACTED
```

① Initialize to NO error. The Modal will not be displayed by our render Function if this is Nothing.

Now, we’ll simply set the errorMessage in the State when an error occurs. This will trigger a re-render and our render Function will see that errorMessage is NOT Nothing and display the Modal.

Here are the changes to handleAction: