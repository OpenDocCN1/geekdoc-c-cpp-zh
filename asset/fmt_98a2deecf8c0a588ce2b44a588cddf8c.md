
然后对 `Main` 进行以下更改：

```
import Debug (spy)

router :: HandlerEnv -> Request -> ResponseM
router env { body, method }
  | method == HTTPure.Post =
      let handlers =
          handle (Proxy :: _ Logon) :| [
          handle (Proxy :: _ Logoff)
          ] <#>
            (_ $ body) in
      case hush <<< (head $ spy "req" $ oneOf handlers) of ①
        Nothing -> HTTPure.badRequest body
        Just reader -> runReaderT reader env
  | otherwise = HTTPure.methodNotAllowed
```

① 注意 `spy "req"` 在 `head` 调用之前。如果我们把它放在之后，那么我们只会在控制台中打印出第一个解码错误。那一个将是 `Logon` 的失败解码，我们期望在发送 `Logoff` 时它会失败。通过把它放在这里，我们将获得所有错误。

停止服务器并重新运行你的程序。这次只需从 Postman 发送 `LogoffRequest`，因为 `authToken` 无关紧要，因为我们怀疑我们因解码问题而失败。得到结果后返回这里。

这里是我得到的结果：

```text
req: [ Left {
    value0:
      NonEmpty {
        value0:
          ErrorAtProperty {
            value0: 'tag',
            value1: ForeignError { value0: 'Expected "LogonRequest" tag' } },
        value1: Nil {} } }, ①
  Right { value0: [Function] } ] ②
```

① 我们不期望 `Logon` 解码器能工作，而且它确实没有。

② 看起来 `Logoff` 解码器工作了。

如果解码工作了，那么问题是什么？看看 `router` 的代码，看看你是否能发现其他错误。

在研究了 `router` 代码后，我可以看到使用 `head` 是错误的方法。你能看出为什么吗？

当我们只有一个处理程序时，使用 `head` 是可以的，但现在，我们必须在所有可能的情况中寻找一个成功的情况。这里是 `oneOf` 的类型签名，可以看出原因：

```
oneOf :: ∀ f a. Alternative f => NonEmpty f a -> f a ①
```

① `oneOf` 返回 `f a`，对于我们来说是 `Array (Either MultipleErrors Handler)`。我们真正想要的只是第一个成功的 `Either MultipleErrors Handler`。我认为我错误地以为 `f` 是 `Either`。仔细考虑的话，我就会意识到 `Either` 不能是 `Alternative`，因为它没有 `Plus`，而 `Plus` 是 `Alternative` 的超类。

很明显 `oneOf` 是错误的方法。我们这样做是因为我们不能/没能使用 `Data.Foldable` 中的 `oneOf`，因为 `Either` 没有 `Plus` 实例。我们真正想要的是这个函数的行为，而不是我们最终选择的那一个。

我犯的错误是没有意识到 `oneOf` 使用 `<|>` 用于 `f`，在我们的例子中是 `Array`，而不是 `a`，在我们的例子中是 `Either`。`Array` 的 `<|>` 只是连接。这不是我们想要的。

要修复这个问题，我们必须编写自己的 `oneOf`，它提供 `Data.Foldable` 中 `oneOf` 的行为，但只适用于 `NonEmpty` 可折叠类型。这样我们就不需要使用 `Plus` 约束，因为我们的列表永远不会为空。

让我们一起写这个。在此之前，先注释掉使用旧 `oneOf` 的 `router` 代码暂时，因为我们将破坏它，我们不希望编译器错误被 `router` 中损坏的代码掩盖：

```
router :: HandlerEnv -> Request -> ResponseM
router env { body, method }
  -- | method == HTTPure.Post =
  --   let handlers =
  --           handle (Proxy :: _ Logon) :| [
  --           handle (Proxy :: _ Logoff)
  --         ] <#> (_ $ body) in
  --   case hush <=< (head $ spy "req" $ oneOf handlers) of
  --     Nothing -> HTTPure.badRequest body
  --     Just reader -> runReaderT reader env
| otherwise = HTTPure.methodNotAllowed
```

现在，我们将从始终以类型签名开始编写 `oneOf`：

```
import Data.NonEmpty (NonEmpty, (:|)) ① ②

oneOf :: ∀ a e f. NonEmpty f (Either e a) -> Either e a
```

① 将 `NonEmpty` 添加到导入列表中。

② 从导入列表中移除了 `oneOf`。

我们有一个 `Either` 的 `NonEmpty f`。在我们的例子中，是一个 `Partially Applied` 调用 `handle` 的 `NonEmpty Array`：

```
let handlers =
      handle (Proxy :: _ Logon) :| [
      handle (Proxy :: _ Logoff)
    ] <#> (_ $ body) in
```

然后我们将 `body` 的应用映射到 `NonEmpty Array` 上，留下通过每个处理器处理请求的结果。只有 1 个处理器会成功，如果有的话，因为请求是唯一的。

是我们想要对这些 `Either` 进行折叠 `<|>`。这将产生第一个 `Right`，即第一个成功的结果，例如：

```
foldl (<|>) [Left 1, Right "yes", Left 2] (Left 99) -- Right "yes" ①
```

① `Left 99` 是我们对 `foldl` 的初始值。

这等价于：

```
Left 99 <|> Left 1 <|> Right "yes" <|> Left 2 -- Right "yes"
```

但如果我们要执行 `foldl`，我们就需要一个初始值。幸运的是，我们使用的是 `NonEmpty`，它总是至少有一个头值。

我们现在将对 `NonEmpty` 进行模式匹配以获取头和尾：

```
oneOf :: ∀ a e f. NonEmpty f (Either e a) -> Either e a
oneOf (x :| xs) = ???
```

现在，我们想要对 `Either` 进行折叠 `<|>`。这将选择第一个 `Right`：

```
import Control.Alt ((<|>)) ①
import Data.Foldable (class Foldable, foldl)

oneOf :: ∀ a e f. Foldable f => NonEmpty f (Either e a) -> Either e a ②
oneOf (x :| xs) = foldl (<|>) x xs ③ ④
```

① 添加了这些导入。

② 现在我们要在 `NonEmpty` 上对 `f` 进行折叠，因此必须将 `f` 约束为 `Foldable`。

③ `x` 是初始值，即 `NonEmpty` 的头。

④ 从这行代码中，应该非常清楚为什么我们需要 `NonEmpty`。对于 `Either`，没有 `Plus`。我们不能对空的 `Either` 数组执行 `foldl`，因为没有来自 `Plus` 的空值可用于作为 `foldl` 函数的初始值。使用 `NonEmpty`，我们总是有头，在本例中是 `x`，作为初始值。

正如始终一样，仅因为此函数可以编译，并不意味着我们已经完成。你能看到 `oneOf` 有什么改进吗？

我认为我们应该通过抽象 `Either e` 为具有 `Alt` 实例的 `t` 来使其更通用：

```haskell

import Control.Alt (class Alt, (<|>))

oneOf :: ∀ a t f. Alt t => Foldable f => NonEmpty f (t a) -> t a

oneOf (x :| xs) = foldl (<|>) x xs

```

1. 将 `Alt` 类添加到导入列表中。
2. 添加了 `Alt t` 约束。
3. 用 `t` 替换了 `Either e`。

现在你可以移除以下导入：

```haskell

import Data.Array (head)

import Debug (spy)

```

然后取消注释 `router` 中的代码并按如下方式更改 `router`：

```haskell

router :: HandlerEnv -> Request -> ResponseM

router env { body, method }

  | method == HTTPure.Post =

      let handlers =

            handle (Proxy :: _ Logon) :|

            [ handle (Proxy :: _ Logoff)

            ] <#> (_ $ body) in

      case hush $ oneOf handlers of

        Nothing -> HTTPure.badRequest body

        Just reader -> runReaderT reader env

  | otherwise = HTTPure.methodNotAllowed

```

1. 我们现在使用的是我们的 `oneOf`，这简化了这行代码，因为它完成了我们需要的一切。我们仍然 `hush` 该 `Either`。
2. 不要忘记将 `bind` 更改为 `apply`，即 `$`。

现在，运行服务器并发送 `LogoffRequest` 看看会发生什么。然后返回这里。

我得到的是：

```json

{"contents":{"tag":"LogoffResultsFailure"},"tag":"LogoffResponse"}

```

这很棒。这是意料之中的，因为我们从未登录过。

现在，先发送 `LogonRequest`，然后从 `Response` 中复制出 `authToken` 并放入 `LogoffRequest` 看看是否现在完全有效。然后继续阅读。

我仍然得到：

```
{"contents":{"tag":"LogoffResultsFailure"},"tag":"LogoffResponse"}
```

那么，还可能有什么问题？查看 `Logoff` 的处理器，看看你是否能看到导致 `LogoffResultsFailure` 的条件。然后返回这里继续阅读。

当我进行此调查时，我发现 `LogoffResultsFailure` 仅在 `Session` 未通过验证时才发送给客户端。

这告诉我 `verifySession` 可能有问题。查看它，看看你是否能发现可能有问题的地方。然后继续阅读。

让我们一起看实现：

```
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar ①
  sessions <- AVar.take sessionsAVar
  now <- getTime <$> liftEffect now
  case Map.lookup authToken sessions of
    Nothing -> AVar.put sessions sessionsAVar *> pure Nothing
    Just (Session session) -> do
      let newSession = Session $ session { lastTime = now }
          newSessions = Map.insert authToken newSession sessions
      AVar.put newSessions sessionsAVar
      pure $ Just newSession
```

① 过期任何不活跃的 `Session`。

它做的第一件事就是过期旧的 `Session`。我怀疑这是否是个问题。也许我们的 `Session` 过期太快了。

向 `Manager.Session` 添加调试，然后相应地修改 `expireSessions`：

```
import Debug (spy) ①

expireSessions :: AVar Sessions -> Aff Unit
expireSessions sessionsAVar = do
  now <- getTime <$> liftEffect now
  sessions <- AVar.take sessionsAVar
  AVar.put
    (spy "expired" $ Map.filter ②
      (\(Session { lastTime }) -> now - lastTime > sessionTimeout)
      sessions)
    sessionsAVar
```

① 添加了导入。

② 打印过滤后剩余的所有 `Session`，以移除旧的。

然后再次运行服务器，先发送 `LogonRequest` 然后发送 `LogoffRequest`。你发送 `LogoffRequest` 时使用什么 `authToken` 都无关紧要，因为我们只关心在 `expireSessions` 中转储所有 `Session`。

发送 `LogoffRequest` 后，搜索控制台中的 `expired` 并在找到后继续阅读。

我得到的是：

```
expired: Leaf {} ①
```

① `Leaf {}` 是空 `Map` 的内部表示。

看起来我们过期得太早了。查看代码，看看你是否能发现我的逻辑错误。然后返回这里。

我看到了。逻辑是反的。我们想要保留空闲时间少于 `sessionTimeout` 的会话，而不是更多：

```
expireSessions :: AVar Sessions -> Aff Unit
expireSessions sessionsAVar = do
  now <- getTime <$> liftEffect now
  sessions <- AVar.take sessionsAVar
  AVar.put
    (spy "expired" $ Map.filter
      (\(Session { lastTime }) -> now - lastTime < sessionTimeout) ①
      sessions)
    sessionsAVar
```

① 将 `>` 改为 `<`。

重新运行服务器，再次只发送一个 `LogoffRequest` 看看你现在得到什么。

我得到：

```
expired: Two {
    value0: Leaf {},
    value1: '6698cd9d-def3-4aa8-a3ca-c4bc8b087fc8',
    value2:
    { authToken: '6698cd9d-def3-4aa8-a3ca-c4bc8b087fc8',
      lastTime: 1602174302071 },
    value3: Leaf {} }
```

这更像了。现在，移除 `import Debug` 和 `spy` 代码。还从 `spago.dhall` 中移除调试。

然后重新运行服务器并进行适当的测试，复制 `authToken` 看看现在会发生什么。

我得到的是：

```
{"contents":{"tag":"LogoffResultsSuccess"},"tag":"LogoffResponse"}
```

成功！！

## 28.10.2. 编码 CreateUserRequest API 处理器

让我们回顾一下我们的图表，特别关注 `CreateUser`：

![](img/8c0e9b687c62642e828ccb5481e11313_1487_0.png)

我们可以看到 `CreateUser` 被标记在 2 条箭头上。一条从 API Handler 到 Account Manager，另一条从 API Handler 到 Account Handler。

Account Handler 需要 APPEND 一个新的 `Account` 记录到 `accounts.csv` 中。而 Account Manager 需要将新的 `User` 添加到 `accountsVar` 中。

让我们再次看看 `Account` 和 `User` 之间的区别：

```fsharp

type UserRow r =

  ( userName :: String

  , temporaryPassword :: Boolean
```

