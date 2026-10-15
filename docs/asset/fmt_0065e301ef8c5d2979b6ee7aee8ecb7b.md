
最后的 TODO 是我们推迟的那一项，即成功创建用户的情况。我们需要将新用户告知父组件。在阅读任何进一步内容之前先进行此更改。

以下是该更改：

```
import Component.Modal (InnerOutput(..)) ①
import Entity.User (User(..)) ①

-- ABOVE CODE REDACTED
    Right CreateUserResultsSuccess -> H.raise $ PassThrough ②
      $ User ③
        { userName
        , admin
        , firstName
        , lastName
        , temporaryPassword: true
        }
-- BELOW CODE REDACTED
```

① 添加了 `(..)` 以获取数据构造函数。

② 将输出发送给父组件。不要忘记 `PassThrough`。

③ 记住我们的输出类型是 `User`。

`Modal` 会看到一个 `PassThrough` 并解包其负载并将其 `H.raise` 给其父组件。

现在，我们需要在 `Users` 页面上添加一个添加用户的按钮。我们不需要检查用户是否具有管理员权限，因为如果他们没有，他们就看不到页面的任何部分。

切换到 `Component.Users`。以下是 `render` 的更改：

```
import AppTheme (paperColor, selectedColor, themeColor, themeFont) ①
import CSS.Common (center) ②
import CSS.Font (FontWeight(..), color, fontWeight, fontSize) ③
import CSS.Geometry ( minWidth, maxHeight, padding, paddingBottom
                    , paddingRight, paddingLeft, width, height) ④
import CSS.Overflow (overflowY, overflowAuto) ②
import CSS.Property (value) ②
import CSS.Size (rem, pct, px) ⑤

-- ABOVE CODE REDACTED
    [ HH.ul ⑥
      [
        HC.style do
          maxHeight (pct 80.0)
          overflowY overflowAuto
      ]
    (Map.values users # fromFoldable
        <#\ (user@(User { userName })) ->
            let isSelected = Just user == selectedUser in
            HH.li [
                HP.class_ $ ClassName "list-group-item"
            , HC.style do
                backgroundColor
                    if isSelected then selectedColor
                    else paperColor
                color
                    if isSelected then white
                    else black
                cursor pointer
            , HE.onClick $ const $ UserSelected user
            ]
            [ HH.text userName ])
    , HH.div ⑦
    [
        HC.style do
            display flex
            flexDirection row
            justifyContent center
            paddingLeft (px 40.0)
    ]
    [ HH.button
        [
            HC.style do
                backgroundColor themeColor
                themeFont
                fontWeight $ FontWeight $ value "500"
                fontSize $ rem 0.8
                width (rem 8.0)
                height $ rem 2.5
                color white
                cursor pointer
            -- COMPILER ERROR!!
            , HE.onClick $ const CreateUser ⑧
        ]
        [ HH.text "Create User" ]
    ]
]
-- BELOW CODE REDACTED
```

+ ① 将 `themeColor` 和 `themeFont` 添加到导入列表中。

+ ② 添加了这些导入。

+ ③ 将 `FontWeight`、`fontWeight` 和 `fontSize` 添加到导入列表中。

+ ④ 将 `maxHeight`、`paddingLeft`、`width` 和 `height` 添加到导入列表中。

+ ⑤ 将 `px` 添加到导入列表中。

+ ⑥ 将 `HH.ul_` 替换为 `HH.ul`，因为它接受属性。也为 `ul` 添加了样式。

+ ⑦ 将此整个 `div` 作为 `ul` 的同级添加。它有一个按钮作为子元素。

+ ⑧ 此 `Action` 需要实现，因此出现编译器错误。

现在实现 `CreateUser` `Action` 并为其处理代码做占位。然后返回这里。

以下是这些更改：

```
data Action
  = Initialize
  | UserSelected User
  | SelectedUserName (Maybe String)
  | Modal (Modal.Output Message.Output)
  | CreateUser ①

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
    CreateUser -> pure unit ②
```

+ ① 添加了此数据构造函数。

+ ② 为此 case 做了占位。

现在重建应用程序并刷新浏览器，看看目前效果如何。不要期望我们的新按钮能立即工作，因为 `handleAction` 中的代码只是占位。

我们需要将 `CreateUser Modal` 添加到 `Users` 页面，即 `Component.Users`。使用使用 `Modal` 的现有代码来帮助你将 `CreateUser Modal` 添加到页面。

完成后，返回这里并继续。

以下是 `Component.Users` 中的代码更改：

```
import Component.Modal.CreateUser as CreateUser ①

type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Map String User
  , initUserName :: Maybe String
  , errorMessage :: Maybe String
  , creatingUser :: Boolean ②
}

data Action
= Initialize
| UserSelected User
| SelectedUserName (Maybe String)
| ErrorModal (Modal.Output Message.Output) ③
| CreateUserModal (Modal.Output CreateUser.Output) ④
| CreateUser

type Slots = ⑤
( errorModal :: H.Slot Message.Query (Modal.Output Message.Output) Unit
, createUserModal
  :: H.Slot CreateUser.Query (Modal.Output CreateUser.Output) Unit
)

_errorModal = Proxy :: Proxy "errorModal" ⑥
_createUserModal = Proxy :: Proxy "createUserModal"

-- ABOVE CODE REDACTED
component = H.mkComponent
  { initialState: \initUserName ->
      { authorized: false
      , selectedUser: Nothing
      , users: Map.empty
      , initUserName
      , errorMessage: Nothing
      , creatingUser: false ⑦
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , receive = Just <<< SelectedUserName
      , initialize = Just Initialize
      }
  }
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
    ErrorModal output -> case output of ⑧
        Modal.Affirmative -> H.modify_ _ { errorMessage = Nothing }
        Modal.Negative -> H.modify_ _ { errorMessage = Nothing }
        Modal.InnerOutput _ -> pure unit
-- BELOW CODE REDACTED

    render :: State -> H.ComponentHTML Action Slots m
    render { authorized, selectedUser, users, errorMessage, creatingUser } = ⑨
-- CODE REDACTED
        , (errorMessage # maybe (HH.text "") \message ->
        HH.slot _errorModal unit ⑩
            (Modal.component ModalCommon.errorConfig Message.component)
            message ErrorModal) ⑪
        , if not creatingUser then HH.text "" else ⑫
        HH.slot _createUserModal unit
            (Modal.component createUserConfig CreateUser.component)
            unit CreateUserModal
    ]
    where
        createUserConfig = Modal.defaultConfig ⑬
            { affirmativeLabel = "CREATE"
            , affirmativeDisabled = true
            }
```

- ① 添加了此导入。

- ② 添加了用于显示 `CreateUser` 模态框的标志位。

- ③ 将 `Modal` 重命名为 `ErrorModal`。

- ④ 添加了 `CreateUserModal`。

- ⑤ 不得不将 `modal` 重命名为 `errorModal`，并添加 `createUserModal`。

- ⑥ 不得不将 `_modal` 重命名为 `_errorModal`，并添加 `_createUserModal`。

- ⑦ 将标志位初始化为不显示 `CreateUser` 模态框。

- ⑧ 将 `Modal` 改为 `ErrorModal`。

- ⑨ 将 `creatingUser` 加入解构。

- ⑩ 使用重命名后的标签 `_errorModal`。

- ⑪ 将 `Action` 从 `Modal` 改为 `ErrorModal`。

- ⑫ 当 `creatingUser` 为 `true` 时，添加 `CreateUser` 模态框。

- ⑬ 重写配置以覆盖“确认”按钮，并将其初始化为禁用状态。这在我们创建 `CreateUser` 模态框时使用。

为了消除编译器错误，先将 `CreateUserModal` 桩实现（stub out）一下：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
    CreateUser -> pure unit
    CreateUserModal _ -> pure unit ①
```

- ① 暂时只是一个桩实现。

现在，在 `handleAction` 中实现 `CreateUser` 的代码。准备好继续时，再回到这里。

这里是那段代码：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
    CreateUser -> H.modify_ _ { creatingUser = true } ①
```

① 在 `State` 中设置 `creatingUser`。

现在，在 `handleAction` 中完善 `CreateUserModal` 的处理。暂时只处理 `Modal.Affirmative` 和 `Modal.Negative` 两种情况，并先桩实现 `Modal.InnerOutput`。然后回到这里继续阅读。

变更内容如下：

```
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
-- CODE REDACTED
    CreateUserModal output -> case output of
        Modal.Affirmative -> H.modify_ _ { creatingUser = false } ①
        Modal.Negative -> H.modify_ _ { creatingUser = false } ①
        Modal.InnerOutput _ -> pure unit ②
-- BELOW CODE REDACTED
```

- ① 停止显示该模态框。

- ② 暂时不做任何事。

即使我们的 `render` 函数还是桩实现，也可以先测试一下 `CreateUser Modal`。要测试，请重新构建应用程序、刷新浏览器、登录、点击 `Users` 按钮，然后点击 `Create User` 按钮。

当我这样做时，得到：

![](img/8c0e9b687c62642e828ccb5481e11313_1869_0.png)

点击 `CANCEL` 按钮会关闭模态框，但点击 `CREATE` 按钮却没有任何反应。这是因为界面没有体现出该按钮处于禁用状态。我们应该让它像 `Logon` 处理 `LOGON` 按钮那样工作。

看看我们在 `Logon` 中是如何处理禁用按钮样式的，然后在 `Component.Modal` 中对禁用按钮做同样的事情。准备好继续时，回到这里。

变更内容如下：
