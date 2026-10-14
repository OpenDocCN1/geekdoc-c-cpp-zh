```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \i -> { count: i }
  , render
  , eval: H.mkEval H.defaultEval {
      initialize = Just Initialize
    , handleAction = handleAction -- COMPILER ERROR!!
    }
  }
where
render :: State -> H.ComponentHTML Action Slots m
render _ = HH.text ""
```

Now, write a stub for handleAction to eliminate our new error. Don’t forget to steal the Type Signature from handleAction in Counter. Then return back here.

Here is the stub for handleAction:

```
-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> pure unit
  Tick -> pure unit

render :: State -> H.ComponentHTML Action Slots m ①
render _ = HH.text ""
```

① I like to have render at the bottom of my where since it’s typically verbose. This way I don’t have to scroll past a bunch of render code just to change handleAction or handleQuery.

Now that we have the skeleton of our Component done, it’s time to flesh out the rest (pun intended).

We’ll start with creating the Emitter and Listener. We’ll code this together since it’s new: