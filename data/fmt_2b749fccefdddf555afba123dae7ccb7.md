
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

② 从此处向下，代码是从 `Logon` 页面的 `handleAction` 复制的。

③ 将请求从 `LogonRequest` 更改为 `QueryUsersRequest`。

④ 在这些位置将 `logonResponse` 重命名为 `queryResponse`。

⑤ 将 `LogonResponse` 更改为 `QueryUsersResponse`。

这种编码方式，即复制/粘贴编码，始终是一个危险信号。我们将在完成此函数后将这段代码提取出来。

现在，我们唯一需要做的就是处理 2 个响应情况：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
          "http://localhost:3000/"
          $ Just $ RequestBody.String
          $ encodeJSON $ QueryUsersRequest { authToken }
        let queryResponse = do
              { body } <- lmap Ajax.printError ajaxResult
              lmap show $ runExcept
                $ decodeJSON body :: _ QueryUsersResponse
        case queryResponse of
          Left err -> alertError err
          Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
            ???
          Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) -> do
            ???
```

现在，针对失败的情况，我们将弹出一个错误提示：

```
-- ABOVE CODE REDACTED
    case queryResponse of
      Left err -> alertError err
      Right (QueryUsersResponse
        (QueryUsersResultsFailure { reason })) ->
        alertError $ "Query Users: " <> case reason of ①
          NotAuthorized -> "Not Authorized"
          NotAuthenticated -> "Not Authenticated"
      Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) -> do
        ???
```

① `QueryUsersFailureReason` 有 2 个可能的值。

接下来，我们在成功的情况下更新 `State`：

```
-- ABOVE CODE REDACTED
    case queryResponse of
        Left err -> alertError err
        Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
        alertError $ "Query Users: " <> case reason of
            NotAuthorized -> "Not Authorized"
            NotAuthenticated -> "Not Authenticated"
        Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) ->
            H.modify_ _ { authorized = true, users = users }
```

① 移除了 `do`，因为这里只有一行代码。

② 我们已经检查过，确保他们有权限查看此页面，因此 `authorized` 为 `true`。

③ 设置 `users`。

最后，我们先复制粘贴 `alertError`，因为最终我们会把它丢弃掉：

```
import Web.HTML.Window (alert) ①
import Web.HTML (window)

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
          $ encodeJSON $ QueryUsersRequest { authToken }
        let queryResponse = do
            { body } <- lmap Ajax.printError ajaxResult
            lmap show $ runExcept
              $ decodeJSON body :: _ QueryUsersResponse ③
        case queryResponse of
          Left err -> alertError err
          Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
            alertError $ "Query Users: " <> case reason of
              NotAuthorized -> "Not Authorized"
              NotAuthenticated -> "Not Authenticated"
          Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) ->
            H.modify_ _ { authorized = true , users = users }
  where
  alertError :: String -> H.HalogenM State Action Slots Output m Unit ④
alertError msg = H.liftEffect $ window >>= alert msg
```

① 添加了这些导入。

② 这是我们复制粘贴块的开始。

③ 这是我们复制粘贴块的结尾。

④ 从 `'Logon'` 复制而来。

现在，让我们来处理这个函数中一大段代码的糟糕复制粘贴操作。把我们从 `Logon` 页面复制的代码提取成一个名为 `apiCall` 的函数。

先写出不带类型签名的 `apiCall`，让编译器帮你确定它。当你准备好继续时，再回到这里。

我们首先只是把 `handleAction` 中的代码块复制粘贴过来：

```
apiCall = do
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken }
    -- COMPILER ERROR!!
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
```

编译器错误告诉我们，我们需要返回一些东西：

```
apiCall = do
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken } -- COMPILER ERROR!!
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
    pure queryResponse ①
```

① 我们现在暂时返回这个响应。

新的编译器错误告诉我们，需要传入 `authToken`：

```
-- COMPILER WARNING!!
apiCall authToken = do ①
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String
        $ encodeJSON $ QueryUsersRequest { authToken }
    let queryResponse = do
        { body } <- lmap Ajax.printError ajaxResult
        lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
    pure queryResponse
```

① 添加了 `authToken` 参数。

现在，它可以编译了。但在处理类型签名之前，我们可以简化返回代码。注意，我们定义了一个名为 `queryResponse` 的变量，仅仅是为了通过 `pure queryResponse` 返回它。让我们去掉这个变量：

```
— COMPILER WARNING!!
apicall authToken = do
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON $ QueryUsersRequest { authToken }
pure do ❶
  { body } <- lmap Ajax.printError ajaxResult
  lmap show $ runExcept $ decodeJSON body :: _ QueryUsersResponse
```

> ❶ 请记住，这个 `do` 代码块是一个 `Either`。

编译器警告正在告诉我们类型签名应该是什么，所以我们要把它加上：

```
import Data.UUID (UUID) ❶

apiCall :: ∀ t132
  . Bind t132
  => MonadAff t132
  => UUID
  => t132 (Either String QueryUsersResponse)
— BELOW CODE REDACTED
```

> ❶ 添加了这个导入。

看起来 `t132` 是一个 `Monad`。你的编号可能会有所不同。由于 `MonadAff` 要求 `t132` 是一个 `Monad`，所以我们要移除 `Bind`。我们还将把它重命名为 `m`：

```
apiCall :: ∀ m
  . MonadAff m
  => UUID
  => m (Either String QueryUsersResponse)
```

在这一点上，我们可以看到这个函数的多态性还不够。它只能与 `QueryUsersRequest` 一起使用。让我们来修复它：

```
apiCall :: ∀ request response m ①
  . MonadAff m
  => UUID
  -> request ②
  -> m (Either String response) ③
apiCall authToken request = do ②
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON request -- COMPILER ERROR!! ④
  pure do
    { body } <- lmap Ajax.printError ajaxResult
    lmap show $ runExcept $ decodeJSON body :: _ response ⑤
```

① 添加了 `request` 和 `response`。

② 添加了 `request` 参数。

③ 将单态类型参数从 `QueryUsersResponse` 改成了多态类型 `response`。

④ 对传入的 `request` 进行编码。

⑤ 现在的解码类型是多态类型 `response`。

编译器报错是因为我们没有 `request` 的 `Encode` 实例。因此，我们需要通过一个约束（Constraint）来要求它：
