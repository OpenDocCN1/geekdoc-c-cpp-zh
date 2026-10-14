
```purescript
delete
  :: ∀ proxy r1 r2 l a
  . IsSymbol l
  => Lacks l r1
  => Cons l a r1 r2
  => proxy l
  -> Record r2
  -> Record r1
```

> 这些 Constraints 已内置于编译器中。

要理解这一点，首先查看 `proxy` 的 Type 参数 `l`，它代表我们在 Row `r2` 中要删除的 `label`。它有一个 `IsSymbol` 约束，这意味着它必须是字面量 String。你不能在此处使用 Type 为 `String` 的变量。

接下来的 2 个 Constraints 是 Type 级魔法的发生之处。

第一个是 `Lacks l r1`。此约束说明返回的 Record 的 Row `r1` 必须不包含 `Symbol` `l`。这很有意义，因为 `delete` 应该删除该字段，而 `Record r1` 是返回的。记住，我们可以使用 Data Constructor `Record` 从 Rows 构造 Records。

第二个是 `Cons l a r1 r2`。`l` 是我们的 `Symbol`，代表一个 Label。`a` 是一个 Type，代表 Label 的 Type。记住 Rows 由 Label 和其对应 Type 的 Pair 组成：

```purescript
type SomeRow = ( someLabel :: String, someOtherLable :: Int )
```

因此，`Cons` 是一个约束，它将确保 Row `r1`，即删除后的标签，加上 Type 为 `a` 的 Label `l`，等于 Row `r2`，即我们开始时的标签。

换句话说，`Lacks` 确保最终返回的 Row `r1` 不已具有我们要删除的标签，而 `Cons` 确保 Rows `r1` 和 `r2` 之间唯一的差异就是一个标签。

所有这些检查都在 Type 级别完成，这就是为什么它是 Type Safe 的，也是为什么 `writeBody__` 无法编译的原因。

如果查看 `delete` 的实现，它只是调用 Javascript 从 Javascript Object 中删除一个字段，而 PureScript Records 的底层表示就是 Javascript Object。这可以安全地完成，因为它已经由编译器进行 Type 检查，所以我们知道在 Javascript 尝试 `delete` 它之前，该键必须存在于 Object 中。

现在，将你的 `loggingRouter` 修改为如下所示：

```haskell
import Record (delete) ❶

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  log $ "REQUEST: " <> show req
  res <- router env req
  log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody") res) ❷
  pure res
```

- ❶ 添加此导入。
- ❷ 这是用于记录 `Response` 的新代码行。

现在，我们可以向此 Function 添加很多东西。例如，我们可以添加时间戳。在生产环境中使用 Log Aggregator 如 Logify 或 DataDog 运行程序时，你不需要这样做，因为这些工具会自动为你的日志行添加时间戳。

以防你不熟悉 Log Aggregators，它们通常会收集程序写入控制台的输出，即 Linux 中的 `stdout` 和 `stderr`，并将其与其他服务器的日志一起聚合到企业的在线 Data Store 中。收集日志的一部分是在收集时为其添加时间戳。这使它们能够以正确的顺序呈现日志。

我们还可以做另一件事，即添加一种方法来将 `Request` 与 `Response` 关联起来，这样当我们在包含许多同时 `Requests` 的巨大日志中挖掘时，我们将能够快速找到某个 `Request` 的对应 `Response`。我们可以很容易地做到这一点。所以让我们这样做。

生成一个 UUID 并将其与 `Request` 和 `Response` 日志行一起显示。查看 Session Manager 中生成 UUID 的位置并为此 Function 盗用该代码。

在完成此任务后返回阅读。

以下是更改：

```haskell
import Data.UUID (genUUID) ❶

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  id <- liftEffect genUUID ❷
  let idStr = " (" <> show id <> ")" ❸
  log $ "REQUEST: " <> show req <> idStr ❹
  res <- router env req
  log $ "RESPONSE: "
      <> (show $ delete (Proxy :: _ "writeBody") res) <> idStr ❹
  pure res
```

- 1. 添加此导入。
- 2. `genUUID` 在 `Effect` 中运行，因此我们使用 `liftEffect`。
- 3. 我们一次性计算标识 `String`。
- 4. 将标识 `String` 附加到两个日志行。

最后一件有用的事情是知道你的服务器响应速度如何，通过计时处理请求所需的时间。这也很简单。我们只需在收到请求时立即从 Epoch 开始获取当前时间（以毫秒为单位），并在响应前立即获取。然后我们计算差值并在 `Response` 日志行中显示毫秒数。

查看我们在 Session Manager 中如何获取当前时间（以毫秒为单位），以帮助你在 `loggingRouter` 中添加此功能。完成后，继续阅读。

以下是这些更改：

```haskell
import Data.JSDate (now, getTime)

loggingRouter :: HandlerEnv -> Request -> ResponseM

loggingRouter env req = do

  start <- getTime <$> liftEffect now

  id <- liftEffect genUUID

  let idStr = " (" <> show id <> ")"

  log $ "REQUEST: " <> show req <> idStr

  res <- router env req

  end <- getTime <$> liftEffect now

  log $ "RESPONSE: "

    <> (show $ delete (Proxy :: _ "writeBody") res)

    <> " [" <> show (end - start) <> " ms]"

    <> idStr

  pure res
```

- 1. 导入时间 Functions。
- 2. 尽可能早地获取开始时间。
- 3. 尽可能晚地获取结束时间。
- 4. 将为 `Request` 提供服务所花费的持续时间添加到 `Response` 日志行。

仔细看看我们的 `loggingRouter`。你是不是很高兴我们把它写成一个单独的 Function？

现在，修改 `main` 以使用 `loggingRouter` 而不是 `router` 并重新运行服务器并用 Postman 测试它。

嗯，当我这样做时，我得到错误：

[error] 你的项目文件中的某些部分从不在项目直接依赖中的包导入模块。
要修复此错误，请将以下包添加到你的配置中的依赖列表中：
- record

修复后重新运行服务器并使用 Postman 测试它。

你应该会看到类似这样的内容：

```
REQUEST: { body: "{ \"tag\": \"LogonRequest\",\n \"contents\": {\n \"userName\": \"admin\",\n  \"password\": \"admin\"\n }\}", headers:

accept: */*

accept-encoding: gzip, deflate, br

cache-control: no-cache

connection: keep-alive

content-length: 95

content-type: text/plain

host: localhost:3000

postman-token: 297f753b-8fb0-47a3-8ee3-49e0fb3890c5

user-agent: PostmanRuntime/7.26.3

, httpVersion: HTTP/1.1, method: Post, path: [], query: (fromFoldable []) }

((UUID 02d93824-585b-45f4-84bd-2ce4531d8289))

RESPONSE: { headers: Content-Length: 154

, status: 200 } [20.0 ms] ((UUID 02d93824-585b-45f4-84bd-2ce4531d8289))
```

① 请注意响应的 body 缺失了。这是因为 Response 将 writeBody 编码为一个 Function，该 Function 会将 body 作为副作用写入。由于 HTTPure 的设计选择，我们没有简单的方法来访问 body。因此对于这个学习示例，我们将把它省略。

现在这是一个相当难看的日志，但对于我们所做的很少的工作来说还不错。而且所有的信息都在那里供我们调试大多数问题。肯定包括我们在这里会遇到的所有问题。

唯一缺少的是时间戳，而由于我们现在代码中已有时间逻辑，添加这个应该很容易。所以，让我们一起做。

首先，我们将 start 和 end 改为 startDate 和 endDate，然后我们将从这些值计算 start 和 end：

```haskell
loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  startDate <- liftEffect now
  id <- liftEffect genUUID
  let idStr = " (" <> show id <> ")"
  log $ "REQUEST: " <> show req <> idStr
  res <- router env req
  endDate <- liftEffect now
  let duration = getTime endDate - getTime startDate
  log $ "RESPONSE: "
    <> (show $ delete (Proxy :: _ "writeBody") res)
    <> " [" <> show duration <> " ms]"
    <> idStr
  pure res
```

+   1. 移除了使用 `getTime` 的映射并重命名以在变量名末尾添加 `Date`。
+   2. 现在在这里使用 `getTime` 从 `startDate` 和 `endDate` 计算持续时间。
+   3. 在日志行中使用 `duration`。

接下来，我们将创建一个小助手来格式化时间戳，称为 `ts`：

```haskell
import Data.JSDate (now, getTime, toUTCString)

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  startDate <- liftEffect now
  id <- liftEffect genUUID
  let idStr = " (" <> show id <> ")"
      ts dt = "(" <> toUTCString dt <> ")"
  log $ "REQUEST: " <> show req <> idStr
  res <- router env req
  endDate <- liftEffect now
  let duration = getTime endDate - getTime startDate
  log $ "RESPONSE: "
    <> (show $ delete (Proxy :: _ "writeBody") res)
    <> " [" <> show duration <> " ms]"
    <> idStr
  pure res
```

+   1. 在导入列表中添加了 `toUTCString`。
+   2. `ts` 将接收一个 `JSDate`，即 `dt`，并通过利用 `toUTCString` 生成可读的人类 UTC 日期和时间。

现在我们要做的就是为日志行加上适当的时间戳前缀：

```haskell
loggingRouter :: HandlerEnv -> Request -> ResponseM

loggingRouter env req = do

    startDate <- liftEffect now

    id <- liftEffect genUUID

    let idStr = " (" <> show id <> ")"

        ts dt = "(" <> toUTCString dt <> ") "

    log $ ts startDate <> "REQUEST: " <> show req <> idStr ①

    res <- router env req

    endDate <- liftEffect now

    let duration = getTime endDate - getTime startDate

    log $ ts endDate <> "RESPONSE: " ②

        <> (show $ delete (Proxy :: _ "writeBody") res)

        <> " [" <> show duration <> " ms]"

        <> idStr

    pure res
```

① 为 Request 添加了 ts startDate。

② 为 Response 添加了 ts endDate。

将你的代码更新为与此匹配，然后重新运行服务器并使用 Postman 测试它。你应该会得到类似这样的内容：

```
(Sat, 22 May 2021 20:06:44 GMT) REQUEST: { body: "{ \"tag\": \"LogonRequest\",\n \"contents\": {\n  \"userName\": \"admin\",\n \"password\": \"admin\"\n }\n}", headers: accept: */*

accept-encoding: gzip, deflate, br

cache-control: no-cache

connection: keep-alive

content-length: 95

content-type: text/plain

host: localhost:3000

postman-token: ed7a8a01-8345-4087-853c-67fc47b4e27a

user-agent: PostmanRuntime/7.26.3

, httpVersion: HTTP/1.1, method: Post, path: [], query: (fromFoldable []) } ((UUID 3ff66d80-ebbe-4b8a-9119-5de7d8e8020b))

(Sat, 22 May 2021 20:06:44 GMT) RESPONSE: { headers: Content-Length: 154

, status: 200 } [18.0 ms] ((UUID 3ff66d80-ebbe-4b8a-9119-5de7d8e8020b))
```

## 28.10. 编码 API

在途中，我们已经为 `LogonRequest` 编码了 API 以使我们的服务器各部分正常工作。但现在，是时候完成 API 了。

我们还有以下 API 请求需要编码：

- Create User
- Query Users
- Logoff

让我们从最容易的一个 `LogoffRequest` 开始。因为我们刚刚完成了 `LogonRequest`，现在做这个是个好时机。

### 28.10.1. 编码 `LogoffRequest` API 处理器

在编码之前，我们应该回顾一下为 `Logon` 所做的工作，看看我们可以借鉴什么：

```haskell
data Logon = Logon

handler :: LogonRequest -> Handler

handler (LogonRequest { userName, password }) = do

  { accountsAVar } <- ask

  verifiedAccount <- lift $ verifyLogon accountsAVar userName password

  HTTPure.ok $ encodeJSON $ case verifiedAccount of

    Nothing -> LogonResponse LogonResultsFailure

    Just (Account { temporaryPassword }) -> LogonResponse
```
