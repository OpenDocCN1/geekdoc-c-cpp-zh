
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual text.

Let's produce proper output.

[content]
```purescript
import CSS.Text.Shadow (textShadow)
import Data.NonEmpty ((:|))
import Halogen.HTML.CSS as HC
import Halogen.HTML.Events as HE
import Halogen.HTML.Properties as HP

-- ABOVE CODE REDACTED
    where
-- handleAction and handleQuery REDACTED
    paperColor :: Color ①
    paperColor = rgb 0xd9 0xd9 0xd9

    themeColor :: Color
    themeColor = rgb 0x00 0x66 0x75

    themeFont :: CSS
    themeFont = fontFamily [ "Verdana" ] $ sansSerif :| []

    render
        :: State iInput
        -> H.ComponentHTML (Action iInput iOutput) (Slots iQuery iOutput) m
    render { iInput } =
        HH.div [
            HC.style do
                paddingTop $ rem 5.0
        ]
        [ HH.header [
            HC.style do
                position fixed
                CSS.top $ px 0.0
                width $ pct 100.0
                height $ rem 4.0
                boxShadow (px 10.0) (px 10.0) (px 20.0) (rgba 0 0 24 0.75)
                display flex
                alignItems center
                justifyContent flexStart
                backgroundColor themeColor
                zIndex 1
        ]
        [ HH.div [
            HC.style do
                paddingLeft $ rem 1.0
                color paperColor
                display flex
```

```
flexDirection row
alignItems center
flexBasis $ px 0.0
flexGrow 1.0
flexShrink 1.0
]
[ HH.img [
    HC.style do
        width $ px 40.0
    , HP.src bookCover -- COMPILER ERROR!!
]
, HH.span [
    HC.style do
        paddingLeft $ rem 1.0
        fontSize $ rem 1.3
        themeFont
        textShadow (px 0.0) (px 0.0) (px 5.0) (rgba 0 0 0 1.0)
        fontWeight $ FontWeight $ value "500"
        letterSpacing $ rem 0.05
    ]
    [ HH.text "Functional Programming Made Easier" ]
, HH.div [
    HC.style do
        display flex
        flexGrow 1.0
        justifyContent flexEnd
        paddingRight $ rem 1.0
    ]
    [ HH.span [
        HC.style do
            themeFont
            fontWeight $ FontWeight $ value "500"
            color white
            padding (rem 1.0) (rem 1.0) (rem 1.0) (rem 1.0)
            cursor pointer
        , HE.onClick $ const Logoff ②
    ] [ HH.text "Logoff" ]
    ]
]
]
, HH.div [
    HC.style do
        display flex
        alignItems center
```

```
justifyContent center
minHeight $ vh 90.0
]
[ HH.slot _inner unit innerComponent iInput Output ] ③
]
```

① 这里的小函数是用于 `render` 的通用样式常量。最终会将其移出，以便其他组件也可以使用。

② 我们在这里处理 `Logoff` 点击。

③ 这里是内部组件最终获得其输入的地方。请记住，`render` 会传入 `State`，其中 `iInput` 已存储以便在此调用中使用。

编译器报错是因为我们没有为网站提供图片。首先，在 `src` 下创建一个名为 `Image` 的新文件夹。

然后前往我的 GitHub Gist 获取包含图片 Data URL 的 PureScript 模块。你可以在此链接找到它，`BookCover.purs`。点击它。

现在，将代码复制到名为 `BookCover.purs` 的新文件中，并将其放在 `src/Image` 文件夹中。从 Github 复制此代码最简单的方法是点击 `Raw` 按钮，然后通过 `Cmd-A` 或 Windows 上的 `Ctrl-A` 全选文本，然后复制文本。

保存该文件，然后返回 `Component.Page` 并添加：

```
import Image.BookCover (bookCover)
```

现在它应该可以编译了。

## 30.8. 登录页面

我们希望尽快测试我们的代码。因此，我们只会创建一个完全占位的登录页面，以便进行测试。

在 `src/Component` 下创建一个名为 `Logon.purs` 的文件并添加以下代码：

```
module Component.Logon where

import Prelude

import CSS (color, white)
import Data.Const (Const)
import Effect.Aff.Class (class MonadAff)
import Halogen as H
import Halogen.HTML.CSS as HC
import Halogen.HTML as HH

type Input = Unit ①
type Output = Void
type State = {}
type Action = Void

type Query :: ∀ k. k -> Type ②
type Query = Const Void

type Slots :: ∀ k. Row k ③
type Slots = ()

component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> {}
  , render
  , eval: H.mkEval H.defaultEval ④
  }
where
  render :: State -> H.ComponentHTML Action Slots m
  render {} = HH.span [ HC.style $ color white ] [ HH.text "Logon" ] ⑤
```

① 所有组件类型都只是简单定义。

② 不要忘记这里的类型签名。如果你忘记了，编译器会提醒你。

③ 我们在这里添加类型签名，就像我们对 `Query` 所做的那样，因为编译器无法推断出我们的 kind。

④ 我们只使用 `defaultEval`，这意味着我们不必实现任何处理器。

⑤ 我们渲染一个简单的文本节点。

让我们将这个新组件作为子组件添加到我们的顶层组件，即路由器组件：

```
import Component.Logon as Logon ①
import Component.Page as Page

-- ABOVE CODE REDACTED
    render :: State -> H.ComponentHTML Action Slots m
    render { route } = case route of
        Logon ->
            HH.slot _logon unit (Page.component Logon.component) unit absurd ②
        Logoff -> HH.span [ HC.style $ color white ] [ HH.text "Logoff" ]
        Users _ -> HH.span [ HC.style $ color white ] [ HH.text "Users" ]
        ChangePassword ->
            HH.span [ HC.style $ color white ] [ HH.text "ChangePassword" ]
```

① 添加了这些导入。

② 渲染 `Logon` 子组件。

现在，我们应该能够再次运行应用程序：

```
make run
```

然而，我们得到了这个错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- nonempty
```

将此包添加到 `spago.dhall` 中，然后使用 `make run` 运行它。

现在，导航到 `localhost:8000` 并刷新页面。你应该会看到：

![](img/8c0e9b687c62642e828ccb5481e11313_1705_0.png)

现在，点击 `Logoff` 按钮，看看会发生什么。

我得到一个新的 URL：

```
localhost:8000/#/logoff
```

但页面仍然显示 `Logon`。为什么会这样？

事实证明，我们谈论过使用 `matchesWith` 进行路由，但我们从未将其添加到我们的应用程序中。

让我们现在添加它：

```
import Data.Route (routeCodec) ①
import Effect.Aff (launchAff_)
import Effect.Class (liftEffect)
import Routing.Hash (matchesWith)
import Routing.Duplex as RouteDuplex

main :: Effect Unit
main = do
  userRef <- Ref.new Nothing
  HA.runHalogenAff do
    body <- HA.awaitBody
    let router = H.hoist (runAppM { userRef }) Router.component
    io <- runUI router unit body ②
    liftEffect $ matchesWith (RouteDuplex.parse routeCodec) ③ ④
      \old' new -> when (old' /= Just new) $ -- COMPILER ERROR!! ⑤
        launchAff_ $ io.query $ H.mkTell $ Router.Navigate new ⑥ ⑦
```

① 添加了这些导入。

② 捕获 `runUI` 的 `HalogenIO`，以便我们可以查询 `Router`，让它知道 `Hash` 已更改。

③ 我们必须使用 `liftEffect`，因为我们在 `Aff` 中，但 `matchesWith` 在 `Effect` 中运行。

④ 我们提供自定义解析器，即 `RouteDuplex.parse routeCodec`。

⑤ 当旧 `hash` 与新 `hash` 不同时，则认为它已更改。

⑥ 我们必须在 `Aff` 中运行 `io.query`，但此 `Lambda` 返回一个 `Effect`。我们使用 `launchAff_` 在 `Aff` 中运行它。

⑦ 我们告诉 `Router` 组件，即我们的顶层组件，进行 `Navigate`。这将更改其状态，以便它会渲染正确的子页面。

`matchesWith` 会监听 `hashChange` 事件，然后调用我们的自定义解析器，如果成功，它会使用 `Maybe a`，即 `Maybe` 之前的路由和当前的路由，调用回调。

如果它们不同，则我们的回调将查询我们的 `Router` 组件，通过 `H.mkTell` 告诉它导航到不同的路由。`Router` 组件将其存储在其状态中，并根据当前路由渲染适当的页面。

在我们查看编译器错误之前，请将你的代码更新为此。

编译器错误是因为 `Route` 没有 `Eq` 实例。在阅读后续内容之前，使用 `derive` 添加该实例。

以下是添加到 `Data.Route` 的内容：

```
derive instance eqRoute :: Eq Route
```

现在，我们的 `Main` 模块应该可以编译了。

使用以下命令运行程序：

```
make run
```

然后前往 `localhost:8000`。确保你不在 `Logoff` URL，即 `localhost:8000/#/logoff`。

然后刷新页面并点击 `Logoff` 按钮，看看会发生什么。

我这样做时，得到的是一个显示 `Logoff` 文本的页面，这正是我们应该期望的。

现在，我们准备开始构建登录页面。

但在我们开始之前，让我们做一些整理工作。首先，我们将把 `Component.Page` 中的那些样式函数移出到它们自己的模块中。

在 `src` 下创建一个名为 `AppTheme.purs` 的文件，并将 `paperColor`、`themeColor` 和 `themeFont` 从 `Component.Page` 移过去。

你应该有：

```
```purescript

module AppTheme where

import Prelude

import CSS (CSS, fontFamily)

import CSS.Color (Color, rgb)

import CSS.Font (sansSerif)

import Data.NonEmpty ((:|))

paperColor :: Color

paperColor = rgb 0xd9 0xd9 0xd9

themeColor :: Color

themeColor = rgb 0x00 0x66 0x75

themeFont :: CSS

themeFont = fontFamily [ "Verdana" ] $ sansSerif :| []

```
```

现在，清理冗余的导入并向 `Component.Page` 添加以下导入：

```
```purescript

import AppTheme (themeColor, paperColor, themeFont)

```
```

快速旁注：在 VSCode 中，一旦你的 PureScript 文件编译成功，并且你有许多冗余导入，你会注意到光标附近弹出一个灯泡图标：

![](img/8c0e9b687c62642e828ccb5481e11313_1707_0.png)

你可以点击灯泡图标，你会得到一个菜单：

![](img/8c0e9b687c62642e828ccb5481e11313_1707_1.png)

选择 `Apply all import suggestions` 会自动清理你的冗余导入。我对其他菜单项的运气不太好，但因人而异。

接下来，在 `src` 下创建一个名为 `CSS` 的文件夹。然后在该文件夹下创建一个名为 `Missing.purs` 的文件。

将以下内容放入该文件中：

```
module CSS.Missing where

import CSS.Flexbox (AlignContentValue, JustifyContentValue)
import CSS.Property (Value)
import CSS.String (fromString)

class SpaceEvenly a where
    spaceEvenly :: a

instance spaceEvenlyValue :: SpaceEvenly Value where
    spaceEvenly = fromString "space-evenly"
instance spaceEvenlyAlignContentValue :: SpaceEvenly AlignContentValue where
    spaceEvenly = fromString "space-evenly"
instance spaceEvenlyJustifyContentValue :: SpaceEvenly JustifyContentValue where
    spaceEvenly = fromString "space-evenly"
```
