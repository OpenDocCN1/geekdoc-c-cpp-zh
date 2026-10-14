
Now, we can make our Config use ButtonDisplay:

```
type Config =
  { affirmativeLabel :: String
  , negativeLabel :: String
  , displayButtons :: ButtonDisplay
  }
```

Make sure your definition matches this one.

Now, we’re going to need to create a Type that specifies the Type of Output that the Inner Component can make.

Currently, all Output from the Inner Component will pass-through to the Parent, but now some Output will be processed by Modal.

We’ll start our definition with the pass-through case:

```
data InnerOutput iOutput
  = PassThrough iOutput
```

And now, we’d like a way for the Inner Component to enable and disable buttons as per requirement 3:

```
data InnerOutput iOutput
  = PassThrough iOutput
  | EnableAffirmative
  | DisableAffirmative
  | EnableNegative
  | DisableNegative
```

And if both buttons are hidden, we’ll need some way to close the Modal. Since Modal sends either Affirmative or Negative to the Parent, we’ll want to maintain that behavior. So, we’ll allow the Inner Component to dictate that as part of the close:

```
```purescript
data InnerOutput iOutput
  = PassThrough iOutput
  | EnableAffirmative
  | DisableAffirmative
  | EnableNegative
  | DisableNegative
  | CloseAffirmative
  | CloseNegative
```
```

Add this to the Modal code.

Next, create a `defaultConfig` for `Config` that maintains our current Modal behavior and then return here.

Here’s that:

```
```purescript
defaultConfig :: Config
defaultConfig =
  { affirmativeLabel: "OK"
  , negativeLabel: "CANCEL"
  , displayButtons: DisplayBothButtons
  }
```
```

Now change component to use `Config`. And change render to abide by the configuration Parameters.

Make that changes and then return here and continue reading.

Here’s the change to component:

```
```purescript
component
  :: ∀ iQuery iInput iOutput m
   . MonadAff m
  => Config ❶
  -> H.Component iQuery iInput iOutput m ❷
  -> H.Component iQuery iInput (Output iOutput) m
component config innerComponent = H.mkComponent ❸
-- BELOW CODE REDACTED
```
```

+   ❶ Added `Config` to Type Signature.
+   
+   ❷ Changed `=>` to `->`.
+   
+   ❸ Added `config` Parameter.

And now, we’ll make the following changes to render. First, destructuring config:

```
render
  :: State iInput
  -> H.ComponentHTML (Action iInput iOutput) (Slots iQuery iOutput) m
render { iInput } =
  let { affirmativeLabel
      , negativeLabel
      , displayButtons
      } = config in ①
    HH.div [
-- BELOW CODE REDACTED
```

① Destructure config to get all of the fields into Variables. We could’ve destructured in component instead of defining the config Parameter.

And then we’ll decide which buttons to display:

```
render
  :: State iInput
  -> H.ComponentHTML (Action iInput iOutput) (Slots iQuery iOutput) m
render { iInput } =
  let { affirmativeLabel
      , negativeLabel
      , displayButtons
      } = config
    displayAffirmative = case displayButtons of ①
      DisplayAffirmative -> true
      DisplayBothButtons -> true
      _ -> false
    displayNegative = case displayButtons of ②
      DisplayNegative -> true
      DisplayBothButtons -> true
      _ -> false in
-- BELOW CODE REDACTED
```

① Decide whethere to display the Affirmative button or not.

② Decide whethere to display the Negative button or not.

Now, change the rest of the rendering code to abide by the configuration before reading further.

Here’s that change:

```
```haskell
[ if not displayAffirmative then HH.text "" else ❶
    HH.button [
        buttonStyle
      , HE.onClick $ const AffirmativeClicked
      ] [ HH.text affirmativeLabel ] ❷
  , if not displayNegative then HH.text "" else ❶
    HH.button [
        buttonStyle
      , HE.onClick $ const NegativeClicked
      ] [ HH.text negativeLabel ] ❷
  ]
]
where
  buttonStyle = HC.style do
```
```

+   ❶ Insert empty Text Node when NOT displayed.
+   
+   ❷ Use the configuration labels.

Now, rebuild the Application:

```
```text
make build
```
```

You should get 2 compiler errors. If you’re in VSCode and are using the Terminal Pane, you can `Option-click` the File and Line number link in the Terminal Pane, or `Alt-click` on Windows, and the editor will jump to the line with the error.

Fix the errors and once you’re program is compiling, return here.

Here are those fixes. First, one in `Component.Logon`:

```
```haskell
, (errorMessage # maybe (HH.text "") \message ->
    HH.slot _modal unit
      (Modal.Component Modal.defaultConfig Message.component) ❶
      message Modal)
]
where logonDisabled = trim userName == "" || trim password == ""
```
```

+   ❶ Added `defaultConfig`.

And the same change is made in Component.Users:

```
-- ABOVE CODE REDACTED
, (errorMessage # maybe (HH.text "") \message ->
  HH.slot _modal unit
    (Modal.component Modal.defaultConfig Message.component) ①
    message Modal)
]
```

① Added defaultConfig.

Now when you rebuild, it should build but you will get the following warning:

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- web-html
```

Remove this from our spago.dhall file before we forget.

Now refresh your Browser, then try to logon with invalid credentials to see if our Modal Component still works.

When I tried, the Modal still works. Thanks good. That means that we didn’t break it.

Next, let’s do a little housekeeping. First, create a Folder under src/Component called Modal. We’re going to put all of our Inner Components for Modal here.

Then move Message.purs from src/Component to src/Component/Modal.

Change the module name in Message.purs to Component.Modal.Message.

Then change the imports of Message.purs in both Component.Logon and Component.Users.

Then just to make sure we got everything:

```
make build
```

Next, change both Logon and Users to only display the OK button. Instead of duplicating the code in both places, make a configuration called errorConfig and put it in a File called Common.purs under the src/Component/Modal.

Then return here when you’re ready to move on.

First, here’s the code in Component.Modal.Common:

```
module Component.Modal.Common where

import Component.Modal (Config, ButtonDisplay(..), defaultConfig)

errorConfig :: Config
errorConfig = defaultConfig { displayButtons = DisplayAffirmative }
```

Here’s the change in Logon:

```
import Component.Modal.Common as ModalCommon ①

-- ABOVE CODE REDACTED
    , (errorMessage # maybe (HH.text "") \message ->
        HH.slot _modal unit
            (Modal.component ModalCommon.errorConfig Message.component) ②
            message Modal)
    ]
    where logonDisabled = trim userName == "" || trim password == ""
```

① Added this import.

② Use errorConfig.

And the change in Users:

```
import Component.Modal.Common as ModalCommon ①

-- ABOVE CODE REDACTED
    , (errorMessage # maybe (HH.text "") \message ->
        HH.slot _modal unit
            (Modal.component ModalCommon.errorConfig Message.component) ②
            message Modal)
    ]
```

① Added this import.

② Use errorConfig.

Now, test your code by rebuilding, refreshing the browser and trying an invalid logon.

When I do this, only the OK button is displayed.

All that’s left to do is finish implementing `InnerOutput`. Currently, `Modal` expects the Inner Component’s Output to be of Type `iOutput`, i.e. any Type. We’ll need to change `Component.Modal` to expect `InnerOutput` instead.

First, we have to change the Child Slot Type:

```
type Slots iQuery iOutput =
  ( inner :: H.Slot iQuery (InnerOutput iOutput) Unit )
```

❶ Changed `iOutput` to `InnerOutput iOutput`.

And then we’ll change `Action`:

```
data Action iInput iOutput
  = Input iInput
  | Output (InnerOutput iOutput)
  | AffirmativeClicked
  | NegativeClicked
```

❶ The Type we get as an `Output` from the Inner Component is now of Type `InnerOutput iOutput`. It used to be just `iOutput`.

Next, we have to change the Type of the Component we pass for the Inner Component to `component` to have `InnerOutput` as its Output Type:

```
component
  :: ∀ iQuery iInput iOutput m
   . MonadAff m
  => Config
  -> H.Component iQuery iInput (InnerOutput iOutput) m
  -> H.Component iQuery iInput (Output iOutput) m
```

❶ Changed Output Type.

Now, we have to fix `handleAction` to deal with all the cases of `InnerOutput`:
