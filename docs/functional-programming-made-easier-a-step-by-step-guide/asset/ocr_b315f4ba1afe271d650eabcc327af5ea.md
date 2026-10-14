And finally, let’s look at an HTTPure.Request:

```
type Request =
  { method :: Method.Method
  , path :: Path.Path
  , query :: Query.Query
  , headers :: Headers.Headers
  , body :: String ①
  , httpVersion :: Version.Version
  }
```

① Our API JSON will be in the body. This is the String each Handler will process.

Study these pieces of information before you begin adding code to router in the Main module. Then add a bit of code to use oneOf and get a Handler into a Variable called handler.

Don’t go any further than that in your coding. Still return HTTPure.notFound for now so that our code will still compile. Then read on when you get stuck or hit an insurmountable compiler error.

The first step is to destructure the Request to get to the body since handle needs the JSON request:

```
router :: Request -> ResponseM
router { body } = HTTPure.notFound
```

Now, we’re going to add oneOf with a list of Handlers, of which we only have 1 at the moment:

```
import Data.Foldable (oneOf) ①
import Handler.Api.Logon (Logon)
import Handler.Class.ApiHandler (handle)
import Type.Proxy (Proxy(..))

router :: Request -> ResponseM
router { body } =
  -- COMPILER ERROR!!
  let handler = oneOf [handle body (Proxy :: _ Logon)] in ②
  HTTPure.notFound
```

① Added these imports.

② We use Proxy to define which handle Method to use.

Even though this has a compiler error, take the time to update your code to look like this.

Here’s the error: