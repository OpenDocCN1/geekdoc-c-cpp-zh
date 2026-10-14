

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- control
- unfoldable
```

将 control 和 unfoldable 添加到 spago.dhall 中。

重新运行后，我们的测试打印出 (Right (Tuple "" "xyz"))，这是正确的！

但我们收到了以下警告：

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- arrays
```

现在 count 不再需要 Data.Array，我们可以安全地从 spago.dhall 中移除它。

我们还应该做一个小的改动。在 Data.Unfoldable 中，有一个名为 none 的函数，它返回一个空的 Unfoldable 集合。这意味着，如果我们使用 none 而不是 empty，就可以在去掉 Plus 约束的情况下使用。约束越少越好：

```
import Data.Unfoldable (class Unfoldable, replicate, none) ① ②

count
  :: ∀ e a f
    . Traversable f ③
    => Unfoldable f
    => Int
    -> Parser e a
    -> Parser e (f a)
count n p
  | n <= 0    = pure none ④
  | otherwise = sequence (replicate n p)
```

+   ① 在导入中添加 none。
+   ② 我们删除了 Control.Plus 导入。
+   ③ 我们移除了 Plus 约束

❹ 将 `empty` 改为 `none`。

运行这个新版本，我们得到：

```
```text
[warn] None of your project files import modules from some projects that are
in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following
packages from the list of dependencies in your config:
– control
```
```

由于我们不再使用 `Control.Plus`，请从 `spago.dhall` 中移除 `control`。

将 `count` 改为更通用确实做了很多额外的工作，但最终是值得的。我们本可以让这个函数一直返回 `Array`，而且很多时候泛化一个函数并不值得。

但在这种情况下，我们正在编写一个通用的解析库，我们不知道世界上谁可能会使用它以及在什么条件下。所以做出这个改动是值得的。此外，泛化得越多，就越容易。所以这是很好的练习。

我们现在就先这样保留这个解析器。我们在学习了 `Monads` 之后再回来处理它，使其成为一个 **Monadic Parser**，它可以解析 Applicative Parser 无法解析的东西。我们还会看到 `Alternative` 如何帮助我们编写更复杂的解析器。

# # 第 18 章。Monads

Monads 是函数式编程中最被糟糕解释的领域。这种糟糕解释的历史来自于那些刚刚学会它们并试图在在线论坛或博客文章中解释它们的人。但问题是他们还没有完全理解它们。或者他们只是部分理解。

另一个问题的解释是他们试图使用类比来使其“易于理解”。这只会进一步模糊主题，在最坏的情况下，会产生误导。

不幸的是，由于这个原因，Monads 获得了难以理解的坏名声。实际上，它们并不比 Functors 或 Applicatives 更难理解。它们只是更强大。当我们将它们结合起来时，它们的力量会成倍增加。

Monads 实际上是函数式编程的精髓，因为我们在现实世界的应用程序中与外部世界交互，而 Monads 帮助我们在纯函数式的方式下做到这一点。

# ## 18.1. 副作用

当你与外部世界交互时，你就在处理 *副作用* 的领域。例如，当你从文件读取或调用 Web API 时，该函数返回的值将不会是确定的，即对于使用相同输入的两次连续调用，结果可能不同。

这些操作与纯函数非常不同，纯函数对于相同的输入总是返回相同的结果。这就是为什么在函数式语言中禁止使用全局变量，因为它们会将副作用引入访问它们的每个纯函数。

让我们先看一个如何在 Javascript 中使用全局变量来维护对函数调用的日志记录的示例：

```
```javascript
var log = '';
const f = x => { x + 10; log += 'added 10\\n'; };
const g = y => y * 100; log += 'multiplied by 100\\n'; };
const h = z => g(f(z));
const h2 = z => g(f(z)) + g(f(z));
```
```

这里全局变量 `log` 在每次调用 `f` 或 `g` 时都会被更新，即这些函数会产生副作用。

这意味着 `f` 和 `g` 不是纯的。查看函数 `h2`，我们可以看到我们不能像在纯函数式语言中那样只评估一次 `g(f(z))` 然后将其值加倍。这些函数需要一遍又一遍地调用，以便它们的副作用能够发生。

对于纯函数，我们唯一能做的就是传入值并传出值。所以让我们用这种方法用 PureScript 编写 `f` 和 `g`：

```
```purescript
f :: Int -> Tuple String Int
f x = Tuple "added 10\n" (x + 10)

g :: Int -> Tuple String Int
g y = Tuple "multiplied by 100\n" (y + 100)
```
```

注意每个函数都返回计算结果和副作用。我们的结果不再是一个纯值。相反，它是一个上下文中的纯值。上下文包含该计算的副作用。

因此，我们还没有破坏任何定律，因为我们保持函数纯。在继续阅读之前，想想我们如何组合这两个函数来产生上面看到的 `h`。

为了了解如何组合 `f` 和 `g` 来产生 `h`，让我们先看看没有副作用的 `f` 和 `g` 的版本：

```
```purescript
f' :: Int -> Int
f' x = x + 10

g' :: Int -> Int
g' y = y + 100
```
```

有了这些纯函数，我们可以轻松地将它们组合起来得到 `h'`：

```
```purescript
h' = g' <<< f'
```
```

但对于 `f` 和 `g`，我们不能这样做，因为 `f` 返回 `Tuple String Int` 而 `g` 接受一个 `Int`：

```
```purescript
f :: Int -> Tuple String Int
f x = Tuple "added 10\n" (x + 10)

g :: Int -> Tuple String Int
g y = Tuple "multiplied by 100\n" (y + 100)
```
```

因此，我们需要编写一个更复杂的函数来组合它们。让我们一行一行地做：

```
```purescript
h :: Int -> Tuple String Int
```
```

`h` 必须返回调用 `f` 和 `g` 时得到的副作用，这些副作用将返回在 Tuple 的第一个位置。

接下来，我们添加 z 参数（参见 Javascript 版本的 h）：

```
h :: Int -> Tuple String Int
h z = ???
```

下一步调用 f 并捕获计算结果和副作用：

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
  ???
```

这里计算结果是 r，副作用是 s。

接下来，我们需要用 f 的结果 r 来调用 g。然后我们将捕获 g 的结果和副作用：

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
      Tuple s' t = g r
  ???
```

我们将 g 的计算结果捕获到 t 中，副作用捕获到 s' 中。

最后，我们必须返回最终的计算结果和整体副作用。最终的计算结果很容易。它就是 t。

但整体副作用是什么？

回顾我们的 Javascript 实现，我们可以看到当我们调用 f 时，log 首先包含字符串 "added 10\n"，然后当我们调用 g 时，"multiplied by 100\n" 会被追加到它后面。我们在这里也应该这样做，只需将 f 的副作用与 g 的副作用连接起来：

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
      Tuple s' t = g r in
  Tuple (s <> s') t
```

# 18.1.1. 组合副作用函数

现在我们有一个可工作的函数，我们应该退一步问自己，我们能让它更好吗？

这并不明显。而且这很糟糕，因为纯版本 h' 是如此简单：

```
h' = g' <<< f'
```

很明显 h' 优于 h。h 的代码痛苦地编写，并且由于其复杂性而容易出错。对于 h'，我们可以直接内联解决方案，但对于 h，我们被迫编写一个函数来组合 f 和 g。

这 hardly 理想。也许我们可以编写一些库函数来让事情变得更好。

让我们尝试通过编写一个 compose 函数来实现，该函数将让我们组合副作用函数。我们该怎么做呢？

这是一个很难一步回答的问题。相反，让我们尝试一些更易实现的目标。我们将编写一个函数，让我们组合返回作为副作用的字符串的函数，说明它们被调用了以及它们做了什么。

让我们称之为 composeDebuggable，因为它会组合任何返回调试信息的函数：

```
composeDebuggable :: ???
```

在这里编写类型签名并不明显。让我们看看常规 compose 函数的类型签名，看看我们能否获得一些启示。查看 Pursuit 我们发现：

```
class Semigroupoid a where
  compose :: ∀ b c d. a c d -> a b c -> a b d

infixr 9 compose as <<<
```

哇。这一点也不令人困惑。好吧，首先，什么是 Semigroupoid？

Semigroupoid 是一个没有恒等态射要求的范畴。

记住，范畴由对象和态射组成。每个对象都有一个恒等态射（这部分不是 Semigroupoid 的一部分）。并且态射是可组合的（这部分是 Semigroupoid 的一部分）。

我们可以将 Semigroupoids 概括为可组合的东西。如果这是真的，那么我们可以使 Function 成为 Semigroupoid 的实例，因为函数可以被组合：

