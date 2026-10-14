

import Halogen.Subscription as HS ①

-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
    ②
    ???
  Tick -> pure unit

① 添加了此导入。

② 我们首先创建 Emitter 和 Listener，分别重命名为 tickEmitter 和 tickListener。

接下来，我们将使用 H.subscribe 订阅 Emitter。这会返回 SubscriptionId，以便我们选择时取消订阅。

Subscription 会在 Halogen 组件 Finalized 时自动取消订阅。但在我们的代码中，我们希望在 CountdownTimer 达到 0 时取消订阅。如果我们不关心 SubscriptionId，我们本可以调用此函数的 Prime 版本 H.subscribe'。

以下是订阅的代码：

```
import Halogen.Query.HalogenM as HQ ①

-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
    tickSubscription <- HQ.subscribe tickEmitter ②
    ???
  Tick -> pure unit
```

① 添加了此导入。

② 添加了 H.subscribe'。

接下来，我们将使用 forkAff 创建一个 Fiber，每秒发出一次 Tick：

```
import Control.Monad.Rec.Class (forever) ①
import Data.Time.Duration (Milliseconds(..))
import Effect.Aff (forkAff, delay)

-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
    tickSubscription <- HQ.subscribe tickEmitter
    tickFiber <- H.liftAff $ forkAff $ forever do ②
      delay $ Milliseconds 1000.0 ③
      H.liftEffect $ HS.notify tickListener $ Tick tickSubscription ④
      ???
  Tick -> pure unit
```

① 添加了这些导入。

② 无限循环。

③ 延迟 1 秒。

④ 发出 Tick Action。注意 sid 参数。这是为了让我们在计数器达到 0 时取消订阅。这意味着我们的 Tick 定义需要更改。

让我们接下来为我们的 Tick 定义添加 SubscriptionId：

```
data Action
  = Initialize
  | Tick H.SubscriptionId ①
```

① 我们为 Tick Action 添加了一个参数。

现在我们将把参数添加到 handleAction 中的 Tick：

```
-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize ->
    H.subscribe' \sid -> EventSource.affEventSource \emitter -> do
      fiber <- forkAff $ forever do
        delay $ Milliseconds 1000.0
        EventSource.emit emitter (Tick sid)
    ???
  Tick sid -> pure unit ①
```

① 添加了名为 sid 的 SubscriptionId 参数。

接下来，我们需要将 fiber 保存到我们的 State 中，以便在 Finalize 或计数器达到 0 时可以杀死它：

```
-- ABOVE CODE REDACTED
where
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do
    { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
    tickSubscription <- HQ.subscribe tickEmitter
    tickFiber <- H.liftAff $ forkAff $ forever do
      delay $ Milliseconds 1000.0
      H.liftEffect $ HS.notify tickListener $ Tick tickSubscription
    H.modify_ _ { tickFiber' = Just tickFiber } ①
  Tick sid -> pure unit
```

① 将 tickFiber' 保存到 State 中，以便以后使用 killFiber 停止它。

我们现在需要在 State 中添加 tickFiber'：

```
import Effect.Aff (Fiber, forkAff, delay) ①

type State =
  { count :: Int
  , tickFiber' :: Maybe (Fiber Unit) ②
  }
```

① 将 Fiber 添加到导入列表中。

② 将 tickFiber' 添加到 State。注意名称中的 Prime。这有助于我记住它是一个 Maybe

现在我们必须更新 initialState 以适应 State 的更改：

```
component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \i -> { count: i, tickFiber': Nothing } ①
  , render
  , eval: H.mkEval H.defaultEval {
      initialize = Just Initialize
    , handleAction = handleAction
    }
  }
where
  -- BELOW CODE REDACTED
```

① 初始化为 未运行的 fiber。

现在，我们准备开始处理 Tick Action：

```
-- ABOVE CODE REDACTED
where
  handleAction
    :: Action
    -> H.HalogenM State Action Slots Output m Unit
  handleAction = case _ of
    Initialize -> do
      { emitter:tickEmitter, listener:tickListener } <- H.liftEffect HS.create
      tickSubscription <- HQ.subscribe tickEmitter
      tickFiber <- H.liftAff $ forkAff $ forever do
        delay $ Milliseconds 1000.0
        H.liftEffect $ HS.notify tickListener $ Tick tickSubscription
      H.modify_ _ { tickFiber' = Just tickFiber }
    Tick sid -> do
      { count } <- H.get ①
      ???
```

① 从我们的 State 中获取 count。

接下来，我们将只要 count 是正整数就递减 count：

```
-- ABOVE CODE REDACTED
  Tick sid -> do
    { count } <- H.get
    unless (count <= 0) $ H.modify_ _ { count = count - 1 } ①
    ???
```

① 只要 count 不为 0 或更小，我们就递减我们的 count。

最后，当 count 达到 0 时，我们将通知我们的 Parent 并取消订阅 EventSource，从而触发其 Finalizer，杀死计时器 Fiber：

```
-- ABOVE CODE REDACTED
  Tick sid -> do
    { count } <- H.get
    unless (count <= 0) $ H.modify_ _ { count = count - 1 }
    when (count == 1) do
      H.raise unit ①
      H.unsubscribe sid ②
      killTickFiber ③
```

① 通过 H.raise 通知 Parent 计时器已过期。我们只发送 unit，因为除了事件已发生之外没有真正的信息需要传递。

② 使用传入的 sid 值从 EventSource 取消订阅。

③ 杀死 fiber（我们需要编写它）。

现在，让我们编写 killTickFiber：

```
import Data.Maybe (Maybe(..), maybe) ①
import Effect.Aff (Fiber, forkAff, delay, killFiber) ②
import Effect.Exception (error) ③

-- ABOVE CODE REDACTED
Tick sid -> do
  { count } <- H.get
  unless (count <= 0) $ H.modify_ _ { count = count - 1 }
  when (count == 1) do
    H.raise unit
    H.unsubscribe sid
    killTickFiber
where
  killTickFiber = do
    { tickFiber' } <- H.get
    tickFiber' # maybe (pure unit) \tickFiber -> do
      H.liftAff $ killFiber (error "Event source finalized") tickFiber ④
      H.modify_ _ { tickFiber' = Nothing } ⑤
```

① 将 maybe 添加到导入列表中。

② 将 killFiber 添加到导入列表中。

③ 添加了此导入。

④ 杀死 fiber。

⑤ 清除 tickFiber'，以免其他人再次尝试杀死它。顺便说一下，如果你尝试杀死一个未运行的 fiber，你的程序不会崩溃，但这只是良好的做法，以防有一天 Fiber 实现发生变化。

我们可能应该在组件 Finalize 且计数器尚未达到零时杀死 tick Fiber：

```
data Action
  = Initialize
  | Finalize ①
  | Tick H.SubscriptionId

-- ABOVE CODE REDACTED
Finalize -> killTickFiber ②
Tick sid -> do
  { count } <- H.get
  unless (count <= 0) $ H.modify_ _ { count = count - 1 }
  when (count == 1) do
    H.raise unit
    H.unsubscribe sid
    killTickFiber
-- BELOW CODE REDACTED
```

① 添加了 Finalize Action。

② 如果在最终化时 fiber 仍在运行，则杀死 fiber。

在继续阅读之前，请确保你的代码是最新的并且可以编译。

我们需要做的最后一件事是完成 render 的编码：

```
import CSS.Display (display, flex) ①
import CSS.Flexbox (flexDirection, column)
import CSS.Geometry (padding)
import CSS.Size (rem)
import Halogen.HTML.CSS as HC

-- ABOVE CODE REDACTED
render :: State -> H.ComponentHTML Action Slots m
render { count } =
  HH.div
    [ HC.style do
        display flex
        flexDirection column
        padding (rem 1.0) (rem 1.0) (rem 1.0) (rem 1.0)
    ]
    [ HH.text $ "COUNTDOWN: " <> show count ]
```

① 添加这些导入。

在用它更新你的代码之前，花点时间理解 render 代码。你之前已经见过所有这些内容，除了 padding 也许，它以与 CSS 中的 padding 相同的顺序接受 Size 的 padding 值，即 上、右、下 和 左。

现在，我们将把 CountdownTimer 作为另一个顶级组件添加到其中。我们将把它添加到 body 中，这意味着它将被追加到我们已经拥有的带有 Counters 的 body 中，即 假设我们在 Counter 之后添加它。

回到我们的 Main 模块，我们将进行以下更改：

```
import Component.CountdownTimer as CountdownTimer ①

main :: Effect Unit
main = do
  HA.runHalogenAff do
    body <- HA.awaitBody
    io <- runUI (Counter.component 3) 0 body
    io.subscribe $ CR.consumer \currentCount -> do
      log $ "Received Count from Top-level Counter: " <> show currentCount
      pure Nothing
    void $ runUI CountdownTimer.component 15 body ② ③
    ???
```

① 添加了此导入。

② 使用 15 秒倒计时启动 CountdownTimer。

③ 我们丢弃了计时器组件的 HalogenIO 值，因为我们不会使用它。

现在，我们将订阅计时器过期事件，并在其触发时处置 Counter 组件：

```
import Effect.Aff (launchAff_) ①

main :: Effect Unit
main = do
  HA.runHalogenAff do
    body <- HA.awaitBody
    io <- runUI (Counter.component 3) 0 body
    io.subscribe $ CR.consumer \currentCount -> do
      log $ "Received Count from Top-level Counter: " <> show currentCount
      pure Nothing
    ioTimer <- runUI CountdownTimer.component 15 body
    void $ liftEffect $ HS.subscribe ioTimer.messages ②
      \_ -> launchAff_ io.dispose ③ ④
```

