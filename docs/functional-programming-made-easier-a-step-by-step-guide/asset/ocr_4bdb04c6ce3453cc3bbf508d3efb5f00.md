```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { }
  , render
  , eval: H.mkEval H.defaultEval
  }
```

Can you see what we’re missing?

We are using all of the defaults. We need to override them so we can add handleAction. Make that change to add ONLY handleAction using what we did in halo or in Component.Page as a example.

Return back here when you’re finished coding.

Here is that change:

```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction -- COMPILER ERROR!!
      }
  }
```

No, surprise at the compiler error since we haven’t written handleAction yet. We’ll do that soon enough, but for now, we need to add the Value of the Username and Password fields into our State so that we can keep track of their values as they change.

Then when the user clicks on the Logon Button, we’ll have them at the ready and can use them to call our backend server.

Update State to include this information and then continue reading once you’re done.

Here is that change: