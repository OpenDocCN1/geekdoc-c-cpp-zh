
```
    }
  }
}
```

使用`emptyUUID`作为虚拟`authToken`，并在完成后返回此处。

以下是要添加到 `test` 的代码：

```
import Data.UUID (emptyUUID) ①
test :: Effect Unit
test = do
  -- log $ encodeJSON
  --   $ LogonRequest { userName: "joeuser", password: "password" } ②
  log $ encodeJSON $ LogonResponse
    $ LogonResultsSuccess
      { authToken: emptyUUID, mustChangePassword: true } ③
```

- ❶ 导入 `emptyUUID` 以获取测试 UUID。
- ❷ 注释掉这段代码。
- ❸ 添加了这行代码。

运行此代码输出：

```
{"contents":{"contents":{"mustChangePassword":true,"authToken":"00000000-0000-0000-0000-000000000000"},"tag":"LogonResultsSuccess"},"tag":"LogonResponse"}
```

最后，注释掉该 `log` 行并添加代码来测试 `LogonResponse` 的失败情况，看看它是否具有与以下相同的结构：

```
{
  "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsFailure"
  }
}
```

在阅读后续内容之前先完成此操作。

以下是 `test` 的更改：

```
test :: Effect Unit
test = do
  -- log $ encodeJSON
  --   $ LogonRequest { userName: "joeuser", password: "password" }
  -- log $ encodeJSON $ LogonResponse
  --   $ LogonResultsSuccess
  --     { authToken: emptyUUID, mustChangePassword: true }
  log $ encodeJSON $ LogonResponse $ LogonResultsFailure
```

运行后输出：

```
{ "contents": { "tag": "LogonResultsFailure" }, "tag": "LogonResponse" }
```

这也匹配。

看起来我们正在朝着正确的方向前进。

接下来，我们将处理 `Logoff` API。以下是参考设计：

```json
{ "tag": "LogoffRequest",
  "contents": {
    "authToken": "e0fc09ad-894a-4399-9940-870895c27394"
  }
}

{ "tag": "LogoffResponse",
  "contents": {
    "tag": "LogoffResultsSuccess"
  }
}

{ "tag": "LogoffResponse",
  "contents": {
    "tag": "LogoffResultsFailure"
  }
}
```

现在，在 `Api` 目录下创建一个名为 `Logoff.purs` 的文件，并像我们为 `Logon` 所做的那样进行操作。然后返回此处查看你的完成情况。

由于它与 `Logon.purs` 几乎相同，以下是完整实现：

```
module Api.Logoff where ①
import Data.Generic.Rep (class Generic)
import Data.UUID (UUID)
import Foreign.Generic (genericEncode, genericDecode)
import Foreign.Generic.Class (class Encode, class Decode, defaultOptions)

newtype LogoffRequest = LogoffRequest { authToken :: UUID }
derive instance genericLogoffRequest :: Generic LogoffRequest _
instance encodeLogoffRequest :: Encode LogoffRequest where
    encode = genericEncode defaultOptions
instance decodeLogoffRequest :: Decode LogoffRequest where
    decode = genericDecode defaultOptions

data LogoffResults = LogoffResultsSuccess | LogoffResultsFailure
derive instance genericLogoffResults :: Generic LogoffResults _
instance encodeLogoffResults :: Encode LogoffResults where
    encode = genericEncode defaultOptions
instance decodeLogoffResults :: Decode LogoffResults where
    decode = genericDecode defaultOptions

newtype LogoffResponse = LogoffResponse LogoffResults
derive instance genericLogoffResponse :: Generic LogoffResponse _
instance encodeLogoffResponse :: Encode LogoffResponse where
    encode = genericEncode defaultOptions
instance decodeLogoffResponse :: Decode LogoffResponse where
    decode = genericDecode defaultOptions
```

① 不要忘记模块名称上的 `Api` 前缀，因为此文件位于 `Api` 目录下。

以下是 `QueryUsers` API 设计的参考：

```json
{ "tag": "QueryUsersRequest",
  "contents": {
    "authToken": "e0fc09ad-894a-4399-9940-870895c27394"
  }
}

{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsSuccess",
    "contents": {
      "users": [
        { "tag": "User",
          "contents": {
            "userName": "joeuser",
            "temporaryPassword": true,
            "admin": true,
            "firstName": "Joe",
            "lastName": "Mama"
          }
        },
        { "tag": "User",
          "contents": {
            "userName": "janeuser",
            "temporaryPassword": false,
            "admin": false,
            "firstName": "Jane",
            "lastName": "Mama"
          }
        }
      ]
    }
  }
}

{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsFailure",
    "contents": {
      "reason": { "tag": "NotAuthorized" }
    }
  }
}
```

❶ 不要忘记这也可以是 `NotAuthenticated`。

现在，在 `Api` 目录下创建一个名为 `QueryUsers.purs` 的文件并尽可能编码。这会有一些小障碍，但请尝试看看能否克服。然后返回此处查看你的完成情况。

此代码与之前的相比有一些不同之处，因此我们将放慢一点。以下是与之前几乎相同的部分：

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

❶ 不要忘记模块名称上的 `Api` 前缀，因为此文件位于 `Api` 目录下。

现在编写 `QueryUsersResults` 有一些不同之处：

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

- ❶ 第一个问题是我们需要定义 `User`。
- ❷ 第二个问题是我们需要为 `QueryUsersFailureReason` 创建一个类型。

你可能编写了不同的代码，它也完全可以，但为了继续完成本章，请将你的代码更改为与此匹配，即使我们有一些未定义项。

接下来，我们需要定义 `User`，但我希望将 `User` 定义放在 `Api` 模块之外。它在我们的系统中更像是一个实体。

因此，在 `src` 下创建一个名为 `Entity` 的新文件夹，然后在其中添加一个名为 `User.purs` 的文件。

然后使用以下内容作为参考编写 `User` 实体代码及其 `Encode` 和 `Decode` 实例：

```
{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsSuccess",
    "contents": {
      "users": [
        { "tag": "User",
          "contents": {
            "userName": "joeuser",
            "temporaryPassword": true,
            "admin": true,
            "firstName": "Joe",
            "lastName": "Mama"
          }
        },
        { "tag": "User",
          "contents": {
            "userName": "janeuser",
            "temporaryPassword": false,
            "admin": false,
            "firstName": "Jane",
            "lastName": "Mama"
          }
        }
      ]
    }
  }
}
```

在阅读后续内容之前完成该文件的代码。

以下是 `User` 的代码：

```
module Entity.User where
import Data.Generic.Rep (class Generic)
import Foreign.Generic (genericEncode, genericDecode)
import Foreign.Generic.Class (class Encode, class Decode, defaultOptions)

newtype User = User 2
  { userName :: String
  , temporaryPassword :: Boolean
  , admin :: Boolean
  , firstName :: String
  , lastName :: String
  }
derive instance genericUser :: Generic User _
instance encodeUser :: Encode User where
  encode = genericEncode defaultOptions
instance decodeUser :: Decode User where
  decode = genericDecode defaultOptions
```

① 不要忘记在模块名上加上 `Entity` 前缀，因为这个文件位于 `Entity` 目录下。

② 虽然我们的图表中为 CSV 包含了 `passwordHash`，但我们应该尽可能保护该信息。这就是为什么它在 `User` 中缺失的原因。否则，它可能会意外地在 `QueryUsersResponse` 中发送给客户端。

现在，将 `Entity.User` 导入到 `Api.QueryUsers` 中。这应该能消除 `User` 上的编译器错误。

然后在 `Api.QueryUsers` 中编写 `QueryUsersFailureReason` 的类型并使其可编码和可解码。以下是供参考的 JSON：

```
{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsFailure",
    "contents": {
      "reason": { "tag": "NotAuthorized"} ①
    }
  }
}
```

① 不要忘记这也可以是 `NotAuthenticated`。

完成 `QueryUsersFailureReason` 的编码后，`Api.QueryUsers` 应该可以编译了。

停止阅读并试试看。

以下是 `QueryUsersFailureReason` 的代码：

```
data QueryUsersFailureReason = NotAuthorized | NotAuthenticated

derive instance genericQueryUsersFailureReason
  :: Generic QueryUsersFailureReason _

instance encodeQueryUsersFailureReason
  :: Encode QueryUsersFailureReason where
encode = genericEncode defaultOptions

instance decodeQueryUsersFailureReason
  :: Decode QueryUsersFailureReason where
decode = genericDecode defaultOptions
```

接下来，在继续之前将 `QueryUsersResponse` 的代码添加到 `Api.QueryUsers` 中。

以下是完整实现：

```
module Api.QueryUsers where
import Data.Generic.Rep (class Generic)
import Data.UUID (UUID)
import Entity.User (User) ①
```
