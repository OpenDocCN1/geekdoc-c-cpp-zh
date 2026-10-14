Second, if we decided to change where we store the Accounts, we’ll have minimal changes to make to our code.

And finally, we don’t have to figure out how to write this complex line of code every time we want to get the accounts.

Next, create a File under src/Handler/Api called QueryUsers.purs and code up a the ApiHandler Instance stubbing out the handler Function for now. Use all of the code we’ve written so far as reference.

Then return here to see how you did.

We’ll start with:

```
module Handler.Api.QueryUsers where

import Prelude

import Data.Api.QueryUsers (QueryUsersRequest(..), QueryUsersResponse(..)
, QueryUsersResults(..)
, QueryUsersFailureReason(..))
import Handler.Class.ApiHandler (class ApiHandler, Handler)
import Handler.Api.Common (handleApi)
import HTTPure as HTTPure

data QueryUsers = QueryUsers

handler :: QueryUsersRequest -> Handler
handler _ = HTTPure.notFound ①

instance apiHandlerQueryUsers :: ApiHandler QueryUsers where
  handle _ = handleApi handler
```

① This is stubbed out.

The instance implementation was copy and pasted from CreateUser’s with the obvious edits to change CreateUser to QueryUsers.

Next, the imports were stolen once again from CreateUser and edited where necessary.

The QueryUsers data Type is following the standard pattern we established for API Handlers.

And finally, handler is a dummy version that always sends a 404. It’s just here to keep the compiler happy.

We have some warnings about redundant imports, but we’re going to ignore them for now because we plan on needing them eventually. And if not, we can clean them up in the end.