
请记住，我们在堆栈底部有 `Effect` Monad。由于 `Effect` 是我们通过 `main` 函数返回给 PureScript 的内容，因此没有 `runEffect` 函数。

这就是为什么我们返回 `Effect` Monad 的原因。我们将在本书的 Beyond 部分更详细地讨论 `Effect` 和 `main`。

`_` 是我们的类型孔。注意它没有命名。你可以在类型签名中拥有未命名的类型孔。它只是为了让编译器在我们的代码编译后为我们提供推断的类型。

下一步是编写 `runApp` 函数的其余部分，记住使用每个 Monad 的单个 run 函数，从顶部开始，逐步向下工作，直到到达 `Effect`。

作为参考，以下是 run 函数的类型签名：

```purescript
runExceptT :: ∀ e m a. ExceptT e m a -> m (Either e a)

runWriterT :: ∀ w m a. WriterT w m a -> m (Tuple a w)

runStateT :: ∀ s m a. StateT s m a -> (s -> m (Tuple a s))
```

在阅读进一步内容之前，请编写 `runApp` 的其余部分。

我们将通过执行堆栈顶部的 Monad，即 ExceptT 来开始：

```purescript
runApp :: Int -> AppM -> Effect _

runApp st = ??? <<< runExceptT
```

然后是堆栈中下一个 Monad，即 WriterT：

```purescript
runApp :: Int -> AppM -> Effect _

runApp st = ??? <<< runWriterT <<< runExceptT
```

最后，堆栈中最后一个可运行的 Monad，即 StateT：

```purescript
runApp :: Int -> AppM -> Effect _

runApp st = flip runStateT st <<< runWriterT <<< runExceptT
```

① 通过翻转 `runStateT`，我们可以先提供第二个参数，即初始状态。这使我们能够使用函数组合以无点方式编写 `runApp`，使 `AppM` 参数未命名。

我们会得到一些编译器错误，因为我们没有导入 `runWriterT` 和 `runExceptT` 定义。我们不需要从库中包含 StateT，因为我们自己编写了它。

让我们添加导入：

```
import Control.Monad.Except.Trans (ExceptT, runExceptT)

import Control.Monad.Writer.Trans (WriterT, runWriterT)
```

现在我们的代码可以编译了，编译器对我们的类型孔给出了一个警告：

![](img/8c0e9b687c62642e828ccb5481e11313_979_0.png)

继续根据此警告消息更新你的类型签名。提示：你可以在 VSCode 中将鼠标悬停在黄色下划线的代码上，然后从弹出消息中选择文本并复制粘贴到代码中。

这里是该更改：

```
import Data.Either (Either) ①

runApp
  :: Int
  -> AppM
  -> Effect (Tuple (Tuple (Either String Unit) String) Int)

runApp st = flip runStateT st <<< runWriterT <<< runExceptT
```

① 这是我们在此模块中首次使用 Either，因此我们需要导入它。

让我们像上一章那样提取该返回类型，去掉 Effect 部分。为其创建一个类型别名并将其命名为 StackResult。然后继续。

这里是该重构：

```
type StackResult = Tuple (Tuple (Either String Unit) String) Int

runApp :: Int -> AppM -> Effect StackResult

runApp st = flip runStateT st <<< runWriterT <<< runExceptT
```

接下来，创建一个名为 AppEffects 的类型别名，它是一个记录，用于存储运行我们的栈的副作用。这将以与顺序无关的方式保存我们栈的副作用。不要忘记包含纯计算结果。

请先尝试一下，然后继续阅读。

这里就是：

```
type AppEffects =
  { log :: String ①
  , state :: Int ②
  , result :: Maybe Unit ③ ④
  }
```

① WriterT Monad 的副作用将存储在这里。它是最终的日志。

② StateT Monad 的副作用将存储在这里。它是最终的状态。

③ 纯计算值将存储在这里。在这种情况下，它唯一可能的值是 Unit。它在这里是为了展示 AppEffects 通常应包含的内容，即使在我们的情况下它是平凡的。

④ 这是一个 Maybe，因为可能出现错误，这意味着我们不会有最终结果。

现在我们有了 AppEffects，调用我们应用程序代码的代码，即我们的 Monad 栈，可以与栈顺序隔离开来。

现在，让我们创建一个名为 AppResult 的类型别名，其中包含运行我们的 Monad 栈的副作用值，即 AppEffects，以及可选的错误如果发生的话。

先做这个，然后继续阅读。

我们有 2 种方法可以采用，创建记录或使用元组。两者都可以，但由于我们只有 2 个东西，我将使用元组：

```
type AppResult = Tuple (Maybe String) AppEffects ①
```

① 错误位于元组的第一个位置。我在这里使用 Maybe，因为可能没有发生错误。

继续更改你的代码以匹配这一点，以便我们今后使用相同的类型进行编码。

顺便说一下，我们本可以将 AppResults 中的结果设为 Either 并在其中放置纯计算结果或错误。然后我们就不需要元组了。我们在这里拥有的与那是同构的，所以我们暂时保留我们拥有的东西。如果证明有问题，我们以后会更改它。

现在，我们想要编写一个函数，我们将调用它 results，用于获取我们的 StackResult，它与栈顺序紧密耦合，并将其转换为 AppResult，它与栈顺序松散耦合。

当两个或多个事物紧密耦合并且其中一个发生变化时，其他的必须发生变化。

当两个或多个事物 *松散耦合* 并且其中一个发生变化时，其他的很可能不需要发生变化。很多时候，只需要在接口或映射函数中进行更改。

在我们的例子中，你即将编写的 `results` 函数将获取我们的 `StackResult`，它与栈顺序紧密耦合并将其映射到 `AppResult`，它松散耦合。

就记录而言，它与栈中的 Monad 紧密耦合，但与顺序无关。而 `result` 函数将与我们的栈顺序紧密耦合。

现在，在继续之前，先编写 `results`，它接受一个 `StackResult` 并生成一个 `AppResult`。

我们将从类型签名开始：

```
results :: StackResult -> AppResult
```

类型签名反映了 `results` 将 `StackResult` 映射到 `AppResult`。这里的术语 *map* 可能会令人困惑。我不是在 `Functors` 的上下文中使用它。它以函数的方式从其定义域映射到其值域。

接下来，我们将编写错误情况：

```
import Data.Either (Either(..)) ①

import Data.Maybe (Maybe(..)) ②

results :: StackResult -> AppResult

results (Tuple (Tuple (Left err) l) s)
  = Tuple (Just err) { log: l, state: s, result: Nothing } ③
???
```

① 添加 (..) 以导入 Left。

② 添加 (..) 以导入 Nothing。

③ 注意这里没有结果。那是因为发生了错误。

现在是成功情况：

```
results :: StackResult -> AppResult

results (Tuple (Tuple (Left err) l) s)
  = Tuple (Just err) { log: l, state: s, result: Nothing }

results (Tuple (Tuple (Right result) l) s) ①
  = Tuple Nothing { log: l, state: s, result: Just result }
```

① 在我们的例子中，这里 result 只是 unit。

注意唯一的区别是在元组的第一个位置和计算结果。我们仍然捕获日志和状态。

我们现在有了足够的管道来允许我们编写应用程序代码。此代码将在我们的应用程序 Monad AppM 中运行。我们将调用此函数 app。

首先通过在阅读更多内容之前仅编写类型签名来开始此过程。

这里是类型签名：

```
app :: AppM
```

花点时间意识到当我们调用此函数时，它不会执行我们编写的任何指令。它会在 Monad 中包装 Monad 并将 Monad 函数组合在一起以产生单个、单一的 AppM 类型的 Monad。

这个单一的 Monad 将在我们稍后的代码中执行，当我们将其连同初始状态一起传递给 runApp 时。我们也可以选择不执行这个 Monad。完全由我们决定。

重要的是不要认为调用 app 就是执行代码。它会延迟到我们调用 runApp 时执行，我们的栈会从上到下逐层执行。

现在，app 主体的要求按指定顺序如下：

+   - 将 "Starting App..." 写入日志
+   - 获取状态
+   - 检查状态是否为非零，否则报错 "WE CANNOT HAVE 0 STATE!"
+   - 将 1 加到状态
+   - 将 "Incremented State" 写入日志
+   - 返回纯计算值

在阅读以下提示之前，先编写 app 主体的其余部分。

如果你在这方面遇到困难，请记住：

+   - 以 do 块开始编码
+   - get 和 put 用于读写状态（在 Pursuit 上查找它们）
+   - tell 写入日志
+   - 纯计算值是 AppStack 中的 a
+   - 去 Pursuit 上查找 when 如何检查非零

+   - 函数 throwError 会短路我们的 do 块

 hopefully，这些提示会帮助你完成。请继续在尚未完成的情况下工作代码。

要添加到 app 的第一件事是 do 块，因为我们在 AppM Monad 中操作。实际上，我们会对任何 Monad 都这样做：

```
app :: AppM

app = do
  ???
```

要求中的第一步是记录一个字符串。我们将使用 tell：

```
app :: AppM

app = do
  tell "Starting App..."
  ???
```

如果你卡住了并且这有助于突破那堵砖墙，停止阅读并看看是否能完成编码此函数。

接下来，我们将获取状态。我们将使用 get 并将状态捕获到 n 中：

```
import Control.Monad.State.Class (class MonadState, get) ①

app :: AppM

app = do
  tell "Starting App..."
  n <- get
  ???
```

① 将 get 添加到导入列表中。

然后我们将检查状态是否为非零。我们将使用 when：

```
app :: AppM

app = do
  tell "Starting App..."
  n <- get
  when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!" ①
  ???
```

① throwError 是一个 m a，但 when 需要一个 m Unit。所以我们使用 void 将 m a 转换为 m Unit。

下一个要求是向状态添加 1。我们将使用 put：

```
import Control.Monad.State.Class (class MonadState, get, put) ①

app :: AppM

app = do
  tell "Starting App..."
  n <- get
  when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
  put $ n + 1
  ???
```

① 将 put 添加到导入列表中。

然后我们将再次使用 tell 写入日志：

```
app :: AppM

app = do
  tell "Starting App..."
  n <- get
  when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
  put $ n + 1
  tell "Incremented State"
  ???
```

最后，我们将返回纯计算值。但在这样做之前，我们将回顾我们的定义：

```
type AppStack e w s a = ExceptT e (WriterT w (StateT s Effect)) a ①

type AppM = AppStack String String Int Unit ②
```

① a 是纯计算结果。

② 在这里我们将多态类型参数 a 设置为单态类型 Unit。

所以，我们必须返回类型为 Unit 的值。幸运的是，这很容易，因为该类型的唯一居民是 Unit：

```
app :: AppM

app = do
    tell "Starting App..."
    n <- get
    when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
    put $ n + 1
    tell "Incremented State"
    pure unit ①
```

① 不要忘记 pure。这是因为所有 do 块都必须返回一个 Monad 值。

现在，将你的测试代码改为如下：

```
test :: Effect Unit

test = do
    result1 <- runApp 0 app
    log $ show result1 ①
    result2 <- runApp 99 app
    log $ show result2 ②
```

① 打印 (Tuple (Tuple (Left "WE CANNOT HAVE A 0 STATE!") "Starting App...") 0)。

② 打印 (Tuple (Tuple (Right unit) "Starting App...Incremented State") 100)。

继续运行你的代码，看看是否正常工作。

现在让我们改进代码，以便获得解耦的输出，即 AppResult，而不是耦合的输出 StackResult。

我们将通过调用 results 来实现这一点。

有 2 个地方可以这样做。其中一个比另一个更好。在阅读后续内容之前，先看看你会在哪里放置对 results 的调用。

我们可以在测试代码中放置对 results 的调用，但那样的话，每次调用 runApp 时都必须放置一次。所以，为什么不直接把它放在 runApp 中呢？

这就是我们要做的。如果你还没有这样做，现在就修改 runApp 使用 results。然后继续阅读。

以下是修改后的 runApp 函数：

```
runApp :: Int -> AppM -> Effect AppResult

runApp st =
    (results <$> _) <<< flip runStateT st <<< runWriterT <<< runExceptT
```

1 将 StackResult 改为 AppResult。

2 创建一个匿名函数以保持代码无点式。

如果你使用了非无点式版本也没关系。它看起来像这样：

```
runApp :: Int -> AppM -> Effect AppResult

runApp st ap =
    results <$> (flip runStateT st $ runWriterT $ runExceptT ap)
```

1 注意 <<< 被改为 $，即在 ETA-reduction 中所做的相反更改。

我个人更喜欢无点式版本。

让我们回顾一下测试代码，以及使用这个新更改后我们可以期望它打印什么：

```
test :: Effect Unit

test = do
    result1 <- runApp 0 app
    log $ show result1
    result2 <- runApp 99 app
    log $ show result2
```
