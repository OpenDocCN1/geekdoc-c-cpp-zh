
```scala
nested :: Nested { debug :: Boolean } { count :: Int } String Unit Unit
nested = do
  { debug } <- ask
  { count } <- lift get
  lift <<< lift $ tell $ "The count is: " <> show count
  pure unit
```

- 1. `ReaderT` 没有 `lift` 调用。
- 2. `StateT` 有 1 次 `lift` 调用。
- 3. `WriterT` 有 2 次 `lift` 调用。

在此示例中，所有 `lift` 调用都是为了包装不同的 Monad API 调用。我们将 `StateT` 的 API 函数 `get` 提升一次，因为它在我们的 Monad 栈中是从顶部数第二个。我们将 `WriterT` 的 API 函数 `tell` 提升两次，因为它是从顶部数第三个。

数 `lift` 调用的次数很痛苦，但想象一下我们更改栈顺序的场景。我们必须遍历代码更改 `lift` 调用的次数以再次使计数正确。编译器会在这里帮助我们，因为类型会错误，但这是一个繁琐而痛苦的过程。

由于我们经常使用 API 函数与这些 Monad 交互，如果我们不必担心提升它们就好了。更好的是，我们不必担心调用 `lift` 的次数。

那么我们该如何做到这一点？

一种方法是我们要求 `ReaderT`、`StateT` 和 `WriterT` 各自支持相同的 API。例如，`ReaderT` 将支持 `tell`，`StateT` 也支持。但两者都会将 `tell` 调用委托给其底层 `Monad`。

`ReaderT` 的 `tell` 函数将提升其底层 `Monad` 的 `tell` 函数，在我们示例栈的情况下是 `StateT`：

![](img/8c0e9b687c62642e828ccb5481e11313_883_0.png)

`StateT` 的 `tell` 函数将做同样的事情并提升其底层 `Monad` 的 `tell` 函数，在我们示例栈的情况下是 `WriterT`：

![](img/8c0e9b687c62642e828ccb5481e11313_884_0.png)

`WriterT` 是 `tell` 的实现位置，因此它只是将日志追加。

注意使用这种方法 `tell` 被提升了 2 次。它被提升了恰好满足此栈所需的次数。如果我们有不同的栈，它将被提升恰好满足该特定栈所需的次数，例如：

![](img/8c0e9b687c62642e828ccb5481e11313_884_1.png)

在此栈中，它只被提升一次，因为提升在实际实现 API 调用的 `Monad` 处终止，在本例中为 `WriterT`。

实现 API 调用的正确方法是使用类型类，因为我们有多个类型，即不同的 Monad 转换器，以及相同的一组函数。下面是在 PureScript 中支持 `tell` 的类型类：

```
class Monad m <= MonadTell w m | m -> w where

  tell :: w -> m Unit
```

- 1. 注意函数依赖 `| m -> w`，它表示对于每个 `Monad` `m`，只能有一个 `w`。这看起来可能有限制，但在实践中你的程序通常只有一个 Monad 栈。此依赖可能被添加来帮助编译器更好地确定类型，这意味着我们不需要在代码中指定显式的 Types。

让我们来看 `ReaderT` 对 `MonadTell` 的实现。首先，我们需要查看 `ReaderT` 的 `lift`：

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where

  lift :: ∀ m a. Monad m => m a -> ReaderT r m a

  lift = ReaderT <<< const
```

① 专门针对 `ReaderT` 的 Type Signature。

`lift` 只是将 Monadic Value，`m a`，包装在一个 `ReaderT` 中，其函数通过 `const` 忽略只读值，并返回该 Monadic Value。

以下是 `ReaderT` 的 `tell` 代码：

```
instance monadTellReaderT

  :: MonadTell w m => MonadTell w (ReaderT r m) where

  tell :: w -> ReaderT r m Unit

  tell = lift <<< tell
```

很容易认为这是一个无限递归，因为 `tell` 在等号两边都出现了。如果 `tell` 不是 Typeclass Method，就会是这种情况，因为它会引用自身。

但当我们在等号两边都处理 Typeclass Method 时，我们通常是在查看该 Method 的不同实例。

在这种情况下，右手边的 `tell` 是底层 `Monad`，`m` 所实现的 `tell`。

编译器会看到我们将其与 `lift` 函数组合，并确定它只能是底层 `Monad` 的 `tell`，因为这就是 `lift` 所期望的，即一个 `m a`（参见针对 `ReaderT` 专门化的 `lift` 的 Type Signature）。

## 20.2. Monad Transformers 和它们的 APIs

Monad Transformers 是转换其他 Monads 的 Monads。它们通过从其他 Monads 中取出 Monadic Values，然后通过将它们提升到自己的 Context 中来转换它们。当它们被运行时，它们只是返回原始的 Monadic Value。

Monad Transformers 在 PureScript 库 `purescript-transformers` 中。这意味着你必须将 `transformers` 添加到你的 `spago.dhall` 文件中才能使用它们。

以下是一些更常见的 Monad Transformers：

```
ReaderT r m a

WriterT w m a

StateT s m a

ExceptT e m a ①
```

① 我们还没有见过这个 Type。它用于处理错误。

而一般形式是：

```
t m a
```

`t` 是 Monad Transformer，`m` 是底层 `Monad`，`a` 是 Pure Value。

当你考虑 `lift` 的 Type Signature 时，这种形式是有意义的：

```
class MonadTrans t where

  lift :: ∀ m a. Monad m => m a -> t m a ①
```

① 这里 `t` 可以是 `ReaderT r` 或 `WriterT w` 或 `StateT s` 或 `ExceptT e` 等。

以下是许多更常见 API 的 Typeclass 定义：

```
class Monad m <= MonadAsk r m | m -> r where

  ask :: m r

class Monad m <= MonadTell w m | m -> w where

  tell :: w -> m Unit

class Monad m <= MonadState s m | m -> s where

  state :: ∀ a. (s -> (Tuple a s)) -> m a

class Monad m <= MonadThrow e m | m -> e where

  throwError :: ∀ a. e -> m a

class MonadThrow e m <= MonadError e m | m -> e where

  catchError :: ∀ a. m a -> (e -> m a) -> m a
```

以下是许多更常见的 helper API Functions：

```
asks :: ∀ r m a. MonadAsk r m => (r -> a) -> m a

get :: ∀ m s. MonadState s m => m s

put :: ∀ m s. MonadState s m => s -> m Unit

modify :: ∀ s m. MonadState s m => (s -> s) -> m s

modify_ :: ∀ s m. MonadState s m => (s -> s) -> m Unit
```

这些 helper 是基于 Typeclass Methods 编写的，这就是为什么它们都有 Constraints。也是为什么这些只需要写一次。

## 20.3. 错误 Monad Transformer，`ExceptT`

我们之前见过 `ExceptT` 的一瞥。但 `ExceptT` 到底做什么以及为什么有用？

要回答这个问题，我们应该从它的定义开始：

```
newtype ExceptT e m a = ExceptT (m (Either e a))
```

你可以看到它与 `Either` 并没有太大区别。那么为什么不直接使用 `Either` 并制作一个 `EitherT` 呢？原因很复杂。但基本上这与历史和 Haskell 生态系统中竞争的库开发试图避免名称冲突有关。PureScript 开发者决定保留该名称以保持与 Haskell Type 的熟悉度。

可以说，`ExceptT` 基本上就是 `EitherT`。

请不要将其与其它语言中的 Exceptions 混淆。它不是 Exception。想想 `Either` 是如何工作的，然后加上 transformer 逻辑，你就得到了 `ExceptT`。

`MonadThrow` 和 `MonadError` Typeclasses 在 `ExceptT` 中实现。所有其它 Monad Transformers 只是将这些 Typeclass Methods 委托给它们的底层 Monads，并期望 `ExceptT` 或类似的东西会在 Monad Stack 中位于其下方。

## 20.4. Monad Stack 顺序

Monad Stack 的顺序很重要。看下面的例子：

|  |  |
|---|---|
| `ExceptT` | `runExceptT` |
| `WriterT` | `runWriterT` |
| `StateT` | `runStateT` |
| `Identity` | `unwrap` |

我们将使用 REPL 来帮助我们根据我们如何运行这个 Stack 确定最终结果：

```
$ npx spago repl

PSCi, version 0.14.1

Type :? for help

> import Prelude

> import Control.Monad.State.Trans

> import Control.Monad.Writer.Trans

> import Control.Monad.Except.Trans

> :t flip runStateT unit <<< runWriterT <<< runExceptT ①

forall t17 t18 t20 t9. ExceptT t20 (WriterT t17 (StateT Unit t9)) t18 -> t9 (Tuple (Tuple (Either t20 t18) t17) Unit)
```

① 我们使用 `unit` 作为初始 State。

让我们清理一下那个 Type Signature：

```
-- original

flip runStateT unit <<< runWriterT <<< runExceptT ①

:: forall t17 t18 t20 t9

  . ExceptT t20 (WriterT t17 (StateT Unit t9)) t18 ②

-> t9 (Tuple (Tuple (Either t20 t18) t17) Unit)

-- cleaned up

flip runStateT s <<< runWriterT <<< runExceptT ③

:: ∀ e w s m a

  . ExceptT e (WriterT w (StateT s m)) a ④

-> m (Tuple (Tuple (Either e a) w) s) ④

-- return Value

m (Tuple (Tuple (Either e a) w) s) ⑤
```

- 1. 我们从上到下运行我们的 Stack，这可以从右到左看出，因为我们正在组合 run Functions。
- 2. 注意这个 Type 如何与我们的 Stack 匹配。
- 3. 用 `s` 替换了 `unit`。
- 4. 用 `s` 替换了 `Unit`。
- 5. 最终 Value。

注意我们最终会得到某个 `Monad`，`m` 中的最终 Value。在我们上面的 Stack 图中，这将是 `Identity`。

另一种确定最终返回 Type 的方法是查看每个 run Functions 的 Type Signatures 并进行一些简单的分析：

```
runExceptT :: ∀ e m a. ExceptT e m a -> m (Either e a)

runWriterT :: ∀ w m a. WriterT w m a -> m (Tuple a w)

runStateT :: ∀ s m a. StateT s m a -> s -> m (Tuple a s)
```

当我们第一次调用 `runExceptT` 时，我们会得到 `m (Either e a)`。`(Either e a)` 将是下一个 `Monad` 在 Stack 中的 `a`，在本例中是 `WriterT`。

然后我们调用 `runWriterT`，它返回 `m (Tuple a w)`，并且在将前一个 `Monad` run 返回的内容代入 `a` 后，我们得到：

```
m (Tuple (Either e a) w)
```

`Tuple (Either e a) w` 将是下一个 `Monad` 在 Stack 中的 `a`，即 `StateT`。

最后，我们调用 `runStateT`，它返回 `m (Tuple a s)`，并且在将前一个 `Monad` run 返回的内容代入后，我们得到：

```
m (Tuple (Tuple (Either e a) w) s)
```

当我们解包它时，因为 `m` 在我们的 Stack 图中是 `Identity`，我们最终得到：

```
Tuple (Tuple (Either e a) w) s
```

注意当我们遇到错误时，我们也会得到日志，`w`，最终 State，`s` 和错误，`e`。显然，我们不会得到 Pure Computational Value，因为计算失败了。

这意味着我们的日志和状态是它们在失败点的值。这对于确定出了什么问题非常有帮助。

现在，让我们将 `ExceptT` 向下移动 1 层 Stack：

![](img/8c0e9b687c62642e828ccb5481e11313_890_0.png)

要运行这个 Stack，我们将首先调用 `runWriterT`：

```
m (Tuple a w)
```

然后我们将调用 `runExceptT` 返回：

```
m (Either e (Tuple a w)) ①
```

① `a` 被 `Tuple a w` 替代，即来自 `runWriterT` 的 `a`。

最后，我们将调用 `runStateT`：

```
m (Tuple (Either e (Tuple a w)) s) ①
```

① `a` 被 `Either e (Tuple a w)` 替代，即来自 `runStateT` 的 `a`。

因为 `m` 是 `Identity` 而解包：

```
Tuple (Either e (Tuple a w)) s
```

这次，当我们遇到错误时，我们会丢失日志，`w`。那是因为 `Either e (Tuple a w)` 只有在没有错误时才会给我们日志。

看起来如果发生错误，我们会丢失 `ExceptT` 层以上的所有内容。

让我们通过将 `ExceptT` 再向下移动 1 层来测试该假设，看看我们是否会丢失我们的 State，`s`：

![](img/8c0e9b687c62642e828ccb5481e11313_891_0.png)

当我们这样做时，我们得到：

```
m (Tuple a w)          -- runWriterT

m (Tuple (Tuple a w) s)  -- runStateT

m (Either e (Tuple (Tuple a w) s))  -- runExceptT
```

解包之后：

```
Either e (Tuple (Tuple a w) s)
```

对于这个栈，如果发生错误，我们也会丢失 State，即 `s`。实际上，当 `ExceptT` 位于我们的变换器栈的底部（不包括基础 `Monad` `Identity`）时，一旦发生错误，我们会丢失所有东西。

## 20.5. 使用 Monad 变换器编写代码

让我们编写一些在 Monad 栈中运行的代码。

为此，我们要选择一个将 `ExceptT` 放在栈顶的栈，这样我们就不会丢失任何信息：

|  |  |
|---|---|
| `ExceptT` | `runExceptT` |
| `WriterT` | `runWriterT` |
| `StateT` | `runStateT` |
| `Identity` | `unwrap` |

让我们为我们的应用创建一个 `Monad` 定义：

```
import Control.Monad.Except.Trans (ExceptT)

import Control.Monad.State.Trans (StateT)

import Control.Monad.Writer.Trans (WriterT)

import Data.Identity (Identity)

type AppM e w s a = ExceptT e (WriterT w (StateT s Identity)) a ①
```
