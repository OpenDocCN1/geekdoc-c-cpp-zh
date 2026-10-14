```
```haskell
data Action
  = Logon
  | Input (State -> State) ①
  | Modal (Modal.Output Message.Output)
```
```

① This `Action` looks like it handles inputs.

Let’s checkout `handleAction` from `Logon` to see how `Input` works:

```
```haskell
handleAction
  :: Action
  -> H.HalogenM State Action Slots (InnerOutput Output) m Unit
handleAction = case _ of
  Input f -> H.modify_ f
-- BELOW CODE REDACTED
```
```

Well, that doesn’t look like it’s doing anything special. Where else should we look in `Logon` to see where the button enabling/disabling happens?

The `render` Function has to do that. So look there to see if you can find out how we’re handling it and return here when you’ve found it.

Here’s what I find at the very bottom of `render` in `Logon`:

```
```haskell
where logonDisabled = trim userName == "" || trim password == ""
```
```

Okay, so this will work for us in our `CreateUser` Component. But what about `Input`?

How and where is it used in `Logon`? Take a look and see what you find.

It’s used in `render` for `userName`: