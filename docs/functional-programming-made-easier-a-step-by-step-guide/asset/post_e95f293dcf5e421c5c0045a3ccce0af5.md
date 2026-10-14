
be good for us to see how to develop such a Component and how it will interact with our Page.

Now that we have a plan we’re ready to complete the Logon Page.

The next thing we’ll need to do to is keep track of the data in the fields in our State so that we have the values once the user clicks the Logon Button.

This is normally done with onChange, which is fired when the user exits a field and that field has been modified. But we’re going to want to check on every change. For that, we’re going to want to use onValueInput.

Add an Action called Input and then add onValueInput from Halogen.HTML.Events to both the Username and Password fields to trigger that new Action. Use the code for HE.onClick in this file as reference along with Pursuit.

Return here when you’re ready to move on.

Here are those changes:

```
data Action
= Logon
  | Input String ①

-- ABOVE CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Username: " ]
    , HH.input [
        HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Password: " ]
    , HH.input [
        HP.type_ InputPassword
    , HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- BELOW CODE REDACTED
```

① Added Input Data Constructor. The String Parameter is given to us by onValueInput.

② Added the Event Handler for both fields.

Note that onValueInput takes a Function of Type String -> Maybe a. This allows for us to reject the input in the render logic. We could also reject it handleAction.

Let’s look at our component creation code:

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

```
type State =
  { userName :: String
  , password :: String
  }
```

Next, update initialState to initialize these Values to an empty String then return here.

Here’s that change:

```
component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { userName: "", password: "" }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction -- COMPILER ERROR!!
      }
  }
```

Now write handleAction to maintain these newly added Values to State, but stub out the Logon Action for now. When you’re finished, continue on.

Here’s handleAction:

```
-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input value -> ???
  Logon -> pure unit
```

I only got this far and then I realized that there’s no way to know which field to update.

There are 2 ways to solve this that come to mind. First, we create a UsernameInput and a PasswordInput. But this approach doesn’t scale well. Imagine a large form that has dozens and dozens of fields. We’d have to have a bunch of boilerplate in our Action Type, for example:

```
data Action
  = Field1Input
  | Field2Input
  | Field3Input
  | Field4Input
  | Field5Input
  | Field6Input
  | Field7Input
  | Field8Input
```

The other approach is to pass a Function to update the field in State. Then we can write pretty generic handling code and only require a single Data Constructor.

Comment out the following lines so we can get compiler errors that are useful as we add code:

```
, eval: H.mkEval H.defaultEval
    -- { handleAction = handleAction
    -- }
-- CODE REDACTED
where
  -- handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
  -- handleAction = case _ of
  --   Input value ->
  --   Logon -> pure unit
```

Now, change the Input Data Constructor to take a Parameter that’s a Function which updates State for the field in question. Return here once that’s done.

Here’s that change:

```
data Action
  = Logon
  | Input (State -> State) ①
```

① We will pass the input String and the current State and produce a new State with the appropriate field updated. Notice how the String Parameter is BEFORE the first Parameter. That’s because we want to Partially Apply this Function with the input String leaving us a Function that will modify our State, i.e. State -> State.

Now, change the 2 places we call HE.onValueInput to add this new Parameter to Input. Once you’re done, continue on.

Here’s that change:

```
-- ABOVE CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Username: " ]
    , HH.input [
        HE.onValueInput
            $ Input <<< \s -> _ { userName = s } ① ②
        , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Password: " ]
    , HH.input [
        HP.type_ InputPassword
        , HE.onValueInput
            $ Input <<< \s -> _ { password = s } ① ③
        , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
-- BELOW CODE REDACTED
```

① I wrote the Type Signature for Input to be String -> State -> State so I could code these Functions using a wildcard for the State.

② Update userName.

③ Update password.

This should compile.

Now, uncomment:

```
component = H.mkComponent
  { initialState: \_ -> { userName: "", password: "" }
  , render
  , eval: H.mkEval H.defaultEval
    -- { handleAction = handleAction ①
    -- }
  }
```

① Uncomment these lines.

And then uncomment and finish handleAction. Return here when you’re ready to move forward.

Here’s the completed handleAction:

```
-- ABOVE CODE REDACTED
  where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f ①
  Logon -> pure unit
```

① H.modify_ will update our State. It calls a Function of Type State -> State.

Now modify render to disable the Logon Button if and only if either userName or password are empty. Search Pursuit for disabled. There will be many, but we want the Halogen version. Keep in mind that we’re looking for a way to set the Properties of the button.

Continue reading once you’ve finished.

Here is the first part of the change to render:

```
render :: State -> H.ComponentHTML Action Slots m
render { userName, password } = ①
-- BELOW CODE REDACTED
```

① Destructure State to get userName and password.

And here’s the other change to render:
