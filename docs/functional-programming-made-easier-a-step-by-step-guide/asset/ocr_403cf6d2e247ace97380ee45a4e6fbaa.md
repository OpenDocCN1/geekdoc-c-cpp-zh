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
    Input input -> H.modify_ { iInput = input }
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