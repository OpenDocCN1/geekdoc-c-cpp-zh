

```
type ResponseM = Aff Response
```

然后继续阅读。

我们想要构建一个以 Aff 为底部的 ReaderT Monad Stack：

```
import Control.Monad.Reader (ReaderT) ①
import Effect.Aff (Aff) ①
import Effect.Aff.AVar (AVar) ①
import HTTPure.Response (Response) ②
import Manager.Account (Accounts) ①

type HandlerEnv = ③
  { accountsAVar :: AVar Accounts
  }

class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle
    :: String
    -> Proxy a
    -> Either MultipleErrors (ReaderT HandlerEnv Aff Response) ④ ⑤
```

① 添加了这些导入。

② 移除了 ResponseM 并替换为 Response。

③ 这是我们的 Handler 环境。请记住 HandlerEnv 是只读的，但 AVar 引用的底层数据结构不是。

④ 在成功解码后，我们返回一个 ReaderT。这需要使用 runReaderT 运行。

⑤ 我们的 Monad Stack 在顶部是 ReaderT，底部是 Aff。

看看我们构建的 Monad Stack：

```
ReaderT HandlerEnv Aff Response
```

在对我们的 Stack 调用 runReaderT 后，我们将剩下 Aff Response。这是一个 ResponseM，HTTPure 函数在其中运行。我们将继续记住这一点。

Monad Stacks 非常冗长，所以让我们做出以下更改来简化它：

```
type Handler = ReaderT HandlerEnv Aff Response ①

class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: String -> Proxy a -> Either MultipleErrors Handler ①
```

① 将 ReaderT 部分提取为 Handler。这样好多了，尤其是因为我们的所有处理器都将使用此定义，并且它会清理这些类型签名。

现在，返回 Handler.Api.Logon 并注意编译器错误。如果不存在，则保存文件，如果你在 VSCode 中，你会看到它。

这是因为我们更改了 handle 的类型签名。在继续之前修复它。

我们只需要修复 Logon 的 handle 函数：

```
import Handler.Class.ApiHandler (class ApiHandler, Handler) ① ②

handler :: LogonRequest -> Handler
handler _ = do
  HTTPure.notFound
```

① 将 Handler 添加到导入列表。

② 删除了 HTTPure.Response 的导入，因为我们不再使用 ResponseM。

注意我们没有更改 HTTPure.notFound 行。这是因为 notFound 的类型签名：

```
notFound :: ∀ m. MonadAff m => m Response
```

它在任何具有 MonadAff 实例的 Monad 中运行。我们的旧 Monad Aff 和我们新的 ReaderT 都有 MonadAff 实例。因此，无需更改代码的这一部分。

现在 handler 是一个 ReaderT，我们可以请求 accountsAvar，verifyLogon 需要它。在继续阅读之前将该代码添加到 handler。

以下是添加的内容：

```
```haskell
import Control.Monad.Reader.Class (ask) ❶

handler :: LogonRequest -> Handler
handler _ = do
  { accountsAVar } <- ask ❷ ❸
  HTTPure.notFound
```
```

+   ❶ 导入 `ask`。
+   
+   ❷ 对 `HandlerEnv` 进行解构，只取出 `accountsAVar`。我们将需要它用于 `verifyLogon`。
+   
+   ❸ 编译器会抱怨我们没有使用 `accountsAVar`。不用担心。我们会用到它。

接下来，将对 `verifyLogon` 的调用添加到 `handler`，然后在此返回。

首先，让我们看看 `verifyLogon`：

```
```haskell
verifyLogon :: AVar Accounts -> String -> String -> Aff (Maybe Account)
verifyLogon accountsAVar userName password = do
...
```
```

我们应该首先对 `handler` 的第一个参数进行解构，以公开 `verifyLogon` 所需的 `userName` 和 `password`：

```
```haskell
import Data.Api.Logon (LogonRequest(..)) ❶

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do ❷
  { accountsAVar } <- ask
  HTTPure.notFound
```
```

+   ❶ 添加了 Data 构造子的导入。
+   
+   ❷ 使用模式匹配进行解构。

接下来，我们将调用 `verifyLogon` 并相应地响应：

```
import Manager.Account (verifyLogon) ①
import Data.Maybe (Maybe(..))

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
    { accountsAVar } <- ask
    case verifyLogon accountsAVar userName password of
        Nothing -> ???
```

① 添加这两个导入。

在此停止并处理对 verifyLogon 的调用的错误情况和成功情况。然后返回此处并继续阅读。

对于错误情况，我们将使用 LogonResultsFailure 响应：

```
import Data.Api.Logon (LogonRequest(..)
    , LogonResponse(..), LogonResults(..)) ① ②

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
    { accountsAVar } <- ask
    case verifyLogon accountsAVar userName password of
        Nothing -> LogonResponse LogonResultsFailure ③
        ???
```

① 为 LogonRequest 添加了 (..) 以导入数据构造子。

② 添加了 LogonResponse 和 LogonResults 及其数据构造子。

③ 失败情况。

现在是成功情况：

```
import Entity.Account (Account(..)) ①
import Data.UUID (emptyUUID) ②

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
    { accountsAVar } <- ask
    case verifyLogon accountsAVar userName password of
        Nothing -> LogonResponse LogonResultsFailure
        Just (Account { temporaryPassword }) -> LogonResponse
            $ LogonResultsSuccess
            { authToken: emptyUUID -- TODO get from Session Mgr ③
            , mustChangePassword: temporaryPassword ④
            }
    ???
```

① 导入 Account 数据构造子以进行模式匹配。

② 暂时导入 emptyUUID。

③ 我们最终会调用 Session Manager 为我们创建一个 Session，它将返回一个 authToken。我们现在使用 emptyUUID。

④ 如果文件上的密码是临时的，则 mustChangePassword 为 true。

此时，我们已经编写了 case 表达式，但我们没有对它做任何事情。这个表达式是响应。所以，我们可以在编码后用它进行响应。

添加编码响应的代码，即 case 表达式，然后使用 HTTPure.ok 进行响应。完成后返回此处。

以下是该添加：

```
import Foreign.Generic (decodeJSON, encodeJSON) ①

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
    { accountsAVar } <- ask
    HTTPure.ok $ encodeJSON ②
        $ case verifyLogon accountsAVar userName password of
            Nothing -> LogonResponse LogonResultsFailure -- COMPILER ERROR!!
            Just (Account { temporaryPassword }) -> LogonResponse
                $ LogonResultsSuccess
                { authToken: emptyUUID -- TODO get from Session Mgr
                , mustChangePassword: temporaryPassword
                }
```

① 将 encodeJSON 添加到导入列表。

② 首先对响应进行编码，然后将其发送给客户端。

编译器错误是：

![](img/8c0e9b687c62642e828ccb5481e11313_1399_0.png)

它试图用 Aff 模式匹配 Maybe。你能看出我的错误吗？

我忘了 verifyLogon 在 Aff 中运行。如果是你没忘的话，很好。

让我们修复我的错误：

```
import Control.Monad.Trans.Class (lift) ①

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
  { accountsAVar } <- ask
  verifiedAccount <- lift $ verifyLogon accountsAVar userName password ②
  HTTPure.ok $ encodeJSON $ case verifiedAccount of ③
    Nothing -> LogonResponse LogonResultsFailure
    Just (Account { temporaryPassword }) -> LogonResponse
      $ LogonResultsSuccess
        { authToken: emptyUUID -- TODO get from Session Mgr
        , mustChangePassword: temporaryPassword
        }
```

① 导入 lift。

② 我们需要在这里提升，因为 verifyLogon 在我们的 Monad Stack 的底部运行，即在 Aff 中。由于我们只有 2 层，所以只需要提升一次。

③ 对 verifiedAccount 的提取结果进行 case 分析。

现在它可以编译了。

为了能够测试它，我们需要从 main 函数到 handler。这意味着

我们将不得不完善我们的 `router`。

## 28.7.5. 完善 `router`

这是我们在 `Main` 模块中对 `router` 的进展：

```
router :: Request -> ResponseM
router _ = HTTPure.notFound
```

`router` 需要尝试每个 `ApiHandler` 直到找到一个成功的，然后它将对 `handle` 调用 `runReaderT`。这将返回一个 `ResponseM` 或，更准确地说，一个 `Aff Response`。

让我们从找到成功的处理器的代码开始。

在编码此代码之前，让我们回顾几件事。首先，来自 `Data.Foldable` 的 `oneOf`：

```
-- Combines a collection of elements using the Alt operation.
oneOf :: ∀ f g a. Foldable f => Plus g => f (g a) -> g a
```

+   1. 对我们来说，这里 `f` 将是 `Array`。
+   2. 对我们来说，这里 `g` 将是 `Either`。

所以，现在让我们看看 `Either` 的 `Alt` 实现：

```
-- | The `Alt` instance allows for a choice to be made between
-- | two `Either` values with the `<|>` operator,
-- | where the first `Right` encountered is taken.
-- |
-- | ``` purescript
-- | Right x <|> Right y == Right x
-- | Left x <|> Right y == Right y
-- | Left x <|> Left y == Left y
-- | ```
instance altEither :: Alt (Either e) where
  alt (Left _) r = r
  alt l        _ = l
```

这意味着 `oneOf` 将使用来自 `Either` 的 `Alt` 实现，因此第一个成功的 `Either` 将被选中。

我们可以使用 `oneOf` 来“尝试”每个处理器，并且编码它的那个将产生一个将被选中的 `Right`。在该 `Right` 中将是我们的 API 响应。

