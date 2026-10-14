
> ❶ 我们的 Stack 定义与前一个示例相比发生了变化。

就像之前一样，当调用 `tell` 时，它由 `StateT` 的实例处理，该实例会 `lift` 其底层 `Monad` 的 `tell` 函数，在本例中是 `ReaderT`。

现在我们的 `ReaderT` 实例，即我们正在尝试编码的那个，将被使用。它需要做与 `StateT` 的实例相同的事情，即 `lift` 其底层 `Monad` 的 `tell` 实现，在这个 Stack 中是 `WriterT`。

因此，我们可以安全地为 `ReaderT` 的 `tell` 编码，假设 `WriterT` 或其他一些表现像 `WriterT` 的 `Monad` 在 Stack 中在其下方某处。

让我们回到我们的代码：

```haskell
instance monadTellReaderT :: MonadTell w (ReaderT r m) where
  tell w = ReaderT \r -> ???
```

我们只需要提升底层 `Monad` 的 `tell` 实例。让我们在调用它之前先看看 `lift` 做了什么：

```haskell
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift = ReaderT <<< const
```

我们可以看到 `lift` 已经为我们创建了一个 `ReaderT`。因此我们可以从我们的 `tell` 中将其移除：

```
instance monadTellReaderT :: MonadTell w (ReaderT r m) where

  tell w = ???
```

现在我们可以简单地 `lift` `tell` 函数：

```
instance monadTellReaderT :: MonadTell w (ReaderT r m) where

  tell w = lift $ tell w -- COMPILER ERROR!!
```

以下是编译器对我们简单解决方案的反对意见：

![](img/8c0e9b687c62642e828ccb5481e11313_931_0.png)

我们在提升 `m`，但 `m` 上没有 Constraint 说明它是 `Monad`。但为什么我们需要这个？

如果我们再次查看 `lift` 的定义，我们会看到它将 `m` 约束为 `Monad`：

```
class MonadTrans t where

  lift :: ∀ m a. Monad m => m a -> t m a
```

由于我们调用了 `lift`，我们需要添加相同的 Constraint：

```
instance monadTellReaderT :: Monad m => MonadTell w (ReaderT r m) where ❶

  tell w = lift $ tell w -- COMPILER ERROR!!
```

❶ 将 `m` 约束为 `Monad`。

现在我们有一个不同的错误：

![](img/8c0e9b687c62642e828ccb5481e11313_932_0.png)

注意编译器错误是在 `tell` 调用下方下划线。错误信息告诉我们缺少 `MonadTell` Constraint。这是因为我们在委托给底层 `Monad` 的 `tell` 实现。

为了做到这一点，底层 `Monad` `m` 最好支持 `MonadTell`。

让我们将 `m` 约束为 `MonadTell`：

```
instance monadTellReaderT

  :: (Monad m, MonadTell w m) => MonadTell w (ReaderT r m) where

  tell w = lift $ tell w
```

1 不要忘记 `MonadTell` 的第一个参数的 Constraint 中的 `w`。

但等等。`MonadTell` 不也是一个 `Monad` 吗？让我们查看 `MonadTell` 的定义，看看我们是否正确：

```
class Monad m <= MonadTell w m | m -> w where

  tell :: w -> m Unit
```

是的，它是。`Monad` 是 `MonadTell` 的超类。所以我们可以移除 `Monad` Constraint，因为 `MonadTell` 已经为我们处理了它：

```
instance monadTellReaderT

  :: MonadTell w m => MonadTell w (ReaderT r m) where

  tell w = lift $ tell w
```

再做一个改进，让我们进行 ETA-reduce 并以 Point-free 方式编写：

```haskell
instance monadTellReaderT :: MonadTell w (ReaderT r m) where
  tell = lift <<< tell
```

记住右手的 `tell` 来自 `m` 的实现，所以这里没有无限递归。

现在，我们可以为 `ReaderT` 编写 `MonadState`。以下是它的定义：

```haskell
class Monad m <= MonadState s m | m -> s where ❶
  state :: ∀ a. (s -> Tuple a s) -> m a ❷
```

+   ❶ 我们之前见过的 Functional Dependency。
+   ❷ `state` 接受一个函数，该函数接受一个状态 `s`，并返回一个计算结果 `a` 和一个新状态，然后它会在底层 `Monad` 的上下文中返回该计算结果。

`state` 的类型签名乍一看可能令人困惑。但让我们想象一下，就一会儿，`get`、`put` 和 `modify` 是 `MonadState` 的一部分：

```haskell
-- FICTITIOUS
class Monad m <= MonadState s m | m -> s where
  get :: m s
  put :: s -> m Unit
  modify :: (s -> s) -> m s
```

以下是 `StateT` 的定义供参考：

```haskell
newtype StateT s m a = StateT (s -> m (Tuple a s)) ❶
```

+   ❶ `StateT` 的包含函数在底层 `Monad` 中返回一个 `Tuple`。

现在，我们将为 `StateT` 实现我们的 FICTITIOUS `MonadState`：

```haskell
-- FICTITIOUS
instance monadStateStateT :: Monad m => MonadState s (StateT s m) where
  get :: StateT s m s
  get = StateT \\s -> pure $ Tuple s s

  put :: s -> StateT s m Unit
  put s = StateT \\_ -> pure $ Tuple unit s

  modify :: (s -> s) -> StateT s m s
  modify f = StateT \\s -> let s' = f s in pure $ Tuple s' s'
```

在全部 3 个方法中，我们都使用 `pure` 将 `Tuple` 包装在底层的 `Monad` 中。

让我们将 `pure` 从每个方法中提取出来：

```haskell
-- FICTITIOUS
instance monadStateStateT :: Monad m => MonadState s (StateT s m) where
  get :: StateT s m s
  get = StateT $ pure <<< \\s -> Tuple s s

  put :: s -> StateT s m Unit
  put s = StateT $ pure <<< \\_ -> Tuple unit s

  modify :: (s -> s) -> StateT s m s
  modify f = StateT $ pure <<< \\s -> let s' = f s in Tuple s' s'
```

并且注意到每个 Lambda 基本上都是相同的模式。事实上，它们都共享相同的类型签名，即 `s -> Tuple a s`。

这正是 REAL `MonadState` 中 `state` 的第一个参数的确切类型签名。

我可以想象写这段代码的人注意到了这个模式，并将其提取为一个名为 `state` 的单一方法。然后他们提取了其他 API 函数，例如 `get`、`put` 和 `modify`，仅举几例，并以 `state` 为基础一次性实现它们作为辅助函数：

```
get :: ∀ m s. MonadState s m => m s

get = state \s -> Tuple s s

put :: ∀ m s. MonadState s m => m Unit

put = state \_ -> Tuple unit s

modify :: ∀ m s. MonadState s m => (s -> s) -> m s

modify f = state \s -> let s' = f s in Tuple s' s'
```

注意每个 API 函数都是以 `state` 编写的。这种提取大大减少了实现 `MonadState` 类型类所需的代码。

让我们从这个小小的 digression 中返回来为 `ReaderT` 编写 `MonadState` 实例。以下是类型类的定义：

```
class Monad m <= MonadState s m | m -> s where

  state :: ∀ a. (s -> Tuple a s) -> m a
```

现在，就像 `tell` 一样，我们知道 `ReaderT` 不负责处理状态管理。

相反，它会将该责任委托给其底层的 `Monad`，因为它知道 `StateT` 或其他最终负责状态的 `Monad` 会在其下方位于栈中，否则它不会被调用。

为了实现这一点，它将从其底层 `Monad` 中提升 `state` 函数。让我们看看我们是如何对 `tell` 做到的，看看我们是否可以用 `state` 做类似的事情：

```
instance monadTellReaderT

  :: MonadTell w m => MonadTell w (ReaderT r m) where

  tell = lift <<< tell
```

我看不出我们为什么不能在这里做同样的事情：

```
instance monadStateReaderT

  :: MonadState s m => MonadState s (ReaderT r m) where ①

  state = lift <<< state
```

① 我们确保将 `m` 约束为支持 `MonadState`，因为我们正在委托给它的实现。

并且由于它可以编译，我们可以记下这可能是一个我们可以依赖的模式。例如，我们可以预期 `WriterT` 对 `state` 的实现为：

```
instance monadStateWriterT

  :: (Monoid w, MonadState s m) => MonadState s (WriterT w m) where ❶

  state = lift <<< state
```

❶ 我们在这里有 2 个约束。首先，`w` 必须是 `Monoid`，因为 `WriterT` 的 `lift` 实现具有该约束。其次，由于我们正在提升底层 `Monad` 的 `state` 函数，它最好是一个 `MonadState`。

事实证明，这与 PureScript 库中的实现相同，唯一的区别是我们的版本是无点的。

因此，当我们实现超出我们责任范围的方法时，例如在 `ReaderT` 中写入日志，我们只需提升底层 `Monad` 的实现即可。

在下一章编写 `StateT` 时请记住这一点。

并且这就完成了更常见的 API 函数。我们不必编写 `get`、`put`、`modify_`、`modify` 或 `asks`，因为它们都是以实例实现为基础编写的。

顺便说一下，还有其他 API 函数，但使用频率远低于这些，所以我们在这里不关心它们。但请随意查看 Pursuit 以了解 Monad Transformer 包中还有哪些其他类型类。

## 20.10. 组合子的威力

Monad Transformer 是一种组合子。就像解析器组合子接受其他解析器一样，Monad Transformer 接受其他 Monad。

正如我们在解析器中所看到的，真正的威力来自于组合多个组合子，就像我们在名为 `digits` 的解析器中所看到的那样：

```
digits :: ∀ e. ParserError e => Parser e String

digits = some' digit
```

`digits` 由组合子 `some'` 构建，`some'` 是一个解析器组合子，它接受一个解析器，在本例中为 `digit`。但不要忘记 `digit` 本身也是由另一个解析器组合子 viz. `satisfy` 构建的：

```
digit :: ∀ e. ParserError e => Parser e Char

digit = satisfy "digit" (isDecDigit <<< codePointFromChar)
```

当我们编写 `some` 时，`some'` 就是基于它，我们并没有考虑使用组合子构建的解析器所涉及的所有复杂性，以及该组合子是否建立在另一个组合子之上，等等。

我们只关心处理传递给我们的解析器。

Monad Transformer 也是如此。它们只关心它们在类型定义中接收到的 `Monad`，即我们所说的底层 `Monad`。

如果每个 `Monad` 都关心其底层 `Monad`，那么我们就可以从它们的栈中获得相当复杂的行为。这正是我们所看到的。

有时试图理解这种复杂性会让人头晕，但如果回顾我们编写的代码，你会注意到我们并没有被整体的复杂性困住。我们只一次集中于一个部分，即我们正在处理的 Monad Transformer。

如果该 Transformer 正确地与其底层 `Monad` 协作，那么对我们来说并不重要，该 `Monad` 是另一个像 `StateT` 这样的 Transformer，还是像 `Identity` 或 `Effect` 这样普通的 `Monad`。

再次，我们看到了如何通过组合简单事物获得强大的能力，例如函数式组合、Monadic Bind、解析器组合子，现在是 Monad Transformer。

## 21.1. 编写 StateT Monad Transformer

在上一章中，我们一起编写了 `WriterT` 和 `ReaderT`，现在轮到你从头开始编写一个 Monad Transformer，即 `StateT`。

让我们先从编码类型开始。记住 `State` 持有接受状态值 `s` 并产生纯计算 `a` 以及 Monadic 计算，即新状态的函数。

记住这一点，在阅读之前先写下 `StateT` 的类型定义。尽量不要回头查看你是如何编码 `State` 的。这将有助于看看你记住了多少。

事实上，如果你先写下 `State` 的定义可能会有所帮助。在继续阅读之前尝试一下，如果卡住了，再稍稍阅读以获得简单提示。

如果你卡住了记不起，这里是 `State` 的类型定义：

```
newtype State s a = State (s -> Tuple a s)
```

如果你需要这个提示，现在就停下来，在继续之前尝试完成 `StateT` 的类型定义。

`StateT` 与上面的 `State` 定义非常接近，最大的区别是 `StateT` 有一个底层 `Monad`，并且该函数在该 `Monad` 中返回其计算结果：

```
import Data.Tuple (Tuple) ①

newtype StateT s m a = StateT (s -> m (Tuple a s))
```

① 不要忘记导入 `Tuple`。

花点时间将此定义与 `State` 的进行比较。

接下来，编写 `runStateT`。同样，尽量不要查看你为 `runState` 编写的代码。在继续阅读之前先试试。

我们迄今为止编写的所有 run 函数都只是解包包含的函数：

```
runStateT :: ∀ s m a. StateT s m a -> (s -> m (Tuple a s)) ①

runStateT (StateT f) = f
```

① 我保留了冗余的括号以帮助传达我们正在返回一个函数。

现在，编写 `StateT` 的 `Functor` 实例，并且在编写时请记住我们必须处理底层 `Monad`。

![](img/8c0e9b687c62642e828ccb5481e11313_942_0.png)

如果记得的话，我们在编码 `ReaderT` 时也遇到过同样的问题。我们使用了 `<#>`，它就是 `map`，需要至少一个 `Functor`。所以我们需要为 `m` 添加一个 `Functor` 约束：

```
instance functorStateT :: Functor m => Functor (StateT s m) where

  map f (StateT mg) =

    StateT \s -> mg s <#> \(Tuple x s') -> Tuple (f x) s'
```

注意，我们只为实例代码能够编译所需的程度约束 `m`。我们完全可以把它做成 `Monad`，它仍然会工作。但有限的方法更好，因为它告诉我们实例实现需要什么，在我们的例子中，我们只使用了 `map`，所以 `Functor` 约束就足够了。

接下来要编码的是 `Apply` 实例。在阅读更多内容之前，尽可能写下去。

我们从实例定义开始：

```
