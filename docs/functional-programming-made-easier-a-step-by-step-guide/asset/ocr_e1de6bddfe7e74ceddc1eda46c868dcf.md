Looks like milliseconds from the Epoch will work just fine. So, it’ll be a `Number`:

```
newtype Session = Session
  { authToken :: UUID
  , userName :: String
  , lastTime :: Number
  }
```

One thing to note here is that `userName` may seem a bit our of place here, but it’s in here so we can cross reference a `Session` with its corresponding `Account`, since `Accounts` have unique `userNames`. We’re going to need this to check if the user of a particular `Session` is an `admin` or not since `admin` is stored in `Account`.

And now we can return to `Manager.Session` and fix the compiler error on `shutdown`:

```
shutdown :: AVar Accounts -> Aff Unit --- COMPILER ERROR!
shutdown = void <<< AVar.take
```

First, add a Type Alias for `Sessions` using `Accounts` in `Manager.Account` as an example. Then replace `Accounts` with `Sessions` in `shutdown’s` Type Signature in `Manager.Session`. Do this and then return here.

Here are those changes:

```
import Data.Map (Map) ❶
import Data.UUID (UUID)
import Entity.Session (Session)

type Sessions = Map UUID Session ❷

shutdown :: AVar Sessions -> Aff Unit ❸
shutdown = void <<< AVar.take
```

+   ❶ Added these imports.
+   ❷ Added this definition.
+   ❸ Changed `Accounts` to `Sessions`.

Next, write `startup` for the Session Manager before continuing to read.

It’s Type Signature is analogous to Account Manager’s except that it doesn’t start off with any existing `Sessions`. Granted, we could save out Sessions in a File upon a clean shutdown of the server and then read them in upon startup, but we’re not going to in this design.