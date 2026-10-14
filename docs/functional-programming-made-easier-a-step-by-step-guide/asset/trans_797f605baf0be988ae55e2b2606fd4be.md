

① 添加了此导入。

② 我们通过 ioTimer 订阅第二个顶级组件。

③ 我们丢弃了 Lambda 从 CountdownTimer 的 H.raise 调用中传递过来的单元。

④ HalogenIO 有一个 dispose，我们正在调用它来释放另一个顶级组件 Counter。

确保你的代码是最新的并重新构建应用并运行服务器。你会看到：

```
[info] Build succeeded.
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- const
- datetime
- exceptions
- tailrec
```

将这些添加到 spago.dhall 文件中。

现在，重新构建应用并刷新浏览器并观看 COUNTDOWN。当它达到 0 时，你应该看到两件事。

首先，Counter 及其子组件消失。其次，你应该在控制台中看到所有 4 个 Counters 的 finalize 都被调用了：

![](img/8c0e9b687c62642e828ccb5481e11313_1634_0.png)

所以，这奏效了而且很棒，但我们必须在 Finalize 中自己清理 tickFiber 这一事实是有问题的。我们很容易忘记这一点。Halogen 在我们被 finalize 时已经从 emitter 取消订阅了，所以我们不必记住。但我们的 emitter 有一个 Fiber，我们真的应该杀掉它。如果我们不杀掉它，notify 调用将不会做任何事情，因为没有订阅者，但我们有一个正在运行且什么都不做只是产生热量的 Fiber。

如果我们的页面在一个更大的应用中，那么每次用户导航到我们的页面时都会创建一个新的 Fiber。所以有可能有几十个甚至几十个这些死 Fiber。这不是一个好情况。

这就是为什么我们明确处理了 Fiber 的杀死。但必须有更好的处理方式。花了我一点时间才想出来，但确实有。我只是要直接给你代码，然后我会逐行解释，这样你就能理解它是如何工作的。

首先，注释掉以下代码：

```
import Control.Alt ((<|/>))
import Effect.Aff (Fiber, forkAff, delay, killFiber, launchAff_)
```

① 添加了此导入。这需要在 spago.dhall 中使用 control 包。

② 将 launchAff_ 添加到导入列表中。

然后将 control 添加到你的 spago.dhall 中：

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "halo"
, dependencies =
  [ "aff"
  , "arrays"
  , "console"
  , "const"
  , "control" ①
  , "css"
  , "datetime"
  , "effect"
  , "exceptions"
  , "halogen-css"
  , "halogen-subscriptions"
  , "halogen"
  , "maybe"
  , "prelude"
  , "psci-support"
  , "tailrec"
  , "web-dom"
  , "web-events"
  , "web-html"
  , "web-uievents"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 由于我们添加了 import Control.Alt，所以添加了此包。

现在注释掉：

```
data Action
= Initialize
-- | Finalize ①
| Tick H.SubscriptionId
| HandleDocClick HTMLDocument MouseEvent

component
:: ∀ m
. MonadAff m
=> H.Component Query Input Output m
component = H.mkComponent
{ initialState: \i -> { count: i, tickFiber': Nothing }
, render
, eval: H.mkEval H.defaultEval {
    initialize = Just Initialize
    -- , finalize = Just Finalize ②
    , handleAction = handleAction
}
}
where
-- BELOW CODE REDACTED
```

① 我们不需要手动杀死我们的 Fiber，所以我们不需要处理 Finalize。

② 这个也可以去掉。

现在从 handleAction 中移除以下内容：

```
-- ABOVE CODE REDACTED

-- Finalize -> killTickFiber ①
HandleDocClick _ event -> do
-- BELOW CODE REDACTED
```

① 我们不需要处理不存在的 Action。

我们不需要在 State 中使用 tickFiber：

```
```haskell
type State =
  { count :: Int
  -- , tickFiber' :: Maybe (Fiber Unit) ❶
  }

component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  -- { initialState: \i -> { count: i, tickFiber': Nothing } ❷
  { initialState: \i -> { count: i }
  -- BELOW CODE REDACTED
```
```

+   ❶ 我们不再需要跟踪 `tickFiber`。
+   
+   ❷ 我们也不需要初始化它。

最后，让我们清理导入的编译器警告：

```
```haskell
import Data.Maybe (Maybe(..))
-- import Data.Maybe (Maybe(..), maybe) ❶
import Effect.Aff (forkAff, delay, killFiber, launchAff_) 
-- import Effect.Aff (Fiber, forkAff, delay, killFiber, launchAff_) ❷
```
```

+   ❶ 我们的代码不再使用 maybe。
+   
+   ❷ 我们的代码不再使用 Type Fiber。

此时你的代码应该可以编译。

现在，让我们详细回顾一下我们新的方法。首先，我们从 Tick 开始：

```
```haskell
Tick sid -> do
  { count } <- H.get
  unless (count <= 0) $ H.modify_ { count = count - 1 }
  when (count == 1) do
    H.raise unit
    H.unsubscribe sid ❶
```
```

+   ❶ unsubscribe 将会杀掉我们的 `tickFiber`。

我们移除了 `killTickFiber` 调用，现在依赖 `H.unsubscribe` 来为我们完成此操作。要理解它是如何工作的，我们需要深入研究新的 `Initialize` 代码。

```
Initialize -> do
  -- timer setup
  { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
  tickFiber <- H.liftAff $ forkAff $ forever do
    log "Sleeping..."
    delay $ Milliseconds 1000.0
    H.liftEffect $ HS.notify tickListener Tick ①
  let fiberEmitter = HS.makeEmitter \_ -> pure $ launchAff_ do ② ③
    log "Killing tick fiber..."
    killFiber (error "Event source finalized") tickFiber
  HQ.subscribe' \sid -> (tickEmitter <|> fiberEmitter) <#>( _ $ sid) <4>
 ⑤ ⑥
```

① Tick 期待 SubscriptionId 作为其第一个参数。由于我们还没有订阅，所以还没有它，我们必须从 H.subscribe' 获取，即 Primed 版本。

② 我们正在为我们的 Fiber 创建一个 Emitter，但 ONLY 为了在取消订阅时控制清理。我们使用 makeEmitter 来做到这一点。

③ 我们不关心作为 makeEmitter 传递的函数的第一个参数传递的回调，因为它用于通知。我们已经有 tickEmitter/tickListener 对用于此。我们只是返回在取消订阅时要执行的清理代码。由于我们只有一个订阅者，我们不需要像 create 那样跟踪订阅者。我们只需杀掉 tickFiber。

④ 我们正在使用 Primed 版本的 subscribe 来获取我们将要传递给我们的 Action 的 SubscriptionId，即 Tick，使用 map。

⑤ 我们使用 <|> 将 tickEmitter 和 fiberEmitter 合并成一个 Emitter。当 Halogen Engine finalize 我们的组件时，它会从我们的合并 Emitter 取消订阅，从而触发对两者清理代码的运行。

⑥ Emitter 是一个 Functor，所以我们可以对其进行 map。我们的 Emitter 发出缺少单个参数的 Actions，即 SubscriptionId，因此其类型是 Emitter (H.SubscriptionId -> Action)。我们在 Emitter 上映射一个函数，该函数将 sid 应用于 Tick 数据构造函数从而创建一个 Action。这使得最终结果成为 Emitter Action，这正是 H.subscribe' 期望函数返回的内容。

继续重新运行应用并让 CountdownTimer 倒数到 0。你应该会看到以下内容：

![](img/8c0e9b687c62642e828ccb5481e11313_1640_0.png)

我们每次休眠时都会得到 Sleeping... 消息，即只要 tickFiber 正在运行。一旦我们

① 添加了这些导入

② 添加了这些注释以区分代码块。

③ 我们从浏览器窗口开始获取文档。

④ 我们使用 HQ.subscribe' 和 HQE.eventListener 进行订阅。注意我们正在使用 HS.subscribe 的 Prime 版本，因为我们不需要取消订阅。我们会让 Halogen 在我们被 Finalized 时处理。

⑤ 这是我们要监听的 MouseEvent。

⑥ toEventTarget in Web.HTML.HTMLDocument 将 HTMLDocument 转换为 EventTarget。

⑦ 这是点击事件发生时的回调函数。它接收一个 Event 并返回一个 Maybe Action。由于 ME.fromEvent 返回一个 Maybe，我们使用我们的 Action 数据构造函数对其进行 map。

⑧ 我们即将创建的数据构造函数 HandleDocClick 接收 3 个参数。第一个是 HTMLDocument，第二个是 SubscriptionId，第三个是 MouseEvent。

编译器错误让我们知道我们需要添加 HandleDocClick 的 Action 定义。它将接收 HTMLDocument、SubscriptionId 和 MouseEvent：

```
import Web.HTML.HTMLDocument (HTMLDocument) ①

data Action
  = Initialize
  | Tick H.SubscriptionId
  | HandleDocClick HTMLDocument MouseEvent
```

① 添加了此导入。

现在，我们只是在文档被点击时记录到控制台：

```
import Effect.Class.Console (log) ①

  -- ABOVE CODE REDACTED
  Finalize -> killTickFiber
  HandleDocClick _ _ -> log "Document clicked on"
```

① 添加了此导入。

将此行代码添加到 handleAction 中。

现在，重新运行应用并刷新浏览器。现在点击周围看看控制台中记录了什么。

并且新的构建错误：

