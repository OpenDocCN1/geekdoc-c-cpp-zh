Because of this, there’s no way for the compiler to know which version of `handle` to call. You’ll need to fix this flaw when you code this.

Create a folder under `Handler` called `Class` and then create a file under `Handler/Class` called `ApiHandler.purs` and place the code for this Typeclass there.

Then fix the aforementioned problem and get it to compile.

Do that before reading on.

Here’s the full file:

```
module Handler.Class.ApiHandler where

import Data.Either (Either)
import Data.Unit (Unit)
import Foreign (MultipleErrors)
import Type.Proxy (Proxy)

class ApiHandler :: V k. k -> Constraint
class ApiHandler a where
  handle :: String -> Proxy a -> Either MultipleErrors Unit
```

+   1. Take note of the module’s name. See how it mirrors its path in the File System.
+   2. You could also import `Prelude` to get `Unit`.
+   3. We added a `Proxy` Parameter to get the Type Parameter `a` into `handle`’s Type Signature.

Now, return to `Handler.Api.Logon` and make a `Logon` Type and then make that an Instance of `ApiHandler` that decodes the `Request` into a `LogonRequest` and then handles that `Request`. Do this before moving on.

If you got stuck on creating the Type, here it is:

```
data Logon = Logon
```

It doesn’t need to be anymore complicated than that. It just needs a Data Constructor.

If you got stuck on this Type, add it to your code and then finish by writing the `ApiHandler` Instance. Then continue reading.

We’ll code this one line at a time starting with the instance definition: