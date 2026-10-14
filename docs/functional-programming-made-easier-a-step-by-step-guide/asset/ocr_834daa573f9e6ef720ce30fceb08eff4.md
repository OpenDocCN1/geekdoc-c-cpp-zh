Functor.

So, after all of that, we make our Main module look like:

```
module Main where

import Prelude

import AppM (runAppM)
import Component.Router as Router
import Data.Maybe (Maybe(..))
import Effect (Effect)
import Effect.Ref as Ref
import Halogen as H
import Halogen.Aff as HA
import Halogen.VDom.Driver (runUI)

main :: Effect Unit
main = do
  userRef <- Ref.new Nothing ①
  HA.runHalogenAff do ②
    body <- HA.awaitBody ③
    let router = H.hoist (runAppM { userRef }) Router.component ④
    runUI router unit body ⑤
```

① Create a userRef of Nothing since no user has logged on yet.

② Run Halogen code with this. Don’t forget this is just runAff with unhandled errors thrown as exceptions.

③ Wait for the body to be rendered by the Browser.

④ Hoist our router, which runs in AppM, to now run in Aff.

⑤ Run our Top-level Component passing Unit as Input. This will go to the initialize Function in the Component that will build the inital State.

Now, the only thing that we’re missing is the initial HTML. Create a file called index.html under the root directory of your project and steal all of the HTML code from the halo Application and paste it here: