❶ Don’t forget that this can also be `NotAuthenticated`.

Now, create a file under the `Api` directory called `QueryUsers.purs` and code this as far as you can get. This will have some small stumbling blocks, but give it a try and see if you can overcome them. Then return here to see how you did.

This code has a few wrinkles compared to the others, so we’ll take it a little bit slower. Here’s the part that’s pretty much the same as the rest:

```
```purescript
module Api.QueryUsers where ❶

import Data.Generic.Rep (class Generic)
import Data.UUID (UUID)
import Foreign.Generic (genericEncode, genericDecode)
import Foreign.Generic.Class (class Encode, class Decode, defaultOptions)

newtype QueryUsersRequest = QueryUsersRequest { authToken :: UUID }
derive instance genericQueryUsersRequest :: Generic QueryUsersRequest _

instance encodeQueryUsersRequest :: Encode QueryUsersRequest where
  encode = genericEncode defaultOptions

instance decodeQueryUsersRequest :: Decode QueryUsersRequest where
  decode = genericDecode defaultOptions
```
```

❶ Don’t forget the `Api` prefix on the module name since this file is under the `Api` directory.

Now writing the `QueryUsersResults` has a few wrinkles:

```
```purescript
data QueryUsersResults
  = COMPILER ERROR!!
  = QueryUsersResultsSuccess { users :: Array User } ❶
  | QueryUsersResultsFailure { reason :: QueryUsersFailureReason } ❷
derive instance genericQueryUsersResults :: Generic QueryUsersResults _

instance encodeQueryUsersResults :: Encode QueryUsersResults where
  encode = genericEncode defaultOptions

instance decodeQueryUsersResults :: Decode QueryUsersResults where
  decode = genericDecode defaultOptions
```
```

❶ First issue is that we need to define `User`.

❷ Second issue is that we need to create a Type for `QueryUsersFailureReason`.