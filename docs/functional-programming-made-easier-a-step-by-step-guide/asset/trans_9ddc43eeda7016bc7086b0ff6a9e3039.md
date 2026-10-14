

```
-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String $ encodeJSON $ LogonRequest { userName, password }
    let logonResponse = do
          { body } <- lmap Ajax.printError ajaxResult
          lmap show $ runExcept $ decodeJSON body :: _ LogonResponse
    case logonResponse of
      Left err -> alertError err
      Right (LogonResponse LogonResultsFailure) -> ①
        alertError "Invalid Logon Credentials" ②
      ???
      pure unit
  where
  alertError :: String -> H.HalogenM State Action Slots Output m Unit
  alertError msg = H.liftEffect $ window >>= alert msg
```

① 匹配 Pattern Right，即成功的 Ajax 调用，但 API 响应为失败。

② 通知用户其提供的凭据无效。

最后，我们需要处理成功的情况。首先，只写 Pattern Match，即 -> 的左侧。然后在此返回。

这里只有这一部分：

```
-- ABOVE CODE REDACTED
    case logonResponse of
      Left err -> alertError err
      Right (LogonResponse LogonResultsFailure) ->
        alertError "Invalid Logon Credentials"
      Right (LogonResponse (LogonResultsSuccess { authToken, mustChangePassword })) -> do ① ②
        ???
      pure unit
-- BELOW CODE REDACTED
```

① 解构以获取 authToken 和 mustChangePassword。

② 启动了一个将在 HalogenM 中运行的 do 块。可能如此。到目前为止很难确定。

我们需要将 authToken 保存到 userRef 中。我们可以使用 ask 从 ReaderT 获取 userRef。并且我们可以使用 Effect.Ref 中的 write 来更新 userRef。

在继续阅读之前写下这两行代码。

以下是这些添加内容：

```
import Control.Monad.Reader.Class (class MonadAsk, ask) ①
import Data.Maybe (Maybe(..))
import Effect.Ref as Ref
import Env (Env)

component
  :: ∀ m
  . MonadAff m
  => MonadAsk Env m ②
  => H.Component Query Input Output m
-- BELOW CODE REDACTED

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
  case logonResponse of
    Left err -> alertError err
    Right (LogonResponse LogonResultsFailure) ->
      alertError "Invalid Logon Credentials"
    Right (LogonResponse (LogonResultsSuccess
      { authToken, mustChangePassword })) -> do
      { userRef } <- ask ③
      H.liftEffect $ Ref.write (Just { authToken }) userRef ④ ⑤
      ???
    pure unit
-- BELOW CODE REDACTED
```

① 添加了这些导入。

② 添加了 MonadAsk 约束。

③ 获取 Env，即 ReaderT 环境，并解构它以获取 userRef。

④ 将 authToken 写入 userRef。不要忘记它是 Maybe。

⑤ 我们需要 liftEffect 这个，因为 do 块是 HalogenM 而 Ref.write 在 Effect 中。

最后，如果 mustChangePassword 为 true，则我们希望导航到 ChangePassword，否则我们将导航到 Users。但我们希望将 Logon 页面与我们的 Routes 解耦。

这就是我们创建 Capability.LogonRoute 的原因。想法是也许我们的 Logon 页面会存在于一个库中。

查看我们在 AppM.purs 中完成的 LogonRoute 实例实现，以帮助你在继续阅读之前添加此最后一步。

以下是最后部分：

```
import Capability.LogonRoute (class LogonRoute, PasswordType(..)
    , logonRoute)
import Capability.Navigate (class Navigate, navigate)

component
  :: ∀ m route
  . MonadAff m
  => MonadAsk Env m
  => Navigate m route
  => LogonRoute m route
  => H.Component Query Input Output m
component = H.mkComponent
-- BELOW CODE REDACTED

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
  case logonResponse of
    Left err -> alertError err
    Right (LogonResponse LogonResultsFailure) ->
      alertError "Invalid Logon Credentials"
    Right (LogonResponse (LogonResultsSuccess
      { authToken, mustChangePassword })) -> do
      { userRef } <- ask
      H.liftEffect $ Ref.write (Just { authToken }) userRef
      if mustChangePassword then
        -- COMPILER ERROR!!
        navigate =<< logonRoute PasswordTemporary
      else navigate =<< logonRoute PasswordPermanent
-- BELOW CODE REDACTED
```

① 添加了这些导入。

② 添加了 route。

③ 添加了 Navigate 能力。

④ 添加了 LogonRoute 能力。

⑤ 如果 mustChangePassword 则我们路由到临时密码应去的地方，即我们的更改密码页面。

⑥ 我们使用 =<< 因为 navigate 和 logonRoute 都是单子函数。

⑦ 否则我们导航到永久密码应路由到的地方，即用户页面。

⑧ 移除了 pure unit。

以下是我们的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1737_0.png)

编译器无法弄清楚 Navigate 的第二个类型是什么。这可以通过错误消息中的 t4 看出。它可以弄清楚第一个类型具有 Navigate 实例，因为它知道 HalogenM 的 Navigate 实例，这也约束了 m 必须具有 Navigate 实例。

但它没有 Type route 可以依附，并且没有办法从 m 得到 route。

我们可以通过告诉编译器第二个类型是什么来修复它：

```
-- ABOVE CODE REDACTED
    if mustChangePassword then
      -- NOT IDEAL!!
      navigate <<= (logonRoute PasswordTemporary :: _ route)
      -- NOT IDEAL!!
    else navigate <<= (logonRoute PasswordPermanent :: _ route)
-- BELOW CODE REDACTED
```

但更好的方法是如果我们不必这样做。我们可以通过在编译器可以弄清楚的 m 和它无法弄清楚的 route 之间创建函数依赖来实现：

```
class Monad m <= Navigate m route | m -> route where ①
  navigate :: route -> m Unit
```

① 添加了 | m -> route。这告诉编译器如果你能弄清楚 m 那么它将暗示一个且只有一个 route。

做出此更改以便我们不需要提供显式的类型注释。

让我们也对 LogonRoute 做同样的更改，以防我们不使用 navigate 使用 logonRoute。我们可能不会在该应用程序中这样做，但这仍然是良好的实践：

```
class Monad m <= LogonRoute m route | m -> route where ①
  logonRoute :: PasswordType -> m route
```

① 也在此处添加了函数依赖，以防我们遇到与 Navigate 相同的类似问题。

现在，我们的编译器错误消失了。

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
  case logonResponse of
    Left err -> alertError err
    Right (LogonResponse LogonResultsFailure) ->
      alertError "Invalid Logon Credentials"
    Right (LogonResponse (LogonResultsSuccess
      { authToken, mustChangePassword })) -> do
      { userRef } <- ask
      H.liftEffect $ Ref.write (Just { authToken }) userRef
      if mustChangePassword then
        navigate =<< logonRoute PasswordTemporary
      else navigate =<< logonRoute PasswordPermanent
-- BELOW CODE REDACTED
```

从此代码更改中后退一步，看看是否可以在继续阅读之前改进 if 表达式。

我能看到的第一件事是我们可以提取 navigate：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REACTED
    case logonResponse of
        Left err -> alertError err
        Right (LogonResponse LogonResultsFailure) ->
            alertError "Invalid Logon Credentials"
        Right (LogonResponse (LogonResultsSuccess
            { authToken, mustChangePassword })) -> do
            { userRef } <- ask
            H.liftEffect $ Ref.write (Just { authToken }) userRef
            navigate <<= if mustChangePassword then
                logonRoute PasswordTemporary
            else logonRoute PasswordPermanent
-- BELOW CODE REACTED
```

如果我们也能提取 logonRoute 就更好了：

```
-- ABOVE CODE REACTED
    navigate <<= logonRoute
        $ if mustChangePassword then PasswordTemporary
        else PasswordPermanent
-- BELOW CODE REACTED
```

注意 bind 变成了使用翻转的鱼运算符 <=< 的 Kleisli 组合。我们本可以保留 bind，但函数组合优于函数应用。

将此更改应用到你的代码中。

接下来，让我们在用户每次成功登录时记录到浏览器的控制台。但是，我们不会使用 log。我们将使用 Log 能力：

