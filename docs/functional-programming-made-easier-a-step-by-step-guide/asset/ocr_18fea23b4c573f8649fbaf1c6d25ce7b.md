decrementing its count.

Start by making a Folder under src called Component. Then create a file under Component called Counter.purs.

Let’s start with:

```
module Component.Counter where ①

import Prelude

import Halogen as H
import Halogen.HTML as HH
import Halogen.HTML.CSS as HC
```

① Make sure the module name mirrors the File path from src.

Add this code to your module.

We’re importing some standard modules that nearly all Halogen Components need. Halogen is where general Halogen Functions are, e.g. H.mkComponent to make a Component.

Halogen.HTML is where all of the HTML Functions are to create Virtual DOM Elements, e.g. HH.div, HH.text, HH.button, etc.

Halogen.HTML.CSS is where the CSS style Function is, i.e. HC.style, which let’s you define styles for your Virtual DOM Elements.

Let’s start by adding the component Function. This will create an HH.HTMLComponent, which is a Halogen Component:

```
import Effect.Aff.Class (class MonadAff) ①

component
  :: ∀ m
  . MonadAff m ②
  => H.Component Query Input Output m ③
component = H.mkComponent ④
???
```

① Add this import.

② We’re operating in some Monad m that can operate in Aff. In this application, it’ll be Aff, but it could be your own Monad Stack with Aff at the bottom, i.e. ReaderT Env Aff a.

③ This returns a Halogen Component that renders to HH.HTML. Query, Input and Output are Component-