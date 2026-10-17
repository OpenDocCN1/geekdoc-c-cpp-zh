
```haskell
expireSessions :: AVar Sessions -> Aff Unit
expireSessions sessionsAVar = do
  now <- getTime <$> liftEffect now
  sessions <- AVar.take sessionsAVar
  AVar.put
    (Map.filter
      (\(Session { lastTime }) -> now - lastTime > sessionTimeout)
      sessions)
    sessionsAVar
```

① 过滤函数。

② 解构 `Session` 和底层的 `Record` 以获取到 `lastTime`。

将你的代码更新为与此一致。

我们应该在每次有人尝试验证 `Session` 时调用它。还有，每当有人成功验证 `Session` 时，我们应该更新 `lastTime`，因为他们显然仍处于活跃状态。所以本质上，API 调用会让 `Session` 保持存活。

每次调用 `verifySession` 时先过期 `Sessions`。在继续之前先做到这一点。

我们会在读取它们之前立即过期会话：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.read sessionsAVar
  pure $ Map.lookup authToken sessions
```

① 添加了对 `expireSessions` 的调用

现在，修改你的代码以更新刚刚验证的 `Session` 中的 `lastTime`。由于你正在更新 `Sessions`，你需要将 `read` 改为 `take`，并且在更新完 `Session` 后，你需要使用 `put`。

一旦你完成了或遇到阻碍，回到这里。

我们将从第一部分开始重写 `verifySession`：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.take sessionsAVar
  ???
```

① 将 `read` 改为 `take`。

现在，我们获取当前时间：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.take sessionsAVar
  now <- getTime <$> liftEffect now
  ???
```

① 从 `expireSessions` 那里偷来的。

接下来，我们需要查找 `authToken`，然后分别处理错误和成功的情况。如果你认为可以从这里完成，请停止并去做。准备好后再回来。

首先，我们查找 `authToken` 并处理错误情况：

```haskell
import Data.Maybe (Maybe(..))
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.take sessionsAVar
  now <- getTime <$> liftEffect now
  case Map.lookup authToken sessions of
    Nothing -> AVar.put sessions sessionsAVar *> pure Nothing
    ???
```

1. 添加了 `( .. )` 以包含数据构造子。
2. 查找 `authToken`。
3. 如果未找到，则简单地将原始的 `sessions` 放回去。注意使用了 `*>`，即 `applySecond`。
4. 返回无效，即 `Nothing`。

接下来，我们通过先计算 `lastTime` 等于 now 的新 `Session` 来处理成功情况：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.take sessionsAVar
  now <- getTime <$> liftEffect now
  case Map.lookup authToken sessions of
    Nothing -> AVar.put sessions sessionsAVar *> pure Nothing
    Just (Session session) -> do
      let newSession = Session $ session { lastTime = now }
      ???
```

1. 使用模式匹配解构以暴露底层的 `Record`，即 `session`。
2. 构造一个 `lastTime` 设置为当前时间，即 now 的新 `Session`。注意使用了 `=` 因为我们正在使用更新 `Record` 语法。

现在我们需要更新我们的 `Map`，即 `Sessions`：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
    expireSessions sessionsAVar
    sessions <- AVar.take sessionsAVar
    now <- getTime <$> liftEffect now
    case Map.lookup authToken sessions of
        Nothing -> AVar.put sessions sessionsAVar *> pure Nothing
        Just (Session session) -> do
            let newSession = Session $ session { lastTime = now }
                newSessions = Map.insert authToken newSession sessions ①
            ???
```

① 使用 `newSession` 更新 `Map`。这会用相同的 `authToken` 作为键来替换旧的 `Session` 值。

最后，我们将 `newSessions` 放入 `AVar` 并返回 `newSession`：

```haskell
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
    expireSessions sessionsAVar
    sessions <- AVar.take sessionsAVar
    now <- getTime <$> liftEffect now
    case Map.lookup authToken sessions of
        Nothing -> AVar.put sessions sessionsAVar *> pure Nothing
        Just (Session session) -> do
            let newSession = Session $ session { lastTime = now }
                newSessions = Map.insert authToken newSession sessions
            AVar.put newSessions sessionsAVar ①
            pure $ Just newSession ②
```

① 使用更新后的 `Map`，即 `newSessions` 更新 `AVar`。

② 返回更新后的 `session`，即 `newSession`。

现在，`verifySession` 处理了过期和 `Session` 保持活跃。

但，注意到我们在 2 处调用了 `AVar.put`。如果我们在 `Nothing` 情况下忘记调用它，我们就会有一个相当糟糕的 bug。这个 bug 很容易通过 QA 并进入生产环境。

然后在我们部署服务器数月后的某个不幸日子里，来自已过期会话的请求会挂住我们的服务器。

那是因为我们执行了 `AVar.take` 而没有对应的 `AVar.put`。

更好的做法是只有一个 `AVar.put`。两个 `case` 都依赖它。

我将把 `case` 表达式改为返回一个 `Tuple`，其中包含我们更新后的 `sessions` 以及我们刚刚验证的 `Maybe` 更新后的 `session`：

```haskell
import Data.Tuple (Tuple(..))
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  sessions <- AVar.take sessionsAVar
  now <- getTime <$> liftEffect now
  let Tuple newSessions newSession =
        case Map.lookup authToken sessions of
          Nothing -> Tuple sessions Nothing
          Just (Session session) ->
            let newSession = Session $ session { lastTime = now }
                newSessions = Map.insert authToken newSession sessions in
            Tuple newSessions (Just newSession)
  AVar.put newSessions sessionsAVar
  pure newSession
```

1. 添加了 `import`。
2. 我们的 `case` 表达式返回一个 `Tuple` 并立即解构为 `newSessions` 和 `newSession`。
3. 在失败情况下，我们的旧 `sessions` 未改变。我们也返回 `Nothing` 因为我们未能找到 `authToken`。
4. 我们不再在 `do` 块中。
5. 注意使用了 `in` 关键字，因为我们不再在 `do` 块中。
6. 在成功情况下，我们更新了 `sessions` 和 `session`。因此我们在 `Tuple` 中返回这些更改后的值。
7. 唯一的一个 `AVar.put`。如果我们忘记了这一行代码，我们每次尝试做任何事情时都会发现错误。这个 bug 不会离开开发阶段，更不会离开 QA。
8. 返回我们的 `Maybe Session`。

在继续阅读之前，先将你的 `verifySession` 改为这个更安全的版本。

在继续之前，我们应该运行服务器并确保它仍然正常工作：

```text
npx spago run
```

我收到这个错误：

```text
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
– js-date
```

修复此错误然后再次运行。

然后前往 **Postman** 再次发送一个 `LogonRequest`。

当我这样做时，一切仍然正常工作。希望你的也一样。

## 28.9. Server Logging

Logging 是任何 Server 的生命线。这是因为它们在某个机房里无人值守运行。我们在问题冒头时并不会在场。

Logs 让我们知道发生了什么。

当然在真实世界的服务器中，我们会在 Logging 上花费远比这里更多的时间，但这仍然能给你一个基本概念。

让我们在请求到来时记录每个 `Request`。在阅读下面的内容之前，先查看代码库并找出执行此操作的最佳位置。

我最初的反应是修改 `router`，但随后我意识到制作一个 Logging Router 要好得多。这样我们就不会用日志污染 `router` 的复杂逻辑。

Logging Router 会记录 `Request`，然后调用我们当前的 `router`，然后在返回之前记录 `Response`。它只是对 `router` 的一个简单的函数式包装。

它还必须作为我们当前 `router` 的替代品，这意味着它将具有相同或至少相似的 Type Signature。

尽可能多地编写它。将其命名为 `loggingRouter` 并放入 `Main` 中，然后在完成或遇到瓶颈时返回。

我写的是：

```haskell
loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  log $ "REQUEST: " <> show req
  res <- router env req
  log $ "RESPONSE: " <> show res
  pure res
```

1. 记录 `Request`。
2. 委托给 `router` 并在 `res` 中捕获 `Response`。
3. 记录 `Response`（有编译错误）。
4. 返回 `Response`。

这是编译器的抱怨：

![](img/8c0e9b687c62642e828ccb5481e11313_1438_0.png)

你对这个错误有什么看法？我们下一步该做什么？

当我看到这个时，我问的问题是，`Response` 的 Type 是什么。当我在 Pursuit 上查看时，我发现：

```haskell
type Response =
  { status :: Status.Status
  , headers :: Headers.Headers
  , writeBody :: HTTP.Response -> Aff.Aff Unit
  }
```

这是我们的问题孩子。

那个 `Function` 是 NOT showable。我们希望有一种方法来移除该字段，然后显示记录的其余部分。

我们可以手动完成，但有一个很酷的库可以为任何 `Record` 完成此操作。它叫做 `purescript-record`。它有一个名为 `Record` 的模块。并且该模块中有一个名为 `delete` 的函数，它会创建一个没有指定字段的新 `Record`。

该库可以以 Type Safe 的方式从 `Record` 中删除字段。但它需要一点魔法。

我们首先要能够做的是在 Types 中指定字段名。我们通过使用 `Symbol` 与 `Proxy` 来实现。

让我们看看 kind `Symbol`：

![](img/8c0e9b687c62642e828ccb5481e11313_1439_0.png)

`Symbol` 让我们能够在 Type 定义中使用 `String` 字面量。

让我们先看看如何使用 `Proxy` 与 `delete`：

```haskell
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody") res) ① ②
```

- ① 从 `Response`，即 `res` 中删除名为 `"writeBody"` 的字段。
- ② `_` 由编译器推断为类型 `Proxy`。

这里有一个使用 `delete` 来提取不存在的字段 `writeBody__` 的日志更改的示例。由于我们在 Type 系统中指定了字段名，而该字段不存在，因此以下内容无法编译：

```haskell
-- COMPILER ERROR!!
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody__") res)
```

它会导致以下错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1439_1.png)

这是因为 `delete` 的 Constraints：

```text
```
