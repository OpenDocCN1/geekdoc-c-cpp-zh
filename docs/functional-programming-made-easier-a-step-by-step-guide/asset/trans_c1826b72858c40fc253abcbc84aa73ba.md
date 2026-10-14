

-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get
    logonResponse <- apiCall (LogonRequest { userName, password })
    case logonResponse of
      Left err -> H.modify_ _ { errorMessage = Just err } ①
      Right (LogonResponse LogonResultsFailure) ->
        H.modify_ _ { errorMessage = Just "Invalid Logon Credentials" } ①
      Right (LogonResponse (LogonResultsSuccess
        { authToken, admin, mustChangePassword })) -> do
        log <<= logEntry Info "User logged on"
        { userRef } <- ask
        H.liftEffect $ Ref.write (Just { admin, authToken }) userRef
        navigate <<= logonRoute
          $ if mustChangePassword then PasswordTemporary
            else PasswordPermanent
-- BELOW CODE REDACTED

① 在这 2 处设置 errorMessage，我们之前在这里调用 alertError

我们现在可以删除以下行：

```
import Web.HTML.Window (alert)
import Web.HTML (window)

where
alertError :: String -> H.HalogenM State Action Slots Output m Unit
alertError msg = H.liftEffect $ window >>= alert msg
```

接下来，我们将添加一个 Action 来封装来自 Modal 的 Output：

```
data Action
  = Logon
  | Input (State -> State)
  | Modal (Modal.Output Message.Output) ①
```

① 我们将 Modal 的 Output 传递给 Action。

我们需要在 handleAction 中处理 Modal Action：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
    Modal output -> case output of
        Modal.Affirmative -> H.modify_ _ { errorMessage = Nothing } ①
        Modal.Negative -> H.modify_ _ { errorMessage = Nothing } ①
        Modal.InnerOutput _ -> pure unit ②
-- BELOW CODE REDACTED
```

① 无论用户点击 Affirmative 还是 Negative 按钮，都隐藏 Modal 对话框。

② 我们的 Message Modal 组件不输出任何内容。

最后我们将更改 render，首先解构 errorMessage：

```
render :: State -> H.ComponentHTML Action Slots m
render { userName, password, errorMessage } =
-- BELOW CODE REDACTED
```

然后将 Modal 组件作为最后一个元素添加：

```
import Data.Maybe (Maybe(..), maybe) ①

-- ABOVE CODE REDACTED
    , (errorMessage # maybe (HH.text "") \message -> ②
        HH.slot _modal unit
            (Modal.component Message.component) message Modal) <3> ④ ⑤
    ]
    where logonDisabled = trim userName == "" || trim password == ""
```

① 将 maybe 添加到导入列表中。

② 当我们没有错误消息时，我们使用一个空的 Text 节点。否则，我们创建 Modal 子组件。

③ 我们将 Message 组件作为 Modal 的内部组件传递。

④ 注意我们如何将 message 作为输入传递给 Modal，即使它没有定义自己的输入类型。那是因为它的输入类型与内部组件的输入类型相同。

⑤ 使用 HH.slot 的最后一个参数在此处处理 Modal 输出。

此时，你可以重新构建应用程序：

```
make build
```

接下来，尝试使用无效凭据登录。

你应该会看到：

![](img/8c0e9b687c62642e828ccb5481e11313_1825_0.png)

现在轮到你了。利用我们在 Logon 中所做的工作，使用 Message Modal 组件作为 Users 页面上 alertError 的替代品，即 Component.Users。

如果你忘了我们做了什么以及为什么，可以基本按照 Logon 更改中概述的相同步骤进行。

请确保在阅读后续内容之前先自己尝试一下。

以下是 Component.Users 中 Types 的更改：

component
  :: ∀ m
    . MonadAff m
  => MonadAsk Env m
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \initUserName ->
      { authorized: false
      , selectedUser: Nothing
      , users: Map.empty
      , initUserName
      , errorMessage: Nothing ①
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , receive = Just <<< SelectedUserName
      , initialize = Just Initialize
      }
  }
-- BELOW CODE REDACTED

① 将 errorMessage 初始化为 Nothing。

然后，我们将添加代码以在 handleAction 中处理 Modal Action：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
  Modal output -> case output of ①
    Modal.Affirmative -> H.modify_ _ { errorMessage = Nothing }
    Modal.Negative -> H.modify_ _ { errorMessage = Nothing }
    Modal.InnerOutput _ -> pure unit
  where
-- BELOW CODE REDACTED
```

① 添加此 case。从 Logon 复制而来。

现在我们可以更改调用 alertError 的代码：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken, admin } ->
      when admin do
        queryResponse <-
          apiCall (QueryUsersRequest { authToken })
        case queryResponse of
          Left err -> H.modify_ _ { errorMessage = Just err } ①
          Right (QueryUsersResponse
            (QueryUsersResultsFailure { reason })) ->
            H.modify_ _ { errorMessage = Just $ "Query Users: " ①
              <> case reason of
                NotAuthorized -> "Not Authorized"
                NotAuthenticated -> "Not Authenticated" }
          Right (QueryUsersResponse
            (QueryUsersResultsSuccess { users })) -> do
            let mkMap f = foldl (\m r -> Map.insert (f r) r m) Map.empty
            usersMap = mkMap (_.userName <<< unwrap) users
            { initUserName } <- H.get
            H.modify_ _
              { authorized = true
              , users = usersMap
              , selectedUser = initUserName
                >>>= \userName -> Map.lookup userName usersMap
              }
  -- BELOW CODE REDACTED
```

① 在 2 处在 State 中设置 errorMessage。

现在我们可以删除以下代码行：

```
import Web.HTML.Window (alert)
import Web.HTML (window)

where
alertError :: String -> H.HalogenM State Action Slots Output m Unit
alertError msg = H.liftEffect $ window >>>= alert msg
```

最后，我们将更新 render，首先为 errorMessage 解构：

```
render :: State -> H.ComponentHTML Action Slots m
render { authorized, selectedUser, users, errorMessage } =
-- BELOW CODE REDACTED
```

其次，将 Modal 组件作为最后一个元素添加：

```
-- ABOVE CODE REDACTED
, (errorMessage # maybe (HH.text "") \message ->
  HH.slot _modal unit
  (Modal.component Message.component) message Modal) ①
]
```

① 从 Logon 复制而来。

现在代码应该可以编译了。

我们无法轻松测试这些错误消息，所以我们现在就眨眨眼点头说它有效。

## 30.14. 自定义 Modal 对话框组件

我们希望对 Modal 组件有一定的控制。以下是在我们想要控制的方面：

- 按钮标签
- 显示哪些按钮
- 以某种方式禁用/启用 Affirmative 按钮

我们还可以配置更多内容，例如样式，但对于这个学习应用程序，这些是实际需求，而其他任何内容都是锦上添花。

前两个将通过传递配置记录来实现。我们希望创建一个默认配置，以便我们可以使用 PureScript 的记录更新语法仅更改我们关心的字段。

第三个功能会更复杂，因为我们的内部组件必须与 Modal 通信，即它必须输出 Modal 组件将处理的数据。目前，内部组件的 Output 只是原样传递给父级，不做任何解释。

这不会很难，但会稍微复杂一些，所以我们将一起完成。

前两个功能非常简单。因此，首先在 Component.Modal 中定义一个名为 Config 的配置记录，该记录反映上述需求，然后返回这里。

这是我的初始定义：

