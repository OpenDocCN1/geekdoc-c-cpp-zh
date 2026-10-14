defintion:

```
type Slots iQuery iOutput =
  ( inner :: H.Slot (InnerQuery iQuery) (InnerOutput iOutput) Unit ) ①
```

① Changed iQuery to InnerQuery iQuery.

And we’ll need to handle this InnerQuery, so handleQuery will change:

```
handleQuery
  :: ∀ a
  . (InnerQuery iQuery) a ①
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m (Maybe a)
  handleQuery = H.query _inner unit
```

① We get an InnerQuery now, whereas, we used to get iQuery.

Now we need to Query the Inner Commponent to let it know that the buttons have been clicked:

```
handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m Unit
  handleAction = case _ of
  -- CODE REDACTED
    AffirmativeClickedInternal -> do
      void $ H.tell _inner unit AffirmativeClicked ①
      H.raise Affirmative
    NegativeClickedInternal -> do
      void $ H.tell _inner unit NegativeClicked ①
      H.raise Negative
```

① Let Inner Component know about button clicks just like we let the Parent know on the next line.

When the Inner Component programatically clicks the buttons using CloseAffirmative or CloseNegative, the Modal will inform it that the button has been clicked, which, in this case, is redundant. In this scenario, the Inner Component can just ignore these Queries.

Now, we’re going to need to change both of our Inner Components to support this new Query Type, i.e. InnerQuery.

We’re going to start with Component.Modal.Message. Here’s the current Type: