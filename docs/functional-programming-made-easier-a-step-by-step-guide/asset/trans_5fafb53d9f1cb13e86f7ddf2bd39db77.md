

```text
[info] Build succeeded.
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- web-html
- web-uievents
```

把这些包添加到 `spago.dhall` 中。

再次重新运行应用，并刷新浏览器。现在点击页面各处，看看控制台（Console）中会记录什么。

你是否注意到，你点击的每个元素都会显示 `Document clicked on` 消息？

这是因为 DOM 中的事件会从被点击的元素开始，沿着 DOM 树一路冒泡，直到最终到达 `document`。

这就是 `stopPropagation` 的用途。但它必须在点击的目标（Target）处使用。这意味着如果我们想要使用 `stopPropagation`，就必须把它添加到页面上的每一个元素上。

更好的解决方案是获取事件的实际目标元素（Target Element），也就是用户真正点击的那个元素。然后将其与 `document` 进行比较，判断它是否就是被实际点击的对象，只有在这种情况下，我们才认为 `document` 被点击了。

处理 DOM 从来都不是件容易的事。所以我们一步一步来。

首先，我们要把拿到的 `event` 转成一个 DOM `Node`。然后用 `isEqualNode` 把它和 `document` 的 `Node` 进行比较。我们必须这样做，因为没有可以直接比较 `Element` 的方法。

这是我们的计划：

```text
MouseEvent ---> Event ---> EventTarget ---> Element ---> Node
```

我们从 `MouseEvent` 开始，把它转成 `Event`，再转成 `EventTarget`，一直转换下去，直到得到 `Node`。

我们将逐行培养一段代码，一步一步地修改它，直到我们按照上面的计划得到一个 `Node`：

```purescript
import Web.Event.Event as WebEvent
import Web.DOM.Element as DomElement
import Web.UIEvent.MouseEvent as ME

event :: MouseEvent

ME.toEvent event :: Event

WebEvent.target $ ME.toEvent event :: Maybe EventTarget

DomElement.fromEventTarget
  =<< (WebEvent.target $ ME.toEvent event) :: Maybe Element

DomElement.toNode <$>
  (DomElement.fromEventTarget
    =<< (WebEvent.target $ ME.toEvent event)) :: Maybe Node ①
```

① 我们将使用这一行代码。

好了，我们得到的是一个 `Maybe Node` 而不是 `Node`。我们后面得处理这个问题。

接下来，我们要对 `document` 做同样的处理。这是我们的计划：

```text
HTMLDocument ---> Document ---> Element ---> Node
```

我们还是逐行培养一段代码，一步一步修改，直到得到一个 `Node`。我们会按照上面的计划进行：

```purescript
import Web.DOM.Document as DomDocument
import Web.HTML.HTMLDocument as HTMLDocument

document :: HTMLDocument

HTMLDocument.toDocument document :: Document

DomDocument.documentElement $ HTMLDocument.toDocument document
:: Effect (Maybe Element)

do
  docElem' <- DomDocument.documentElement
    $ HTMLDocument.toDocument document
    :: Effect (Maybe Element)

do
  docNode' <- map DomElement.toNode <$>
    (DomDocument.documentElement $ HTMLDocument.toDocument document)
    :: Effect (Maybe Node) ①
```

① 我们将使用这一行代码。稍后需要用 `H.liftEffect` 把它提升。

以下是代码改动：

```purescript
import Web.DOM.Document as DomDocument ①
import Web.DOM.Element as DomElement
import Web.DOM.Node as DomNode
import Web.Event.Event as WebEvent

-- ABOVE CODE REDACTED
  HandleDocClick document event -> H.liftEffect do ② ③
    docNode' <- map DomElement.toNode <$>
      (DomDocument.documentElement
        $ HTMLDocument.toDocument document) ④
    let clickNode' = DomElement.toNode <$>
      (DomElement.fromEventTarget
        =<< (WebEvent.target $ ME.toEvent event)) ⑤
    case docNode', clickNode' of ⑥
      Just dn, Just cn -> do ⑦
        eq <- DomNode.isEqualNode dn cn ⑧
        when eq $ log "Document clicked on" ⑨
      _, _ -> pure unit ⑩
```

- ① 添加了这些导入。
- ② 我们现在给 `HandleDocClick` 的参数命名。
- ③ 我们用 `lift` 提升 do 块中所有的 `Effect` 调用。
- ④ 上面我们逐步培养出来的一行，用来获取 `document` 的 `Node`。
- ⑤ 上面我们逐步培养出来的一行，用来获取我们点击的元素的 `Node`。
- ⑥ 在 case 表达式中使用两个逗号分隔的值。
- ⑦ 模式匹配两者均为 `Just`。注意模式匹配也是用逗号分隔的。
- ⑧ 比较两个 `Node` 是否相等。
- ⑨ 只有当我们点击的是 `document` 时才记录日志，即被点击的 `Node` 等于 `document` 对应的那个 `Node`。
- ⑩ 兜底模式的通配变量数量必须相同，且用逗号分隔。

现在，重新运行应用……啊，不行。又缺少依赖了：

```text
[info] Build succeeded.
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- web-dom
- web-events
```

更新你的 `spago.dhall`。

现在重新运行应用，刷新浏览器，然后在页面各处点击。你应该会注意到，当你点击所有控件下方区域时，控制台中会记录 `Document clicked on`（在 Chrome 中，则是文本旁边的数字会增加）。

你还应该注意到，点击计数器和倒计时组件（CountdownTimer）的右侧区域，并不会记录 document 被点击。

这是因为这些组件中的 div 横跨了页面的宽度。如果我们想改变这种行为，可以考虑把点击 div 视为点击 document。这显然需要更多的逻辑。

我们也可以把点击按钮视为没有点击 document，而把其他所有点击都视为点击 document。

注释掉你当前的 `HandleDocClick` 代码，并用以下代码替换：

```purescript
import Halogen.HTML.Properties as HP ①

-- ABOVE CODE REDACTED
theCountdownDiv :: H.RefLabel
theCountdownDiv = H.RefLabel "the-countdown-div" ②

render :: State -> H.ComponentHTML Action Slots m
render { count } =
  HH.div
    [ HP.ref theCountdownDiv ③
    , HC.style do
        display flex
        flexDirection column
        padding (rem 1.0) (rem 1.0) (rem 1.0) (rem 1.0)
    ]
    [ HH.text $ "COUNTDOWN: " <> show count ]
```

- ① 添加了这个导入。
- ② 为倒计时 div 创建一个引用标签（Reference Label）。
- ③ 给这个 div 添加一个带有该标签的属性。

现在，我们可以使用 `H.getHTMLElementRef` 配合这个引用标签，获取包含 CountdownTimer 组件的那个 div 的 `Element`。然后我们可以把这个 `Element` 转换成 `Node`，以便与被点击的 `Node` 进行比较：

注释掉你当前的 `HandleDocClick` 代码，并用以下代码替换：

```purescript
-- import Data.Array (elem) ①
import Web.HTML.HTMLElement as HTMLElement ②

-- ABOVE CODE REDACTED
HandleDocClick _ event -> do ③
  let clickNode' = DomElement.toNode <$>
      (DomElement.fromEventTarget
        =<< (WebEvent.target $ ME.toEvent event)) ④
  divNode' <- map HTMLElement.toNode
      <$> H.getHTMLElementRef theCountdownDiv ⑤
  case clickNode', divNode' of ⑥
    Just cn, Just dn -> H.liftEffect do
      eq <- DomNode.isEqualNode cn dn
      when eq $ log "The CountdownTimer DIV clicked on" ⑦
    _, _ -> pure unit
```

1. 添加了这个导入。
2. 注释掉了这个导入。
3. 这个版本的 `HandleDocClick` 不需要 `document` 参数。
4. 和之前一样的代码，用来获取被点击的 `Node`。
5. 查找 `theCountdownDiv` 标签，然后把 `Element` 转换成 `Node`。
6. 这段代码和之前比较 `Node` 的例子非常相似。
7. 我们记录不同的消息，因为我们的目标是点击特定的 `div`。

重新运行应用，刷新浏览器，然后点击各处，看看效果如何。然后回到这里。

你应该会看到，每次点击 `CountdownTimer` 的 `div` 中的任何内容时，都会记录 `The CountdownTimer DIV clicked on`。

让我们看看这个图，看看我们完成了什么：

![](img/8c0e9b687c62642e828ccb5481e11313_1649_0.png)

在这一节中，我们完成了以下内容：

- 创建一个 EventSource
- 订阅非 Halogen 的 DOM EventSource，例如 `document` 上的 `click` 事件

到此为止，我们已经完成了这个图中的所有内容，这意味着我们现在有了一个很好的 Halogen 应用参考。

当我们构建任何 Halogen 应用时，这都会是一个很好的参考，比如我们之前为后端服务器构建前端应用时。

