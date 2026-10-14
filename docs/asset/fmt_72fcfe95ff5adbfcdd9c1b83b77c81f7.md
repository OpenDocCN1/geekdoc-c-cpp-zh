
`1 NotAuthorized` 是指发出请求的账户不是管理员账户。

② 另一个可能的标签值是当 `authToken` 无效时为 `NotAuthenticated`。

创建用户请求：

```
{ "tag": "CreateUserRequest",
  "contents": {
    "authToken": "e0fc09ad-894a-4399-9940-870895c27394",
    "user": {
      "userName": "janeuser",
      "password": "password", ①
      "temporaryPassword": false,
      "admin": false,
      "firstName": "Jane",
      "lastName": "Mama"
    }
  }
}
```

① 此字段是我们用户实体的附加字段。我们必须以某种特殊方式处理它。

创建用户成功响应：

```
{ "tag": "CreateUserResponse",
  "contents": {
    "tag": "CreateUserResultsSuccess"
  }
}
```

创建用户失败响应：

```
{ "tag": "CreateUserResponse",
  "contents": {
    "tag": "CreateUserResultsFailure",
    "contents": {
      "reason": { "tag": "AlreadyExists"} ① ②
    }
  }
}
```

① `AlreadyExists` 是指使用指定的 `userName` 的用户账户已存在。

② 其他可能的标签值是当 `authToken` 无效时为 `NotAuthenticated`，或当用户不是管理员时为 `NotAuthorized`。

## 28.4. 模拟 API

现在我们已经设计了 API，我们应该对其类型进行建模。

首先要做的是在 `src` 目录下创建一个文件夹或目录并将其命名为 `Api`。

然后在 `Api` 目录中创建一个名为 `Logon.purs` 的文件。

然后在 `Logon.purs` 中为以下 JSON 对象编码类型：

```
{
  "tag": "LogonRequest",
  "contents": {
    "userName": "joeuser",
    "password": "password"
  }
}
{
  "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsSuccess",
    "contents": {
      "authToken": "e0fc09ad-894a-4399-9940-870895c27394",
      "mustChangePassword": true
    }
  }
}
{
  "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsFailure"
  }
}
```

在阅读进一步内容之前，尽可能做到。

首先要做的是添加模块定义：

```
module Api.Logon where
```

这里有一个非常重要需要注意的地方是，模块定义不是 `Logon`。它是 `Api.Logon`，因为它在 `Api` 目录下。

接下来，我们将建模请求：

```
newtype LogonRequest = LogonRequest ①
  { ??? ②
  }
```

① 数据构造函数将在 JSON 中成为 `tag` 字段。

② 记录将在 JSON 中成为 `contents` 字段。

我们不使用类型别名，这样我们就能在 JSON 中得到标签。我们想要这样做，以便在我们的 JSON 结构中获得一定的类型安全。

接下来，我们将添加记录字段：

```
newtype LogonRequest = LogonRequest
  { userName :: String
  , password :: String
  }
```

我们应该在这里停下来思考一下密码。

它被定义为 `String`。这并不安全，但不是因为它是 `String`。之所以不安全，是因为我们正以明文形式从浏览器发送到服务器。

这是因为我们的服务器使用的是 `HTTP`，而不是 `HTTPS`。由于我们只是在编写一个学习程序，这没问题，但我们在设计任何登录系统时都应始终牢记这一点。

顺便说一下，你可能会认为在客户端加密密码就能解决这个问题。但事实并非如此。浏览器本质上是不安全的。每个桌面上的每个浏览器都内置了调试工具。基本上，黑客工具已经内置到地球上的每个 Web 应用程序中。

事实上，在客户端加密我们的密码然后通过不安全通道发送，与明文发送相比也只安全一点点。

在明文场景中，黑客只需要拦截传输就能读取密码。

当密码在客户端被加密时，黑客首先必须拦截加密后的密码。然后他们必须理解加密密码的代码是如何工作的。然后他们就可以解密它。

这是可能的，因为加密代码对黑客来说是可用的，因为它是在浏览器中加密的，如果黑客可以访问登录页面，他们就会有访问该代码的权限。

该代码随后可以放入一个程序中，让黑客通过尝试密码进行暴力攻击，直到被盗的加密代码产生黑客截获的加密密码。

第二种场景对黑客来说工作量大得多，会阻止一些黑客，但远非安全，两者都应被视为危险。

换句话说，所有使用密码的登录系统都应通过 `HTTPS` 通信。如果你制作一个通过 `HTTP` 通信的服务器，那么你应该将其置于执行 `HTTPS` 通信的负载均衡器或反向代理之后。

然后你将不安全的服务器置于防火墙之后，即确保它无法从互联网访问。与不安全服务器通信的唯一方式是通过反向代理或负载均衡器。

在排除这个问题之后，我们将基于以下 JSON 对登录响应进行建模：

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsSuccess",
    "contents": {
      "authToken": "e0fc09ad-894a-4399-9940-870895c27394",
      "mustChangePassword": true
    }
  }
}
```

注意 `LogonResultsSuccess` 是一个标签。这是失败情况下 `LogonResultsFailure` 的反面：

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsFailure"
  }
}
```

首先要做的是为这些标签，即数据构造函数，创建一个类型：

```
import Data.UUID (UUID) -- COMPILER ERROR!!
data LogonResults
  = LogonResultsSuccess ①
    { authToken :: UUID ②
    , mustChangePassword :: Boolean
    }
  | LogonResultsFailure
```

① 数据构造函数是 JSON 中的标签。

② 记录是 JSON 中的 `contents`。

如果尚未更新，请将你的代码更新为与此匹配。

编译器错误是因为该包不在我们的 `spago.dhall` 中，所以让我们添加它：

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "arrays"
  , "console"
  , "effect"
  , "httpure"
  , "maybe"
  , "prelude"
  , "psci-support"
  , "uuid" ①
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 保持列表按字母顺序排列。

然后停止服务器（如果它仍在运行）并运行：

```
npx spago build
```

我们仍然会忽略关于 `aff` 的警告。

现在如果你保存 `Logon.purs`，编译器错误应该会消失。

但还有一件事要做。去 Pursuit 上查找 `UUID`，然后点击搜索结果中的包名。

阅读包文档中的说明，然后返回这里。

我找到的内容如下：

> Wrapper for the uuid npm package. This package is not installed automatically, as it comes from npm. Install it with npm install -S uuid.

要安装 npm 包并更新你的 `package.json`，运行：

```
npm install --save uuid@8.3.2 ①
```

① 在文档中，他们说使用 `-S`，这等同于 `--save`。

以下是供参考的响应 JSON 结构：

```
{ "tag": "LogonResponse", "contents": { "tag": "LogonResultsSuccess", "contents": { "authToken": "e0fc09ad-894a-4399-9940-870895c27394", "mustChangePassword": true } } }
{ "tag": "LogonResponse", "contents": { "tag": "LogonResultsFailure" } }
```

最后，我们需要定义 `LogonResponse` 的类型：

```
newtype LogonResponse = LogonResponse LogonResults
```

添加此类型，然后为 `LogonRequest`、`LogonResults` 和 `LogonResponse` 创建 `Encode` 和 `Decode` 实例。参考你在其他章节中编写的代码，了解如何执行此操作。

在继续阅读之前先完成此操作。

首先，这里是 `LogonRequest` 的更改：

```
import Data.Generic.Rep (class Generic) ①
import Foreign.Generic (genericEncode, genericDecode)
import Foreign.Generic.Class (class Encode, class Decode, defaultOptions)
newtype LogonRequest = LogonRequest ②
  { userName :: String
  , password :: String
  }
derive instance genericLogonRequest :: Generic LogonRequest _
instance encodeLogonRequest :: Encode LogonRequest where
  encode = genericEncode defaultOptions
instance decodeLogonRequest :: Decode LogonRequest where
  decode = genericDecode defaultOptions
```

① 添加这些导入。

② 此定义已在此处，我们只是添加了派生 `Generic` 实例的行。

如果你没有完成，请停止并查看是否可以完成 `LogonResults` 和 `LogonResponse` 的 `Encode` 和 `Decode` 实例，然后继续阅读。

以下是 `LogonResults` 的更改：

```
data LogonResults ①
  = LogonResultsSuccess
    { authToken :: UUID
    , mustChangePassword :: Boolean
    }
  | LogonResultsFailure
drive instance genericLogonResults :: Generic LogonResults _
instance encodeLogonResults :: Encode LogonResults where
  encode = genericEncode defaultOptions
instance decodeLogonResults :: Decode LogonResults where
  decode = genericDecode defaultOptions
```

① 此定义已在此处，我们只是添加了派生 `Generic` 实例的行。

如果你没有完成，请停止并查看是否可以完成 `LogonResponse` 的 `Encode` 和 `Decode` 实例，然后继续阅读。

以下是 `LogonResponse` 的更改：

```
newtype LogonResponse = LogonResponse LogonResults
derive instance genericLogonResponse :: Generic LogonResponse _
instance encodeLogonResponse :: Encode LogonResponse where
    encode = genericEncode defaultOptions
instance decodeLogonResponse :: Decode LogonResponse where
    decode = genericDecode defaultOptions
```

① 此定义已在此处，我们只是添加了派生 `Generic` 实例的行。

现在，在我们急于建模任何其他 JSON 请求和响应之前，我们应该编写一些测试代码，以确保我们没有走上错误的道路。

在 `src` 下创建一个名为 `Test.purs` 的文件并添加以下代码：

```
module Test where
import Prelude
import Api.Logon (LogonRequest(..), LogonResponse(..), LogonResults(..))
import Effect (Effect)
import Effect.Class.Console (log)
test :: Effect Unit
test = do
    log "placeholder" ①
```

① 我们稍后会删除它。

不要太担心关于冗余导入的编译器警告。这只是我们完成后会丢弃的测试代码。

接下来，注释掉 `Main.purs` 中的 `main` 并替换为：

```
import Effect (Effect) ①
import Test (test)
main :: Effect Unit
main = test
```

① 添加这些导入。

同样，暂时不要担心冗余导入。

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

现在，再次使用 `npx spago run` 运行你的程序，运行后应输出：

```
placeholder
```

现在，从测试函数中删除日志 `"placeholder"` 行。然后添加代码先创建 `LogonRequest` 再将其编码为 JSON。最后，将该 JSON 显示到控制台。

完成后，返回此处。

以下是该代码：

```
import Foreign.Generic (encodeJSON) ①
test :: Effect Unit
test = do
  log $ encodeJSON
    $ LogonRequest { userName: "joeuser", password: "password" } ②
```

- ① 导入 `encodeJSON` 函数。
- ② 创建一个测试 `LogonRequest`。

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

接下来，注释掉 `log` 行并添加一条类似的但用于 `LogonResponse` 的日志，看看其输出是否与以下内容匹配：

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsSuccess",
    "contents": {
      "authToken": "00000000-0000-0000-0000-000000000000",
      "mustChangePassword": true
```
