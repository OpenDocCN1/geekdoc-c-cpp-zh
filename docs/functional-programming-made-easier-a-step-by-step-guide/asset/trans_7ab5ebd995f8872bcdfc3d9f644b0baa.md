

一起。

以下是 `MonadError` 的参考：

```purescript
class MonadThrow e m <= MonadError e m | m -> e where
  catchError :: ∀ a. m a -> (e -> m a) -> m a
```

让我们从实例定义开始：

```purescript
import Control.Monad.Error.Class (class MonadThrow, class MonadError, throwError)

instance monadErrorStateT :: MonadError e (StateT s m) where
```

❶ 将 `MonadError` 添加到导入列表中。

此时，我正在思考约束。因为 `StateT` 本身不处理错误，我们必须将此调用委托给底层的 `Monad`。

要使其工作，我们的底层 `Monad` 必须支持 `MonadError`。我们之前在 `MonadAsk` 和 `MonadTell` 中见过这种情况。我们需要将其添加为约束：

```purescript
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
```

❶ 底层 `Monad` 被约束为 `MonadError`。

由于此方法与其他方法非常不同，我们将为 `catchError` 添加专门针对 `StateT` 的类型签名，以帮助我们跟踪我们的类型：

```purescript
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
```

接下来我们将添加实现左侧：

```purescript
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = ???
```

❶ 名称 `fmx` 是为了提醒我们，我们有一个返回底层 `Monad` 中值的函数。

② `f` 是将被调用以处理错误的函数。它接收错误 `e`，并返回一个“替换”失败的 `StateT` 的 `StateT`。

接下来，我们使用我们通常的模式：

```purescript
instance monadErrorStateT
  :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \s -> ???
```

现在是最困难的部分。这就是我们进行思考的地方。

我们有 3 件事需要处理：

- 底层 Monad，即其 catchError 实现
- fmx
- f

我们知道我们最终会委托给底层 Monad，因为 StateT 不处理错误。为此，我们将调用底层 Monad 的 catchError。

让我们添加它：

```purescript
import Control.Monad.Error.Class (class MonadThrow, class MonadError, throwError, catchError)

instance monadErrorStateT
  :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \s -> catchError ??? ???
```

① 将 `catchError` 添加到导入列表中。

`catchError` 的第一个参数是底层 Monad 上下文中的值。那么我们如何获得这样的东西呢？

要回答这个问题，请回顾我们剩下的 2 件事。你能看到能提供这个的东西吗？

如果不能，那么是时候写出类型了。为此，我们将参考 `catchError` 的专门类型签名：

```purescript
fmx :: s -> m (Tuple a s)
f :: e -> StateT s m a
```

现在你能看到能提供底层 Monad 中单子值的东西吗？

我们可以看到从上面的类型中，`fmx` 会提供它。但，我们需要给它一个状态值，而我们可以在 Lambda 表达式中获得状态值 `s`：

```purescript
instance monadErrorStateT
  :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \s -> catchError (fmx s) ???
```

查看 `catchError` 类型签名中的第二个参数，我们可以看到我们有一个接受错误并返回 StateT 的函数。让我们添加它的骨架：

```purescript
instance monadErrorStateT
  :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \s ->
      catchError (fmx s) \e -> ???
```

① 添加了 Lambda，`\e -> ???`。

在此错误处理程序中，我们需要调用 `f`，它是 StateT 的 `catchError` 最初传递的错误处理程序。让我们添加它：

```purescript
instance monadErrorStateT
  :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \s ->
      catchError (fmx s) \e -> f e ???
```

现在，在继续之前，我们需要知道 `f e` 的类型是什么：

```purescript
f :: e -> StateT s m a
f e :: StateT s m a
```

你还记得当我们有类似情况时我们做了什么吗，即我们在 Lambda 的右侧有一个 StateT？

在阅读之前回顾 bind 实现，看看我们之前做了什么。

你注意到我们只是调用了 `runStateT` 吗？

由于它在那里可以为我们提供底层 Monad 中的单子值，所以在这里也可以：

```purescript
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
    catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
    catchError (StateT fmx) f = StateT \s ->
        catchError (fmx s) \e -> runStateT (f e) ???
```

现在是关键。`runStateT` 需要第二个参数的状态，但我们从哪里获取状态呢？

我们唯一拥有的状态是我们传递给 `fmx` 的同一个状态。所以这是我们唯一能用的状态。因此我们将使用它：

```purescript
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
    catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
    catchError (StateT fmx) f = StateT \s ->
        catchError (fmx s) \e -> runStateT (f e) s
```

在阅读之前，请确保在代码中添加此内容。

注意，我们将相同的状态传递给了 `fmx` 和 `f`。这与我们在函数中处理多个位置的状态时所做的其他所有事情都非常不同。

通常，我们从使用状态的第一个函数中捕获修改后的状态，并将该修改后的版本传递给需要状态的下一个函数。

我们在这里无法做到这一点，因此最好的办法是使用相同的状态。这意味着如果 `fmx` 调用 `throwError`，`fmx` 对状态所做的任何更改都将丢失。

我们将在后面更详细地讨论这个问题。

## 21.4. 测试我们的 StateT 实现

我们希望测试我们新创建的 Monad 转换器，看看它是否表现正确。为此，我们将借用上一章中看到的一些想法和部分代码。

让我们从应用程序堆栈定义开始：

```purescript
import Control.Monad.Except.Trans (ExceptT)
import Control.Monad.Writer.Trans (WriterT)

type AppStack e w s a = ExceptT e (WriterT w (StateT s Effect)) a
```

① 我们需要这些导入来创建此类型别名。

请将其添加到你的代码中。

以下是我们堆栈的图表：

![](img/8c0e9b687c62642e828ccb5481e11313_977_0.png)

现在，定义一个名为 `AppM` 的应用程序 Monad 的类型别名，利用我们的堆栈定义。我们希望我们的错误为 `String`，我们的状态为 `Int`，我们的日志为 `String`，并且应用程序的最终结果为 `Unit`。

在继续之前编写此代码。

应用程序 Monad 只是为 AppStack 定义中的多态类型提供单态类型：

```purescript
type AppM = AppStack String String Int Unit
```

接下来，我们需要一种运行 Monad 堆栈的方法，因此我们需要一个名为 `runApp` 的函数，它将接收初始状态和应用程序 Monad 并产生结果。

在阅读进一步内容之前，尝试编写 `runApp` 的类型签名。

此类型签名需要我们在上一章中讨论过的分析，即遍历我们堆栈中的类型以弄清楚返回类型。或者，我们也可以用类型孔作弊。作弊容易得多，所以让我们使用类型孔：

```purescript
runApp :: Int -> AppM -> Effect _
```

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

