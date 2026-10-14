Rename it to PassThroughOutput so there’s no ambiguity and then fix the compiler errors that this change caused before returning here.

Here are the changes:

```
data InnerOutput iOutput
  = PassThroughOutput iOutput ①
  | EnableAffirmative
  | DisableAffirmative
  | EnableNegative
  | DisableNegative
  | CloseAffirmative
  | CloseNegative

handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output innerOutput -> case innerOutput of
    PassThroughOutput output -> H.raise $ InnerOutput output ①
-- BELOW CODE REDACTED
```

① Added Output suffix.

We’re going to have to change iQuery to InnerQuery iQuery in component just like we did with InnerOutput:

```
component
  :: ∀ iQuery iInput iOutput m
    . MonadAff m
  => Config
  -> H.Component (InnerQuery iQuery) iInput (InnerOutput iOutput) m ①
  -> H.Component (InnerQuery iQuery) iInput (Output iOutput) m ②
```

① This change is for the same reason we did with InnerOutput.

② Added InnerQuery here also.

You may be wondering why the return Type for component uses Output iOutput Instead of InnerOutput iOutput. This is because Modal has its own Output but not its own Query, which is why the return Type uses InnerQuery.

We are also expecting the Inner Component’s Query to be InnerQuery, so we’ll need to change our Slot