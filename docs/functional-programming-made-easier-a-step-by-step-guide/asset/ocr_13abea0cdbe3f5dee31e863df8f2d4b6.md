```
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
                (Slots iQuery iOutput) (Output iOutput) m Unit
  handleAction = case _ of
    Input input -> ???
    Output output -> ???
    AffirmativeClicked -> ???
    NegativeClicked -> ???
```

For Input, i.e. Input from our Parent, we’ll just update our State and let render pass it to the Inner Component in the HH.slot call:

```
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
                (Slots iQuery iOutput) (Output iOutput) m Unit
  handleAction = case _ of
    Input input -> H.modify_ _ { iInput = input }
    Output output -> ???
    AffirmativeClicked -> ???
    NegativeClicked -> ???
```

For Output, i.e. Output from the Inner Component, we’ll just forward it our Parent:

```
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
                (Slots iQuery iOutput) (Output iOutput) m Unit
  handleAction = case _ of
    Input input -> H.modify_ _ { iInput = input }
    Output output -> H.raise $ InnerOutput output ①
    AffirmativeClicked -> ???
    NegativeClicked -> ???
```