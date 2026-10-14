```
data CreateUserFailureReason
  = NotAuthorized
  | NotAuthenticated
  | AlreadyExists
derive instance genericCreateUserFailureReason
  :: Generic CreateUserFailureReason _

instance encodeCreateUserFailureReason
  :: Encode CreateUserFailureReason where
  encode = genericEncode defaultOptions

instance decodeCreateUserFailureReason
  :: Decode CreateUserFailureReason where
  decode = genericDecode defaultOptions
```

This module should now compile.

# 28.5. Coding the Server’s Infrastructure

Now that we have our API modeled, some of which we’ve already tested, and we have all the Entities involved in that API, we’re ready to build the plumbing of our server.

This is really the operational part of the server, i.e. it’s infrastructure, e.g. the startup, shutdown, saving and loading accounts, and setting up the API handler.

Let’s look back at our original diagram: