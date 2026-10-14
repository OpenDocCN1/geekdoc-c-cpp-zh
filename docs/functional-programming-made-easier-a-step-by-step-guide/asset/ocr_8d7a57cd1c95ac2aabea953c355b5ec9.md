+   ① Added `optional` and `segment` to the import list.
+   ② Added this import.
+   ③ Using `/` to separate Path Segments.
+   ④ Using `optional` combinator since the second path segment is optional.

Now, that you’ve seen how to write a customer Codec for your own Types, I have some bad news. We don’t have a `UserId` for our users. We only have a unique `userName`. That means that we cannot use the code we just wrote.

If this was a real Application, then this is how you would probably do it. But since this is just a learning Application, not having a unique `UserId` is fine.

So, we’re going to have to make the following change to our Route Type:

```
data Route
  = Logon
  | Logoff
  | Users (Maybe String) ①
-- | Users (Maybe UserId)
```

① Changed `UserId` to `String`.

Then change our Codec as follows:

```
routeCodec :: RouteDuplex' Route
routeCodec = root $ sum
  { "Logon": path "logon" noArgs
  , "Logoff": path "logoff" noArgs
  , "Users": "users" / optional segment ①
  -- , "Users": "users" / (optional $ userId segment)
  }
```

① `segment` parses and prints a `String`.

This Router Codec looks complete enough for us to continue building the rest of our Application.

# 30.3. Application Monad

When we wrote our Halogen Application in the previous Chapter, we ran it in `Aff`. But normally, we’re going to want to run our components in a Monad Stack.

And this Application is no different. We’re going to need an Application Monad that we can run our Component Computations in.