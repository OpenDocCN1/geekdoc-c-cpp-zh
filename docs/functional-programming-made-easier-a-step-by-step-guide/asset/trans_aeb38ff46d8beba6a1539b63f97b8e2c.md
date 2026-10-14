
```
-- ABOVE CODE REACTED
render :: State -> H.ComponentHTML Action Slots m
render { route } = case route of
  Logon -> HH.slot_ _logon unit (Page.component Logon.component) unit ①
  Logoff -> HH.span [ HC.style $ color white ] [ HH.text "Logoff" ]
  Users _ -> HH.span [ HC.style $ color white ] [ HH.text "Users" ]
  ChangePassword -> HH.slot_ _changePassword unit
    (Page.component ChangePassword.component) unit ①
```

最后，在 `Component.ChangePassword` 中编写 `render` 函数，以在页面中间放置一个文本为 `Users` 的按钮。

利用我们目前编写的 `Component.Page` 和 `Component.Logon` 中的一切来帮助你。在排查 CSS 为何不生效时，Google 和 StackOverflow 都是你的朋友。

使用 Flex Grids，因为它们使用起来相当简单，别忘了 `align-items` 和 `justify-content`。

当你得到你认为可行的东西后，回到这里。

我基本上是从 Logon 的按钮那里“偷”来的代码：

```haskell
import AppTheme (themeColor, themeFont) ①
import CSS.Background (backgroundColor)
import CSS.Color (white)
import CSS.Common (center)
import CSS.Cursor (cursor, pointer)
import CSS.Display (display, flex)
import CSS.Flexbox (flexDirection, row, justifyContent, alignItems)
import CSS.Font (FontWeight(..), fontWeight, fontSize, color)
import CSS.Geometry (width, height, paddingTop)
import CSS.Property (value)
import CSS.Size (vw, rem)

-- ABOVE CODE REDACTED
render :: State -> H.ComponentHTML Action Slots m
render _ =
  HH.div [
    HC.style do
      display flex
      flexDirection row
      alignItems center
      justifyContent center
      paddingTop $ vw 0.65
  ]
  [ HH.button
    [
      HC.style do
        backgroundColor themeColor
        themeFont
        fontWeight $ FontWeight $ value "500"
        fontSize $ vw 1.0
        width (rem 20.0)
        height $ vw 3.0
        color white ②
        cursor pointer ②
      , HE.onClick $ const Click
    ]
    [ HH.text "Users" ]
  ]
```

① 添加了这些导入。对于 CSS 导入，我们本可以使用 `import CSS` 来包含大多数这样的导入，因为它重新导出了大部分常见 CSS 函数，除了我们写过的 `CSS.Cursor`。但我喜欢把它们分开，因为这样可以让我知道我拥有哪些 CSS 功能，而不是一个没有特定分组或顺序的庞大导入列表。

② 从这里移除了我们在 Logon 页面上所做的禁用检查。

现在，构建客户端：

```
make build
```

确保你的服务器仍在运行，然后转到浏览器，确保 URL 是 `localhost:3000/#/change-password`。如果已经是，则只需重新加载页面，否则，在地址栏中输入此 URL 并按回车。

当我执行任一操作时，页面中间会出现一个 `Users` 按钮。

但我们已经不再登录。我们刷新了页面，`authToken` 不再存在于内存中。

我们需要让 Router 更智能。如果 `userRef` 为空，那么无论 URL 的 Hash 值是什么，Router 都必须将用户重定向到 Logon 页面。

在阅读我的解决方案之前，先试着做出这个修改。

我的解决方案如下：

```
import Control.Monad.Reader.Class (class MonadAsk, ask) ①
import Data.Maybe (Maybe(..), isNothing) ②
import Effect.Ref as Ref ③

-- ABOVE CODE REDACTED
where
  handleQuery
    :: ∀ a
    . Query a
    -> H.HalogenM State Action Slots Output m (Maybe a)
  handleQuery = case _ of
    Navigate route a -> do ④
      { userRef } <- ask ⑤
      ref <- H.liftEffect $ Ref.read userRef ⑥
      H.modify_ _ { route = if isNothing ref then Logon else route } ⑦
      pure (Just a) ⑧
-- BELOW CODE REDACTED
```

① 向导入列表中添加了 `ask`。
② 向导入列表中添加了 `isNothing`。
③ 添加了这个导入。
④ 添加了一个 `do` 块来执行多个步骤。
⑤ 请求 ReaderT 环境（即 `Env`），通过解构只获取 `userRef`。
⑥ 读取 `Ref`，以便查看它是否为 `Nothing`。我们使用 `liftEffect`，因为 `Ref.read` 在 `Effect` 中运行，而我们处于 `HalogenM` 中。
⑦ 如果我们尚未登录，总是强制路由为 `Logon`。否则，遵循我们从 `Navigate` Action 获得的路由。
⑧ 由于我们现在在 `do` 块中，不需要 `applySecond`。

现在，重新构建客户端：

```
make build
```

现在，刷新浏览器，看看它是否将我们重定向到 Logon 页面。

的确会重定向，但它不会改变 URL 中的 Hash。那是因为我们是在内部路由。

这里我们可以做两件不同的事情。我们可以保留现状，然后在用户成功登录后，查询 Hash 以了解用户原本试图前往哪里，并转到那里，而不是转到 Logon 页面的默认位置。

为此，我们会使用 `Routing.Hash` 中的 `getHash` 和 `Routing.Duplex` 中的 `Route.parse`。一旦用户登录，我们就获取 Hash 并尝试解析它。如果解析成功且不是 `Route.Logon`，那么我们就遵循它并重定向。我们将依赖每个页面来验证用户是否有权查看该页面，因此这不会带来安全风险。

如果 Hash 无法解析，或者解析后只是 `Route.Logon`，那么我们就保留当前逻辑。当然，如果我们有一个真正可用的 ChangePassword 页面，这个逻辑会稍微复杂一些。

但是，对于这个应用程序，我们不需要那种行为，尽管这是常态。对我们来说，我们只需使用 `navigate` 来相应地设置 Hash，而不是像之前那样只在内部路由：

```
import Capability.Navigate (class Navigate, navigate) ①

-- ABOVE CODE REDACTED
    where
    handleQuery
        :: ∀ a
          . Query a
        -> H.HalogenM State Action Slots Output m (Maybe a)
    handleQuery = case _ of
        Navigate route a -> do
            { userRef } <- ask
            ref <- H.liftEffect $ Ref.read userRef
            if isNothing ref then navigate Logon ②
            else H.modify_ _ { route = route } ③
                pure (Just a)
-- BELOW CODE REDACTED
```

① 向导入列表中添加了 `navigate`。
② 现在我们显式地导航到 Logon。这将改变浏览器地址栏中的 Hash。
③ 否则，我们只需遵循请求的路由。

现在，重新构建客户端：

```
make build
```

并刷新浏览器。

当我这样做时，我的 Hash 是 `/logon`。

重新登录，然后试试 Users 按钮，看看会发生什么。

当我点击它时，会进入 Users 页面。现在，刷新页面，看看是否带着正确的 Hash 回到 Logon 页面。

当我这样做时，确实如此。所以，看起来我们的 Hash 路由现在工作得好多了。

## 30.11. 用户页面

Users 页面左侧将包含一个用户列表，当用户点击列表中的某个用户时，我们将路由到 Users 页面，但这次是选中了一个用户。

这种路由方式将使浏览器后退按钮以用户所期望的更自然的方式工作。

当选中一个用户时，页面右侧将显示包含该用户详细信息的字段。

此页面还将包含一个“创建用户”按钮，允许我们创建新用户。

首先在 `src/Component` 下创建一个名为 `Users.purs` 的文件。

接下来，按照我们在 ChangePassword 页面上所做的，编写以下 Types。请记住，我们可能有也可能没有当前选中的 `User`，并且当用户不是管理员而没有权限查看此屏幕时，我们需要在屏幕上显示一条消息：

- `Input`（来自父组件）
- `Output`（传给父组件）
- `State`
- `Action`（来自事件监听器的事件）
- `Query`（来自父组件的 `H.tell` 或 `H.request`）
- `Slots`（用于子组件）

把我们迄今为止所写的内容作为你编码时的速查表，准备好继续前进后回到这里。

下面是 `Component.Users` 的开头：

```
module Component.Users where

import Prelude

import Data.Const (Const) ①
import Data.Maybe (Maybe)
import Entity.User (User)
import Halogen as H
import Halogen.HTML.CSS as HC
import Halogen.HTML as HH
import Halogen.HTML.Events as HE
import Halogen.HTML.Properties as HP

type State =
  { authorized :: Boolean ②
  , selectedUser :: Maybe User ③
  , users :: Array User ④
  }
type Input = Unit
type Output = Void
data Action
  = Initialize ⑤

type Query :: ∀ k. k -> Type
type Query = Const Void

type Slots :: ∀ k. Row k
type Slots = ()
```

① 其中一些导入现在就需要，另一些则是为后续代码预留的。
② `authorized` 是一个标志，我们将用它来跟踪用户是否为管理员。这必须存储在 State 中，因为 `render` 是纯函数，无法读取 `userRef`。当用户未被授权查看此页面时，`render` 将不显示该页面。
③ `selectedUser` 将来自 Hash 路由。在这种情况下，我们需要以不同的方式渲染，以便选中的用户在用户列表中被高亮显示。
④ `users` 是我们从服务器获取的用户列表。
⑤ 我们必须使用 `QueryUsers` API 调用来调用服务器，以获取所有用户的列表。我们会尽快执行此操作，这将是我们组件初始化后处理的第一个 Action。

根据我们目前所了解的情况，这是一个良好的开端。随着我们进一步了解支持此页面所需行为的需求，我们将在此处进行必要的修改。

接下来，编写 component 函数、`render` 的桩版本，并为 `Initialize` 分支编写桩实现，在
