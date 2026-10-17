
1 打印 `(Tuple (Just "WE CANNOT HAVE A 0 STATE!") { log: "Starting App...", result: Nothing, state: 0 })`。

2 打印 `(Tuple Nothing { log: "Starting App...Incremented State", result: (Just unit), state: 100 })`。

运行你的代码，确保你得到预期的输出。

这样看起来容易多了，但请注意成功情况下的日志输出，即对 `runApp` 的第二次调用。你能看到有什么问题或不足吗？

由于我们选择让我们的日志类型为 `String`，我们有一个连写日志，即我们的字符串在没有某种分隔符的情况下被连接。让我们通过为日志条目添加行结束符来修复这个问题。

有两种方法可以实现这一点。其中一种更好。

第一种方法是在每条 `tell` 代码行的末尾简单地添加 `"\n"`。或者我们可以编写一个名为 `log` 的函数来写入日志并为其收到的每个字符串添加 `"\n"`。

后一种解决方案远比要求在每行末尾放置 `"\n"` 更好。它有 2 个原因。首先，它减轻了开发者的不必要负担。

其次，我们可以做到一次然后忘记它。但如果我们要求在每次 `tell` 调用时都这样做，我们就必须每次都记住，而我们知道总会有人忘记这样做。很可能就是我们自己。

在阅读更多内容之前，先写出一个名为 `log` 的函数类型签名，该函数将解决此问题。

以下是类型签名：

```
log :: String -> ??? ①
```

① 返回类型并不明显。

如果你不知道它返回什么，那么现在就在那里放一个类型孔。然后继续编写函数的其余部分。

如果你在测试代码中遇到编译器错误，不用担心，我们很快就会修复它。

这样做，然后继续阅读。

以下是带有类型孔的签名：

```
log :: String -> _
```

现在我们将在提供的字符串上调用 `tell`：

```
log :: String -> _
log s = tell s
```

现在我们添加行结束符：

```
log :: String -> _
log s = tell $ s <> "\n" ①
```

① 不要忘记 `$` 或括号。

现在我们遇到了前面提到的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_988_0.png)

我们现在有一个名为 `log` 的本地函数，它与我们从 `Event.Console` 模块导入的 `log` 冲突。

为了解决这种歧义，我们将完全限定该模块的导入：

```
import Effect.Console as Console ①
```

① 注意包含 `log` 的导入列表已丢失，并且添加了 `as` 子句为我们调用的模块创建了一个名为 `Console` 的别名。

现在，我们必须更改测试代码中对 `Console log` 的调用：

```
test :: Effect Unit
test = do
  result1 <- runApp 0 app
  Console.log $ show result1 ①
  result2 <- runApp 99 app
  Console.log $ show result2 ①
```

① 使用完全限定的名称 `log`。

现在我们在本地 `log` 函数上遇到编译器错误：

```
log :: String -> _
log s = tell $ s <> "\n" --- COMPILER ERROR!
```

以下是编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_988_1.png)

这说我们在 `log` 代码中缺少 `MonadTell` 的约束。但我们实际上缺少的不仅仅是这个。我们甚至在类型签名中都没有 `Monad`。那就是错误消息引用 `t2` 的原因。

该类型对编译器来说是一个未知类型。

因此，我们需要在类型签名中添加一个 `Monad`，然后才能对其进行约束。但怎么做呢？

好吧，我们知道 `log` 在支持 `MonadTell` 的某个 `Monad` 中运行。这意味着 `log` 将在该 `Monad` 的上下文中返回一个值。所以，让我们在类型孔中添加这一事实：

```
log :: ∀ m. String -> m _
log s = tell $ s <> "\n" -- COMPILER ERROR!
```

① 我们知道我们返回的是某个 `Monad` 值。值的类型目前对我们来说是未知的。

我们仍然有同样的错误，但至少现在我们有一个可以约束的 `Monad`。因此，我们现在就约束它：

```
log :: ∀ m. MonadTell String m => String -> m _
log s = tell $ s <> "\n"
```

现在我们得到以下类型孔警告：

![](img/8c0e9b687c62642e828ccb5481e11313_989_0.png)

编译器推断出我们的包含值是 `Unit` 类型。因此，我们可以用 `Unit` 替换我们的类型：

```
log :: ∀ m. MonadTell String m => String -> m Unit
log s = tell $ s <> "\n"
```

事实证明，我们本可以直接查看 `tell` 的类型来确定我们的返回类型会是什么，因为 `log` 只是调用 `tell`：

```
class Monad m <= MonadTell w m | m -> w where
  tell :: w -> m Unit
```

我带你走这条路是为了练习当类型孔更有帮助时。关于这种方法的一个说明，它并不总是顺利进行，在需要约束的情况下尤其如此。

因此，最好还是付出努力弄清楚类型，而不是依赖编译器提供帮助。

对于特别复杂的类型签名，你可以使用另一种方法，完全跳过编写类型签名。一旦你的函数编译通过，你会得到一个警告，告诉你类型签名应该是什么。

现在就试试这种方法，注释掉 `log` 的类型签名，看看编译器会给出什么警告。在阅读后续内容之前先这样做。

我得到的警告是：

![](img/8c0e9b687c62642e828ccb5481e11313_990_0.png)

这里建议的类型签名是：

```
forall t237. MonadTell String t237 => String -> t237 Unit
```

虽然这个类型签名相对简单，但仍然很难弄清楚我们应该把 `t237` 称为什么。我们必须查看 `MonadTell` 来看看它的第二个参数叫什么：

```
class Monad m <= MonadTell w m | m -> w where
  tell :: w -> m Unit
```

从中我们可以看出 `t237` 是 `m`。因此，我们进行该替换：

```
∀ m. MonadTell String m => String -> m Unit
```

① 我们使用 `∀` 而不是 `forall`。

现在我们有一个在由 `Monad` 转换器构建的 `Monad` 栈中运行的应用程序。我们可以访问所有 API，我们的 `StateT` 实现似乎作为 `PureScript` 库版本 `StateT` 的替代品运行良好。

但遗憾的是，一切并不那么简单。总是存在需要考虑的细微差别。

## 21.5. 使用 StateT 与 ExceptT 的问题

让我们回顾一下我们对 `catchError` 的实现：

```haskell
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f =
    StateT $\\s -> catchError (fmx s) \\e -> runStateT (f e) s
```

请看上面的代码，并特别注意 `State`，`s`。它在 2 处被使用。

它首先被传递给 `fmx`。那个函数是 `catchError` 即将尝试求值的函数，如果且仅如果出现错误，它就会调用错误处理程序，即 `Lambda`。

现在，仔细看看 `Lambda`，特别是 `s` 被传递给 `runStateT` 的地方。注意它是我们传递给出现错误的那个代码的同一个 `s`，即 `fmx`。

但如果 `fmx` 改变了 `State` 呢？我们难道不想要这些更改吗？

我们要么始终想要这些更改，要么从不想要它们。问题在于我们只有在没有错误时才会得到这些更改。如果有错误，任何 `State` 更改都将丢失。

这可能或可能不是我们想要或期望的。而且，更糟糕的是，这种行为取决于栈的顺序。其他栈顺序会始终保留 `State` 更改。

这意味着我们无法轻易预测程序的行为，这绝对是一个糟糕的情况。

此时，你可能会想知道我们的实现是否坏了，我们只需要修复它就行了。嗯，我第一次看到这个问题时也这么想过。

这是我第一次尝试修复它：

```haskell
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  -- DOES NOT FIX THE PROBLEM!!!!!
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT \\s -> fmx s >>= \\(Tuple x s') ->
              catchError (pure $ Tuple x s') (\\e -> runStateT (f e) s')
```

① 使用 `bind`，我捕获了 `s'` 中的已更改 `State`。

我这里的想法是捕获 `fmx` 中的 `State` 更改 `s'`，然后将更新后的 `State` 传递给 `runStateT`。

我以为这会解决问题。它并不会。

失败的原因是栈排序的工作方式以及 `ExceptT` 的 `bind` 短路方式。让我解释一下。

首先要理解的是 `StateT` 的 `catchError` 版本会在什么时候被调用。要回答这个问题，请回顾我们有效的实现：

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f =
    StateT $ \s -> catchError (fmx s) \e -> runStateT (f e) s
```

注意我们在实现内部调用了 `catchError`。我们知道这不是递归调用。它实际上是在调用底层 `Monad` 的 `catchError`。这意味着 `ExceptT` 不在我们的栈之上，因为如果它在，我们的 `catchError` 将永远不会被调用，因为 `ExceptT` 已经处理了它。

要让它被调用，我们必须在栈中位于 `ExceptT` 之上。

所以，让我们看看栈的情况：

![](img/8c0e9b687c62642e828ccb5481e11313_992_0.png)

现在，当我们在 `Monadic` 代码中调用 `catchError` 时，我们会先调用 `StateT` 的 `catchError` 实现。它会委托给底层 `Monad` 的实现，在上面的栈中是 `ExceptT`。这才是真正的实现。

如果 `ExceptT` 在 `StateT` 之上，那么 `ExceptT` 的实现会被先调用。由于它是真正的实现，即它不像 `StateT` 那样委托责任，`StateT` 的实现将永远不会被调用。

让我们回到我没有成功的修复：

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  -- DOES NOT FIX THE PROBLEM!!!!
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = StateT $ \s -> fmx s >>= \(Tuple x s') ->
                 catchError (pure $ Tuple x s') (\e -> runStateT (f e) s')
```

看看 `fmx s >>>= ...`。

事情就是在这里出错的。由于 `ExceptT` 在我们的栈下方，它会调用自己的 `bind`，该 `bind` 在错误时短路。所以，在错误情况下，`Lambda` 永远不会被调用。这就是短路的全部意义。

这意味着 `s'` 将不会捕获失败计算中进行的更改。

事实证明，根本没有办法修复这个问题。我们永远无法获得足够的信息来提取底层 `Monads` 中修改后的 `State`。

所以如果我们无法修复它，我们就必须学会与之共存，这意味着我们需要了解如何正确使用 `catchError` 以及我们可能遇到的陷阱。

在我们能做到这一点之前，我们需要了解 `spy` 函数。`spy` 会接受任何值并将其内部表示显示在控制台上，无论它是否有 `Show` 实例。它用于调试目的。

以下是它的类型签名：

```
spy :: ∀ a. DebugWarning => String -> a -> a
```

首先要注意的是，`spy` 的类型签名中 `DebugWarning` 是一个标记约束，编译器会查找它并警告你正在使用 `spy` 函数。

原因是因为 `spy` 破坏了 `PureScript` 中所有函数都是纯的这一契约。它通过打印到控制台来实现这一点。这只能用于调试目的。绝不应该在生产代码中使用。

要意识到，当你使用 `spy` 并且编译器对函数调用的结果进行记忆化时，你的 `spy` 输出可能不会对使用该函数的每次调用都发生一次。

***记忆化*** 是记住计算结果以避免再次调用函数的术语。编译器通过将结果存储在内存中的某个位置来记住结果，或者在生成二进制代码的 `Haskell` 的情况下，将其保存在 `CPU` 寄存器中。

编译器可以在纯函数式编程中进行此类优化，因为它知道所有函数都是纯的，用相同的输入调用它会产生相同的输出。

`spy` 类型签名中要注意的第二件事是它的第一个参数是 `String`。`spy` 会用它作为输出的前缀，后跟冒号和空格。这有助于你知道自己打印了什么。

`spy` 将输出的值是第二个参数，`a`。

第三点要注意的是 `spy` 返回一个 `a`。所以，它就像 `identity` 但带有真实世界的副作用。不是我们用 `Monads` 做过的纯副作用。

以下是你如何使用它的示例：

```
import Debug (spy) ①
add :: Int -> Int -> Int
add x y = (spy "X" x) + (spy "Y" y)
```

① 你需要将 `debug` 包添加到你的 `spago.dhall` 文件中才能导入 `Debug`。

现在，当 `add` 被调用为：

```
add 10 99
```

那么 `x` 和 `y` 的值将被显示到控制台：

```
X: 10
Y: 99
```

当你的 `PureScript` 程序在 `Node.js` 下运行时，就像我们一直做的那样，那么值会像 `Effect.Console.log` 一样输出。

但是，当你的代码在浏览器中运行时，那么你的输出将在浏览器的控制台日志中。

在使用 `Monadic` 代码中使用 `spy` 时，你希望以以下方式使用它：

```
app :: AppM
app = do
  s <- get
  pure $ spy "Our state" s ①
  let x = spy "Our state" s ②
  pure unit
```

① 由于 `spy` 返回 `s`，即我们的 `State`，我们需要使用 `pure` 将该纯值包装在我们的 `Monad` 上下文中。记住，我们 `do` 块的每一行都必须是 `Monadic` 值。

② 我们可以将 `spy` 的结果赋给某个随机值。我们永远不会使用这个值，但由于 `PureScript` 不像 `Haskell` 那样懒惰，它仍将被求值。

这两种方式都很好用，但我倾向于使用 `let` 方法。

现在我们准备好看看一个你可能会使用 `catchError` 的示例。让我们从上面的图表中 `StateT` 在 `ExceptT` 之上的栈开始：

```
type AppM = StateT Int (ExceptT String (WriterT String Effect)) Unit
runApp
  :: Int
  -> AppM
  -> Effect (Tuple (Either String (Tuple Unit Int)) String)
runApp s = runWriterT <<< runExceptT <<< flip runStateT s
```

如果你想跟随这段代码，你可以创建一个名为 `Ch21a.purs` 的文件并复制 `Ch21.purs` 中的所有代码，确保将模块名称更改为 `Ch21a`。然后用上面的代码替换 `AppM` 和 `runApp`。

现在我们将替换我们的验证函数：

```
import Debug (spy) ①
-- COMPILER WARNING!! ②
validate :: Int -> AppM
validate n = do
  s <- get
  let x = spy "s in validate" s
  log "HEY!!!!!!!!!!!!!!!!!" -- This will NOT be lost on the error case
```
