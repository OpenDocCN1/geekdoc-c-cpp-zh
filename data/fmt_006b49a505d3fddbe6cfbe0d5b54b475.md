
这全部是从 halo 偷来的。我们将在登录页面中使用它。

现在，返回 `Component.Logon` 并删除以下内容：

```
import CSS (color, white)
```

现在添加以下导入：

```
import AppTheme (paperColor, themeColor, themeFont)
import CSS.Background (backgroundColor)
import CSS.Border (borderRadius)
import CSS.Box (boxShadow)
import CSS.Color (rgba, white)
import CSS.Common (center)
import CSS.Cursor (cursor, pointer)
import CSS.Display (display, flex)
import CSS.Flexbox (flexDirection, column, row, flexGrow, alignItems
    , justifyContent)
import CSS.Font (FontWeight(..), color, fontSize , fontWeight)
import CSS.Geometry ( paddingTop, paddingBottom, paddingRight, paddingLeft
    , width, height)
import CSS.Missing (spaceEvenly)
import CSS.Property (value)
import CSS.Size (rem, px, pct, vw)
import DOM.HTML.Indexed.InputType (InputType(..))
import Halogen.HTML.Events as HE
import Halogen.HTML.Properties as HP
import Image.BookCover (bookCover)
```

接下来，用以下内容替换 `Action` 定义：

```
data Action
    = Logon
```

现在用以下内容替换 `render` 函数：

```
render :: State -> H.ComponentHTML Action Slots m
render {} =
    HH.div [
        HC.style do
            display flex
            flexDirection column
            width $ vw 22.0
            height $ vw 25.0
            paddingTop $ vw 1.25
            paddingBottom $ vw 1.25
            paddingLeft $ vw 1.50
            paddingRight $ vw 1.50
            backgroundColor paperColor
```

```
borderRadius (px 7.0) (px 7.0) (px 7.0) (px 7.0)
    boxShadow (px 10.0) (px 10.0) (px 20.0) (rgba 0 0 24 0.75)
]
[ HH.div[
    HC.style do
        paddingRight $ vw 1.0
        display flex
        flexDirection column
        alignItems center
        justifyContent center
        flexGrow 10.0
    ]
    [ HH.img [
        HC.style do
            width $ pct 40.0
        , HP.src bookCover
    ]
    ]
, HH.div [
    HC.style do
        display flex
        flexDirection column
        justifyContent spaceEvenly
        alignItems center
        flexGrow 3.0
    ]
    [ HH.div [
        HC.style do
            display flex
            flexDirection row
            alignItems center
            justifyContent center
            themeFont
        ]
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Username: " ]
    , HH.input [
        HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
```

```
fontSize (vw 1.0)
]
]
, HH.div [
    HC.style do
        display flex
        flexDirection row
        alignItems center
        justifyContent center
        themeFont
]
[ HH.label [
    HC.style do
        width (rem 6.0)
] [ HH.text "Password: " ]
, HH.input [
    HP.type_ InputPassword
, HC.style do
    backgroundColor paperColor
    width (vw 8.3)
    paddingLeft (rem 0.5)
    paddingRight (rem 0.5)
    fontSize (vw 1.0)
]
]
]
, HH.div [
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
        color white
```

```
cursor pointer
    , HE.onClick $ const Logon
    ]
    [ HH.text "LOGON" ]
    ]
]
```

大部分代码都是样式，但有几件事值得注意，例如我们如何指定输入字段为密码：

```
import DOM.HTML.Indexed.InputType (InputType(..)) ①

-- ABOVE CODE REDACTED
    , HH.input [
        HP.type_ InputPassword ②
        , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
-- BELOW CODE REDACTED
```

① 我们需要导入 `InputType` 类型，它具有输入字段类型的 Data 构造子。

② 将 `type` 属性设置为 `InputPassword`。

另一个值得注意的项目是按钮点击处理：

```
import Halogen.HTML.Events as HE ①

-- ABOVE CODE REDACTED
    [ HH.button
      [
        HC.style do
          backgroundColor themeColor
          themeFont
          fontWeight $ FontWeight $ value "500"
          fontSize $ vw 1.0
          width (rem 20.0)
          height $ vw 3.0
          color white
          cursor pointer
        , HE.onClick $ const Logon ②
      ]
      [ HH.text "LOGON" ]
    ]
-- BELOW CODE REDACTED
```

① 我们导入 `Halogen.HTML.Events` 以获取标准 DOM 事件，例如 `onChange`、`onBlur`、`onKeyUp` 等。

② `onClick` 接受一个消耗事件的函数。我们不关心点击的细节，所以我们使用 `const` 来丢弃它。

使用以下命令运行你的应用程序：

```
make run
```

你会得到以下错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- dom-indexed
```

相应地更新你的 `spago.dhall` 文件，运行程序并导航到 `localhost:8000`。确保不要只刷新浏览器，因为 URL 位于注销屏幕。

当你这样做时，你应该会看到以下内容：

![](img/8c0e9b687c62642e828ccb5481e11313_1714_0.png)

现在，我们需要做出一些决定。我们希望用户输入他们的用户名和密码然后点击登录按钮。但如果他们没有这样做而只是点击了登录按钮，我们应该怎么办？

我们可以做几件事。我们可以在必填字段中没有数据时禁用登录按钮。这需要我们监控用户名和密码的每次更改，以便在所有必填字段都有数据时立即启用登录按钮。

另一种方法是在必填字段为空且他们点击了登录按钮时给出错误消息。唯一的问题是我们如何显示此错误消息？

我能想到 2 种方法。首先，我们在有问题的字段旁边显示错误消息，即为空的必填字段。另一种方法是在其中显示错误消息的弹出对话框。

你会采取哪种方法，为什么你认为你的方法比其他方法更好？在阅读我的意见之前先想一想。

我最喜欢的方法是禁用按钮并仅在有效时显示它，因为我认为它提供了更简洁的 UI。这种方法的唯一缺点是用户可能不明白他们需要输入什么才能启用按钮。但我认为在这种表单中我们不会冒这个风险，因为任何在互联网上花费过时间的人都遇到过许多登录屏幕。

因此，对于这种场景，我将选择这种方法。然而，如果这是一个更复杂的表单，那么我会选择在缺失字段旁边添加错误消息。

而且虽然对话框在这里不是一个糟糕的想法，但在这个应用中我们会有很多对话框的机会。

对话框不是我最喜欢的解决方案，但有时它们是必要的，以减少屏幕混乱，而且它会

对我们来说，看看如何开发这样一个组件以及它将如何与我们的页面交互是很有益的。

现在我们已经有了计划，我们准备完成登录页面。

接下来我们需要做的是在我们的 `State` 中跟踪字段中的数据，以便在用户点击登录按钮时我们拥有这些值。

这通常是使用 `onChange` 完成的，当用户退出一个字段并且该字段已被修改时就会触发。但我们希望在每次更改时都进行检查。为此，我们将使用 `onValueInput`。

添加一个名为 `Input` 的 `Action`，然后将 `onValueInput` 从 `Halogen.HTML.Events` 添加到用户名和密码字段以触发该新的 `Action`。使用本文件中 `HE.onClick` 的代码作为参考以及 Pursuit。

准备好继续时返回这里。

以下是这些更改：

```
data Action
= Logon
  | Input String ①

-- ABOVE CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Username: " ]
    , HH.input [
        HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Password: " ]
    , HH.input [
        HP.type_ InputPassword
    , HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- BELOW CODE REDACTED
```

① 添加了 `Input` 数据构造子。`String` 参数由 `onValueInput` 提供给我们。

② 为两个字段添加了事件处理程序。

请注意 `onValueInput` 接受一个类型为 `String -> Maybe a` 的函数。这允许我们在 `render` 逻辑中拒绝输入。我们也可以在 `handleAction` 中拒绝它。

让我们看看我们的组件创建代码：

```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { }
  , render
  , eval: H.mkEval H.defaultEval
  }
```

你能看出我们缺少什么吗？

我们正在使用所有默认值。我们需要覆盖它们以便我们可以添加 `handleAction`。使用我们在 `halo` 或 `Component.Page` 中所做的内容作为示例，对其进行更改以仅添加 `handleAction`。

完成编码后返回这里。

以下是该更改：

```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction -- COMPILER ERROR!!
      }
  }
```

不，编译器错误并不令人惊讶，因为我们还没有编写 `handleAction`。我们很快就会这样做，但现在，我们需要将用户名和密码字段的值添加到我们的 `State` 中，以便我们可以跟踪它们的变化。

然后当用户点击登录按钮时，我们将拥有它们，可以使用它们来调用我们的后端服务器。

更新 `State` 以包含此信息，然后在完成后继续阅读。

以下是该更改：

```
type State =
  { userName :: String
  , password :: String
  }
```

接下来，更新 `initialState` 将这些值初始化为空字符串然后返回这里。

以下是该更改：

```
component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> { userName: "", password: "" }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction -- COMPILER ERROR!!
      }
  }
```

现在编写 `handleAction` 以维护这些新添加到 `State` 的值，但暂时对 `Logon` `Action` 进行存根。完成后继续。

以下是 `handleAction`：
