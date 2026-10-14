
![](img/8c0e9b687c62642e828ccb5481e11313_1810_0.png)

The last thing we need to do on this page is to Create a new User. But to do that, we’re going to need a Modal Dialog Box first.

## 30.12. Modal Dialog Component

We’re going to build a Modal Dialog Component called Modal. It will work similar to our Page Component in that it’ll have an Inner Component. The Inner Component can be anything, e.g. a Form like we’ll need for the Create User Modal or just Text as we’ll need for our error Dialogs that will replace the use of alertError.

Let’s start with a design:

![](img/8c0e9b687c62642e828ccb5481e11313_1810_1.png)

Input from the Parent to the Modal Component will be passed directly to the Inner Component. And Output from the Inner Component will be passed directly to the Parent.

The Modal Component will have 2 buttons with default labels OK and CANCEL, which will produce the Outputs Affirmative and Negative respectively. We’ll allow some configuration on our Modal Component, i.e. re-labeling the buttons and disabling the Cancel Button.

This is going to be pretty complicated compared to other Components that we’ve done so far, and more complicated than the average Component. Because of that, we’ll code the Modal Component and the Message Component together. This should be enough experience to allow you to code the Create User Modal on your own.

Let’s start by creating a File under src/Component called Modal.purs with the following:

```
module Component.Modal where

import Prelude

import Effect.Aff.Class (class MonadAff)
import Halogen as H ①
import Halogen.HTML as HH
import Halogen.HTML.CSS as HC
import Halogen.HTML.Events as HE

type State iInput = { iInput :: iInput } ②
```

① We’ll need these Halogen imports eventually.

② Our State is similar to Page’s for all the same reasons. We need to save the Input in the State so we can pass it to the Inner Component in render as one of the HH.slot Parameters.

Consulting our design diagram, it’s clear that there are 3 Outputs, so we’ll define those:

```
data Output iOutput ①
  = Affirmative
  | Negative
  | InnerOutput iOutput ②
```

① iOutput is the Type for the Inner Component’s Output.

② InnerOutput wraps the Inner Component’s Output in our Output.

Affirmative and Negative are to let our Parent know that the buttons have been clicked.

Returning again to our diagram, we can see that there are 4 Actions, one for each arrow:

```
data Action iInput iOutput
  = Input iInput ①
  | Output iOutput ②
  | AffirmativeClicked ③
  | NegativeClicked ③
```

① Input from Parent.

+   2. **Output** from Inner Component.

+   3. Button clicks.

We’re reacting to **Input** from the Parent, **Output** from the Inner Component and the user clicking on buttons.

Next, we define the Child Slots Type and Symbol Proxies for the labels:

```
import Type.Proxy (Proxy(..))

type Slots iQuery iOutput = ( inner :: H.Slot iQuery iOutput Unit )

_inner = Proxy :: Proxy "inner"
```

+   1. Added this import.

This code is like what we did for the Page Component.

And now we’re ready to code the **component** creation Function. We’ll start with the Type Signature:

```
component
  :: ∀ iQuery iInput iOutput m
   . MonadAff m
  => H.Component iQuery iInput iOutput m
  => H.Component iQuery iInput (Output iOutput) m
```

+   1. We always need this when we run in a Monad that eventually runs in `Aff`.

+   2. The Inner Component.

+   3. Notice how our `Query` and `Input` Type Parameters are exactly the same Type as our Inner Component’s. That’s why we didn’t define them in this module.

And now, we call `H.mkComponent` to make the Component:

```
```haskell
component
  :: ∀ iQuery iInput iOutput m
  => MonadAff m
  => H.Component iQuery iInput iOutput m
  => H.Component iQuery iInput (Output iOutput) m
component innerComponent = H.mkComponent
  { initialState: \iInput -> { iInput } ❶
  , render
  , eval: H.mkEval $ H.defaultEval
      { handleAction = handleAction ❷
      , handleQuery = handleQuery ❸
      , receive = Just <<< Input ❹
      }
  }
  where
  ???
```
```

+   ❶ We initialize our `State` with the `Input` from the Parent.
+   
+   ❷ We’re going to need to handle our `Actions`.
+   
+   ❸ Queries will simply be forwarded to the Inner Component like we did in the Page Component.
+   
+   ❹ We will handle Input from the Parent the same way we did in the Page Component, i.e. Inputs are passed to the Inner Component by `render`, which were put into the `State` by `handleAction`.

Now, we ready to write `handleAction`’s Type Signature:

```
```haskell
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
          (Slots iQuery iOutput) (Output iOutput) m Unit ❶
```
```

❶ This Type differs only slightly from what we did in the Page Component. In `Page`, our Output was the SAME as our Inner Component. In `Modal`, we have our OWN `Output` so we define the Output as `Output iOutput`, whereas `Page` defined it as just `iOutput`.

Next, we’ll write the boilerplate part of `handleAction`:

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

❶ We wrap `output` in `InnerOutput` since we have other `Outputs`.

For `AffirmativeClicked` and `NegativeClicked`, we will Output `Affirmative` and `Negative` respectively:

```
```haskell
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
                  (Slots iQuery iOutput) (Output iOutput) m Unit
  handleAction = case _ of
    Input input -> H.modify_ _ { iInput = input }
    Output output -> H.raise $ InnerOutput output
    AffirmativeClicked -> H.raise Affirmative
    NegativeClicked -> H.raise Negative
```
```

For `handleQuery`, we’ll just steal it from `Component.Page` since they both just forward the Query:

```
```haskell
import Data.Maybe (Maybe) ❶

-- ABOVE CODE REDACTED
handleQuery
  :: ∀ a
   . iQuery a
  -> H.HalogenM (State iInput) (Action iInput iOutput)
                (Slots iQuery iOutput) (Output iOutput) m (Maybe a) ❷
handleQuery = H.query _inner unit
```
```

+   ❶ Added this import.
+   
+   ❷ Once again, the Output Type differs from the Page Components in the exact same way.

And now, for the `render` Function. There is nothing difficult here if you’ve done HTML and CSS before. So, I’m going to just give you the whole thing. As you type it in, take time to note what’s being done:

```
```purescript
import Prelude hiding (top) ❶

import AppTheme (paperColor, themeColor, themeFont)
import CSS.Background (backgroundColor)
import CSS.Color (rgba, white)
import CSS.Common (center)
import CSS.Display (display, position, fixed, zIndex, flex)
```
```
