❹ There are no Child Components, hence the empty Row Type.

Next, code the Types for `Query` and `Action` before reading any further.

Here are those Types:

```
import Data.Const (Const) ❶

type Query :: ∀ k. k -> Type
type Query = Const Void ❷

data Action
  = Initialize ❸
  | Tick ❹
```

+   ❶ Add this import.
+   ❷ We have no `Queries`.
+   ❸ The `Initialize` Action will start our timer on.
+   ❹ We’ll emit an `Tick` Action every second until our counter expires, i.e. reaches `0`.

Next, write as much of the `component` Function as you can using `Counter` as an example. Then return here and we’ll move forward together.

First, we’ll write the Type Signature:

```
import Effect.Aff.Class (class MonadAff) ❶
import Halogen as H
import Halogen.HTML as HH

component
  :: ∀ m
   . MonadAff m
  => H.Component Query Input Output m
component = ???
```

+   ❶ Added these imports.

Now, we’ll call `H.mkComponent`: