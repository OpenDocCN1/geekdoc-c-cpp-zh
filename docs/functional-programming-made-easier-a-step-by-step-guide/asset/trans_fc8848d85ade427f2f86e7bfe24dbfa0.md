

handleAction。完成后返回此处。

以下是组件的类型签名：

```
import Capability.Navigate (class Navigate) ①
import Data.Route (Route)
import Effect.Aff.Class (class MonadAff)

component
  :: ∀ m
  . MonadAff m ②
  => Navigate m Route ③
  => H.Component Query Input Output m
```

① 添加了这些导入。

② 我们的 Monad，m，最终将在 Aff 中运行。

③ 我们知道当用户选择不同用户时需要进行导航，因此我们需要从我们的 Monad，m 中获得此 Capability。

现在是实现部分：

```
import Data.Maybe (Maybe(..)) ①

component
  :: ∀ m
  . MonadAff m
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ ->
      { authorized: false ②
      , selectedUser: Nothing
      , users: []
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , initialize = Just Initialize ③
      }
  }
where
???
```

① 添加了 ( . . ) 以包含 Data 构造子。

② 我们现在将 State 初始化为未授权、无所选用户和无用户。Initialize 将正确设置这些，因为它可以执行效果来获取已登录用户并查询后端以获取用户。

③ 使用 Action Initialize 处理 initialize。

而现在是存根代码：

```
-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> pure unit

render :: State -> H.ComponentHTML Action Slots m
render _ = HH.text ""
```

让我们为如何编写 Initialize 制定一个计划：

+   - 从 LoggedOnUser 获取 authToken
+   - 仅当用户是管理员时调用服务器查询用户
+   - 等待。等待。

我们不知道用户是否是管理员。我们如何获取此信息？

让我们查看 LoggedOnUser：

```
type LoggedOnUser =
  { authToken :: UUID
  }
```

目前，我们没有此信息。

接下来，让我们查看我们从哪里获取此信息，即我们服务器中的 LogonResponse：

```
data LogonResults
  = LogonResultsSuccess
    { authToken :: UUID
    , mustChangePassword :: Boolean
    }
  | LogonResultsFailure
```

应该很清楚我们缺少一个关键信息来完成此页面的代码。

返回到 `server` 代码并在我们将 `authToken` 放入 `LogonResponse` 的位置，让我们也添加 `admin`。在阅读后续内容之前先进行此更改。

首先要做的是向 `LogonResponse` 添加一个 `admin` 字段：

```
data LogonResults
  = LogonResultsSuccess
      { authToken :: UUID
      , admin :: Boolean
      , mustChangePassword :: Boolean
      }
  | LogonResultsFailure
```

❶ 向 Record 添加了 `admin`。

接下来，我们将更新 `Handler.Api.Logon` 中的 Logon API 处理程序：

```
handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
  { accountsAVar, sessionsAVar } <- ask
  verification <- lift $ verifyLogon accountsAVar userName password
  response <- case verification of
    Nothing -> pure $ logonResponse LogonResultsFailure
    Just (Account { admin, temporaryPassword }) -> do
      authToken <- lift $ createSession sessionsAVar userName
      pure $ LogonResponse
        $ LogonResultsSuccess
          { authToken
          , admin
          , mustChangePassword: temporaryPassword
          }
  HTTPure.ok $ encodeJSON response
```

❶ 从 `Account` 中解构时添加了 `admin`。

❷ 在响应中添加了 `admin`。

现在，使用 `Ctrl-C` 终止服务器并使用以下命令重新运行它：

```
npx spago run
```

服务器运行后，返回到 `client` 项目并构建它，以便编辑器会看到我们对服务器代码中 LogonResultsSuccess 所做的更改：

```
make build
```

现在向 LoggedOnUser 添加 admin 标志，然后返回此处。

以下是该更改：

```
type LoggedOnUser =
  { authToken :: UUID
  , admin :: Boolean ①
  }
```

① 添加了 admin。

最后，在我们初始化 LoggedOnUser 时添加 admin 值。完成后返回此处。

以下是 Component.Logon 中 handleAction 中的该更改：

```
-- ABOVE CODE REDACTED
    case logonResponse of
      Left err -> alertError err
      Right (LogonResponse LogonResultsFailure) ->
        alertError "Invalid Logon Credentials"
      Right (LogonResponse (LogonResultsSuccess
        { authToken, admin, mustChangePassword })) -> do ①
        log <<= logEntry Info "User logged on"
        { userRef } <- ask
        H.liftEffect $ Ref.write (Just { admin, authToken }) userRef ②
        navigate <<= logonRoute
          $ if mustChangePassword then PasswordTemporary
            else PasswordPermanent
-- BELOW CODE REDACTED
```

① 在 LogonResultsSuccess 的解构中添加了 admin。

② 将 admin 添加到 LoggedOnUser。

现在，让我们以稍有不同的视角返回到为 Component.Users 中的 Initialize 编码制定计划：

+   - 从 LoggedOnUser 获取 authToken
+   - 如果 LoggedOnUser 无权查看此页面则不执行任何操作
+   - 调用服务器查询用户
+   - 相应地更新 State

现在，编写 Initialize 的代码以查询后端以获取用户并初始化 State。从我们在 Logon 页面上所做的工作中窃取代码以向后端发出 API 调用。

现在暂时使用相同的 alertError 函数处理错误。我们将在下一节创建 Modal Dialog 组件时替换它。

然后在你卡住或准备继续时返回此处。

我们将从以下代码开始编码：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    ???
```

现在，我们需要检查 LoggedOnUser，我们可以从 ReaderT 环境中获取它：

```
import Control.Monad.Reader.Class (class MonadAsk, ask) ①
import Effect.Ref as Ref
import Env (Env)

component
  :: ∀ m
  . MonadAff m
  => MonadAsk Env m ②
  => Navigate m Route
  => H.Component Query Input Output m
-- BELOW CODE REDACTED

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask ③
    loggedOnUser' <- H.liftEffect $ Ref.read userRef ④
    ???
```

① 添加了这些导入。

② 添加了此约束，以便我们可以调用 ask。

③ 从环境中获取 userRef。

④ 读取 Ref 以获取其中存储的值，即 Maybe LoggedOnUser。请注意它是 Maybe。这就是我用 Prime 为其命名的原因，以提醒自己此变量存在问题。

现在，我们需要处理 Maybe：

```
import Data.Maybe (Maybe(..), maybe) ①

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } -> ② ③
      ???
```

① 将 maybe 添加到导入列表。

② 如果没有已登录用户则不执行任何操作。这永远不应该发生，因为当出现这种情况时，我们的 Router 组件会重定向到 Logon 页面。

③ 在 Just 情况下，我们的 Lambda 解构 LoggedOnUser。

如果你卡住了并且觉得可以完成，请在此停止并尝试一下。准备继续时返回此处。

我们只想在用户有权访问时才查询用户，即管理员：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        ????
```

现在我们只需复制 Logon 页面 handleAction 中所做的一段代码：

```
import Affjax as Ajax ①
import Affjax.ResponseFormat as ResponseFormat
import Affjax.RequestBody as RequestBody
import Control.Monad.Except (runExcept)
import Data.Api.QueryUsers (QueryUsersRequest(..), QueryUsersResponse(..)
                         , QueryUsersFailureReason(..)
                         , QueryUsersResults(..))

import Data.Bifunctor (lmap)
import Data.Either (Either(..))
import Foreign.Generic (encodeJSON, decodeJSON)

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string ②
          "http://localhost:3000/"
          $ Just $ RequestBody.String
          $ encodeJSON $ QueryUsersRequest { authToken } ③
        let queryResponse = do ④
              { body } <- lmap Ajax.printError ajaxResult
              lmap show $ runExcept
              $ decodeJSON body :: _ QueryUsersResponse ⑤
        case queryResponse of ④
          Left err -> alertError err
          ???
```

① 添加了这些导入。

② 从此处向下，代码是从 Logon 页面的 handleAction 复制的。

③ 将请求从 LogonRequest 更改为 QueryUsersRequest。

④ 在这些位置将 logonResponse 重命名为 queryResponse。

⑤ 将 LogonResponse 更改为 QueryUsersResponse。

这种编码方式，即复制/粘贴编码，始终是一个危险信号。我们将在完成此函数后将这段代码提取出来。

现在，我们唯一需要做的就是处理 2 个响应情况：

