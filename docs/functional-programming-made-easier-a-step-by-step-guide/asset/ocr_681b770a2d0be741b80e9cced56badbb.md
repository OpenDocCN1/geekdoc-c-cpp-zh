```
```haskell
import Prelude

import Data.Api.CreateUser (CreateUserRequest(..)
                           , CreateUserResponse(..), CreateUserResults(..))
import Handler.Api.Common (handleApi)
import Handler.Class.ApiHandler (class ApiHandler, Handler)
```
```

I've brought in more than I need at the moment in anticipation that we'll need them when we write `handler`.

This one has `Handler`, which is unnecessary at this point, but won't be for long.

Now, we have to tackle the `handler` Function.

But before we do, let's make a plan. Think through the steps that needs to be done to create a user in the system. Write them down if that helps. Then keep reading to see how your list compares with mine.

Here's my list (order matters):

+   - Verify `Session`.
+   - Make sure user is an `admin`.
+   - Create an `Account` from `user` in the `CreateUserRequest` using the `password` to calculate `passwordHash`.
+   - Call `createAccount` in the Account Manager to add it to our in memory accounts.
+   - If the previous call succeeded, then call `createAccount` in the Account Handler to append it to `accounts.csv`.

Well, that seems simple. But why this order?

Because the Account Handler doesn't know if the `Account` exists. It just does the File I/O. By calling the Account Manager first we can avoid writing to `accounts.csv` with a duplicate `userName` since `createAccount` in the Account Manager will give us an error if `userName` is a duplicate.

First, comment out the instance code to remove the compiler error:

```
```haskell
-- instance apiHandlerCreateUser :: ApiHandler CreateUser where
--   handle _ = handleApi handler
```
```

So, code up `handler` by using `Logoff` and even `Logon` for reference. Return here when you're done or if you get stuck.

The first and easiest part is the Type Signature: