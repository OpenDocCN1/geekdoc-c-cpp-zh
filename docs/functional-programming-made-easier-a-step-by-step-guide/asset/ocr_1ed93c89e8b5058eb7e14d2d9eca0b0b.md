[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- httpure

Now edit your Main.purs to be the following:

```
module Main where

import Prelude

import Effect.Class.Console (log)
import HTTPure as HTTPure
import HTTPure.Request (Request)
import HTTPure.Response (ResponseM)
import HTTPure.Server (ServerM)

router :: Request -> ResponseM
router _ = HTTPure.ok "This works" ① ②

port :: Int
port = 3000

main :: ServerM
main = HTTPure.serve port router
  $ log $ "Server up running on port: " <> show port ③
```

① The router takes any request and determines the appropriate response. Our simple one here just replies with a constant text message.

② HTTPure.ok send a response with an HTTP Statue Code of 200.

③ HTTPure.serve starts an insecure server on the specified port. Once the server is up, it’ll run the third Parameter, which is an Effect Unit. This could’ve been a do block, but we’ve only have 1 line of code.

Now run this server using:

```
npx spago run
```

Then open up a browser and put in the Address Bar, localhost:3000, then hit return. It should display This works.

Now, if you look closely at main’s Type Signature, you may be wondering how we can have a main that