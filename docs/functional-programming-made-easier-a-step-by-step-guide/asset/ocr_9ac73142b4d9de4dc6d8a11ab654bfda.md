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