complicated than the average Component. Because of that, we’ll code the Modal Component and the Message Component together. This should be enough experience to allow you to code the Create User Modal on your own.

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