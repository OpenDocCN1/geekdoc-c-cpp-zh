```
-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize ->
    H.subscribe' \sid -> EventSource.affEventSource \emitter -> do
      fiber <- forkAff $ forever do
        delay $ Milliseconds 1000.0
        EventSource.emit emitter (Tick sid)
    ???
  Tick sid -> pure unit ①
```

① Added SubscriptionId Parameter called sid.

Next, we need to save fiber to our State so we can kill it on Finalize or when the counter reaches 0:

```
-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
    tickSubscription <- HQ.subscribe tickEmitter
    tickFiber <- H.liftAff $ forkAff $ forever do
      delay $ Milliseconds 1000.0
      H.liftEffect $ HS.notify tickListener $ Tick tickSubscription
    H.modify_ _ { tickFiber' = Just tickFiber } ①
  Tick sid -> pure unit
```

① Save tickFiber' in State so we can stop it later with killFiber.

We now need to add tickFiber' to our State: