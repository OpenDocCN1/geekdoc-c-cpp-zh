```
type Request =
  { method :: Method.Method
  , path :: Path.Path
  , query :: Query.Query
  , headers :: Headers.Headers
  , body :: String
  , httpVersion :: Version.Version
  }
```

Routers have the following Type Signature:

```
router :: Request -> ResponseM
```

Since `router` is just a normal Function, we can use Guards or Pattern Matching to handle different requests.

Replace your `router` with the following:

```
router :: Request -> ResponseM
router { path: [ "hello" ] }  = HTTPure.ok "hello" ❶
router { path: [ "goodbye" ] } = HTTPure.ok "goodbye" ❷
router _                       = HTTPure.notFound ❸
```

+   1. This Pattern Matches the `path` of the URL for `hello`, e.g. `localhost:3000/hello`.
+   2. This also Pattern Matches the `path`, but for `goodbye`.
+   3. All other cases are a Not Found error, i.e. `404`.

Next, the following change your `main`:

```
import HTTPure.Server (ServerM) ❶

main :: ServerM ❷
main = HTTPure.serve port router
  $ log $ "Server up running on port: " <> show port
```

+   1. Added this import.
+   2. Replace `main` with this.

Then remove the following imports: