
```haskell
import Prelude

import Data.Api.CreateUser (CreateUserRequest(..)
                           , CreateUserResponse(..), CreateUserResults(..))
import Handler.Api.Common (handleApi)
import Handler.Class.ApiHandler (class ApiHandler, Handler)
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

```
```haskell
handler :: CreateUserRequest -> Handler
```
```

Next, easiest part is the left-hand side of the equal sign:

```
```haskell
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = ???
```
```

Notice the destructuring. This is to make our code easier to read.

We should start with a do block since we’re running under the Monad Stack of Handler:

```
```haskell
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
  ???
```
```

The very first thing we must do is to validate the credentials of the caller. Here’s `verifySession`’s Type Signature to help us:

```
```haskell
verifySession :: AV ar Sessions -> UUID -> Aff (Maybe Session)
```
```

We can see that it runs in `Aff` which is at the bottom of the Handler Monad Stack which means that it’ll need a `lift`.

It will also need `sessionsAVar`.

Let’s do both of those steps

```
```haskell
import Control.Monad.Reader.Class (ask)
import Control.Monad.Trans.Class (lift)
import Manager.Session (verifySession)

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
  { sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  ???
```
```

❶ Add these imports.

❷ Get the `sessionsAVar`.

❸ Verify the session.

Next, we'll handle the 2 cases of verifiedSession. We'll start with the failure case:

```
import Data.Maybe (Maybe(..)) ①

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
    { sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of ②
        Nothing -> ???
        ???
```

① Import Maybe and its Data Constructors.

② This case expression will evaluate to a response like we've done in other handlers.

At this point, we'll want to look at CreateUserResponse and its related Types to see what to return:

```
data CreateUserFailureReason
    = NotAuthorized
    | NotAuthenticated
    | AlreadyExists
    | FileIOError String

data CreateUserResults
    = CreateUserResultsSuccess
    | CreateUserResultsFailure { reason :: CreateUserFailureReason }

newtype CreateUserResponse = CreateUserResponse CreateUserResults
```

Take a look at this to see what the response should be. Then read on.

Here's the response for the error case:

```
import Data.Api.CreateUser (CreateUserRequest(..)
    , CreateUserResponse(..), CreateUserResults(..)
    , CreateUserFailureReason(..)) ①

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
    { sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> CreateUserResponse
            $ CreateUserResultsFailure { reason: NotAuthenticated }
        ???
```

① Added CreateUserFailureReason to import list.

Next, we’ll deal with the success case:

```
import Entity.Session (Session(..)) ①

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
    { sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> CreateUserResponse
            $ CreateUserResultsFailure { reason: NotAuthenticated }
        Just (Session { userName }) -> ??? ② ③
```

① Import Session and its Data Constructors for Pattern Matching.

② verifySession returns the Session of the requestor but we’re only concerned with userName to check for the NotAuthorized case, i.e. the user making this request is NOT an admin.

③ We destructure the Session to gain access to userName.

Next, we should check to make sure the user is an admin. But we’re going to have to write a Function called findAccount first. We’re going to switch to the Account Manager, i.e. Manager.Account, and write findAccount there.

Write just the Type Signature before reading further.

Since accounts is stored in an AVar, we’ll need to pass AVar Accounts to findAccount. We’ll also have to pass the userName:

```
```haskell
findAccount :: AVar Accounts -> String -> Aff (Maybe Account)
findAccount accountsAVar userName =
  AVar.read accountsAVar >>= pure <<< Map.lookup userName
```
```

This version eliminates the accounts Variable and is easier to read.

Now, we can use this in our handler code:

```
```haskell
import Data.Maybe (Maybe(..), maybe)
import Entity.Account (Account(..))
import Manager.Account (findAccount)

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user }) = do
  { sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  response <- case verifiedSession of
    Nothing -> CreateUserResponse
      $ CreateUserResultsFailure { reason: NotAuthenticated }
    Just (Session { userName }) -> do
      admin <- lift $ findAccount accountsAVar userName
        <#> maybe false (\\(Account a) -> a.admin)
      if not admin then CreateUserResponse
        $ CreateUserResultsFailure { reason: NotAuthorized }
      else
        ???
```
```

+   1. Added maybe to the import list.
+   2. Add these imports.
+   3. `lift` the call to `findAccount` since it runs in `Aff`.
+   4. Use maybe to turn the not-found case into `false`.
+   5. If found then make sure the Account is an admin account, i.e. admin is true. Notice that we’re destructuring the Record to get at admin. In this case, this approach is more terse.
+   6. Response is NotAuthorized if this request is from a non-admin account.

This is probably the first usage of maybe that we’ve come across. Here’s its Type Signature:

```
```haskell
maybe :: ∀ a b. b -> (a -> b) -> Maybe a -> b
```
```

maybe takes a default Value for the Nothing, i.e. b, case and then a Function for the Just case. Notice that

```
```haskell
module Crypto where

import Prelude

import Data.Char (toCharCode)
import Data.Foldable (foldl)
import Data.String.CodeUnits (toCharArray, fromCharArray)
import Effect.Aff (Aff)
import Random.LCG (Seed, mkSeed)
import Test.QuickCheck.Arbitrary (arbitrary)
import Test.QuickCheck.Gen (sample)
import Data.String.CodePoints (length)
import Node.Crypto.Hash (Algorithm(..), hex)
import Effect.Class (liftEffect)

userNameSeed :: String -> Seed
userNameSeed userName =
  userName
    # toCharArray
    <#> toCharCode
    # foldl (*) 1
    # mkSeed

userNameSalt :: Int -> String -> String
userNameSalt saltLength userName =
  fromCharArray
    $ sample (userNameSeed userName) saltLength arbitrary

passwordHashHex :: String -> String -> Aff String
passwordHashHex userName password =
  let salt = userNameSalt (3 * length userName) userName in
  liftEffect $ hex SHA512 (password <> salt)
```
```

Once that compiles, delete the functions in `Handler.Account` that got moved and import `passwordHashHex` from `Crypto` so it’ll compile again.

Then you’ll wind up with a boatload of warning for redundant imports. So, clean those up.

Once you’ve done that refactor, continue reading.

Now, return back to `handler` in `Manager.Account`.

Import `passwordHashHex` from `Crypto` and remove the old import of `passwordHashHex` from `Handler.Account`.
