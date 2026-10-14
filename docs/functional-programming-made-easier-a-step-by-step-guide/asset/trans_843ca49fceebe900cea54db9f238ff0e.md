

现在使用以下命令运行服务器：

```
npx spago run
```

然后修复错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- foreign-generic
```

现在，再次使用 npx spago run 运行你的程序，运行后应输出：

```
placeholder
```

现在，从测试函数中删除日志 "placeholder" 行。然后添加代码先创建 LogonRequest 再将其编码为 JSON。最后，将该 JSON 显示到控制台。

完成后，返回此处。

以下是该代码：

```
import Foreign.Generic (encodeJSON) ①

test :: Effect Unit
test = do
  log $ encodeJSON
    $ LogonRequest { userName: "joeuser", password: "password" } ②
```

- ① 导入 encodeJSON 函数。
- ② 创建一个测试 LogonRequest。

现在运行你的程序看看结果。然后在阅读后续内容之前，将其与以下内容进行比较，看看结构是否相同：

```
{ "tag": "LogonRequest",
  "contents": {
    "userName": "joeuser",
    "password": "password"
  }
}
```

测试代码的输出如下：

```
{"contents":{"userName":"joeuser","password":"password"},"tag":"LogonRequest"}
```

即使顶层 JSON 键的顺序不同，这也符合我们的 API 设计，因此没问题。

接下来，注释掉 log 行并添加一条类似的但用于 LogonResponse 的日志，看看其输出是否与以下内容匹配：

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsSuccess",
    "contents": {
      "authToken": "00000000-0000-0000-0000-000000000000",
      "mustChangePassword": true
    }
  }
}
```

使用 emptyUUID 作为虚拟 authToken，并在完成后返回此处。

以下是要添加到 test 的代码：

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

① 不要忘记模块名称上的 Api 前缀，因为此文件位于 Api 目录下。

以下是 QueryUsers API 设计的参考：

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

接下来，我们需要定义 User，但我希望将 User 定义放在 Api 模块之外。它在我们的系统中更像是一个实体。

因此，在 src 下创建一个名为 Entity 的新文件夹，然后在其中添加一个名为 User.purs 的文件。

然后使用以下内容作为参考编写 User 实体代码及其 Encode 和 Decode 实例：

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

以下是 User 的代码：

