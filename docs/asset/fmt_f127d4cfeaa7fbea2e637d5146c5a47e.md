
`else go count state`

```
① 当我们看到 Tock 时递增计数。
```

编译器报错如下：

```text

No type class instance was found for

  Data.Eq.Eq TickTock

```

继续之前先修复这个错误。

我们需要为 `TickTock` 添加一个 `Eq` 实例：

```purescript

data TickTock = Tick | Tock

derive instance eqTickTock :: Eq TickTock

```

现在，我们可以删除占位的 `test` 函数，并重写 `test` 函数来创建 `AVar`，并在继续阅读之前 `fork` 出 `Fibers`。

以下是 `test` 函数的第一部分：

```purescript

import Effect.Aff (Aff, delay, launchAff_)

test :: Effect Unit

test = launchAff_ do

  ???

```

- ① 将 `launchAff_` 添加到导入列表中。
- ② 使用 `launchAff_` 在 `Aff` 中运行。这将使使用 `Fibers` 和 `Affs` 比在 `Effect` 中工作容易得多。

接下来，我们将创建 `AVar`：

```purescript

test :: Effect Unit

test = launchAff_ do

  ttAVar <- AVar.empty

  ???

```

① 将其创建为空。这使我们在时钟开始运行之前有时间启动 `Fibers`。

接下来，我们将启动 `Clock Fiber` 和 `Bomb Fiber`：

```purescript

import Effect.Aff (Aff, delay, launchAff_, forkAff)

test :: Effect Unit

test = launchAff_ do

  ttAVar <- AVar.empty

  clockFiber <- forkAff $ clock ttAVar

  bombFiber <- forkAff $ bomb ttAVar 3

  ???

```

- ① 将 `forkAff` 添加到导入列表中。
- ② `destinationCount` 为 3 秒。

现在 `Fibers` 正在运行，我们可以启动时钟。请注意，在此步骤之前，`Clock Fiber` 在尝试获取 `AVar` 时会阻塞。`Bomb Fiber` 在尝试读取 `AVar` 时也是如此：

```purescript

test :: Effect Unit

test = launchAff_ do

  ttAVar <- AVar.empty

  -- COMPILER WARNING!!

  clockFiber <- forkAff $ clock ttAVar

  -- COMPILER WARNING!!

  bombFiber <- forkAff $ bomb ttAVar 3

  AVar.put Tick ttAVar

```

我们将忽略那个提醒我们创建了 `clockFiber` 和 `bombFiber` 但尚未使用它们的警告。暂时还没用。

现在，运行你的程序：

```text

npx spago run

```

然后我们得到 `spago` 错误：

```text

[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.

To fix this error add the following packages to the list of dependencies in your config:

- datetime

```

通过将缺失的包添加到 `spago.dhall` 并重新运行来修复此问题。

它应该产生以下输出：

```text

Tick

Tock

Tick

Tock

Tick

Tock

BOOM!!

```

唯一的问题是程序永远不会退出。按 `Ctrl-C` 终止它。我们应该如何解决这个问题？

有两种方法可以处理这个问题。我们能采取的第一种方法是让 `Bomb Fiber` 与 `Clock Fiber` 通信，告诉它自己已退出。然后 `Clock Fiber` 也会退出。另一种方法是监视 `Bomb Fiber`，当它退出时，我们就终止 `Clock Fiber`。

如果 `Clock Fiber` 需要受控关闭，例如它需要做一些清理工作，那么第一种方法很好。但我们的 `Clock Fiber` 非常简单，没有这样的需求。在没必要的情况下，没有理由去引入这种方法的全部复杂性。

因此，我们将选择第二种方法。但我们如何知道 `Fiber` 何时退出？

去 `Pursuit` 中搜索 `killFiber`，并在同一页面上查找另一个可用于得知 `Bomb Fiber` 何时退出的函数。找到后，回到这里。

我希望你能找到 `joinFiber`：

```purescript

joinFiber :: Fiber ~> Aff

```

这个类型签名并没有告诉我们太多信息。但文档说：

> 阻塞直到 fiber 完成，并产出结果。如果 fiber 抛出异常，它会在当前 fiber 中被重新抛出。

这告诉我们，我们可以调用 `joinFiber`，当它返回时，就可以安全地使用 `killFiber` 终止我们的 `Clock Fiber`。

接下来，修改 `test`，以便一旦 `Bomb Fiber` 退出就正确地终止 `Clock Fiber`。然后继续阅读。

以下是这些更改：

```purescript

import Effect.Aff (Aff, delay, launchAff_, forkAff, killFiber, joinFiber)

import Effect.Exception (error)

test :: Effect Unit

test = launchAff_ do

  ttAVar <- AVar.empty

  clockFiber <- forkAff $ clock ttAVar

  bombFiber <- forkAff $ bomb ttAVar 3

  AVar.put Tick ttAVar

  joinFiber bombFiber

  killFiber (error "Exploded") clockFiber

```

- ① 将 `killFiber` 和 `joinFiber` 添加到导入列表中。
- ② 添加此导入。
- ③ 对 `Bomb Fiber` 调用 `joinFiber`，阻塞直到 `Bomb Fiber` 退出。
- ④ **使用一个 `Error` 终止 `Clock Fiber`。** 由于 `clock` 是通过 `forkAff` 启动的，而不是 `runAff` 或其他支持 `Cancelers` 的函数，因此这个 `Error` 会被 `clock` 忽略。

现在运行你的程序，它应该会正常退出。

但相反，你会得到以下内容：

```text

[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.

To fix this error add the following packages to the list of dependencies in your config:

- exceptions

```

修复此问题并重试。程序现在应该会自行退出。

## 23.2. Effects 程序规格说明

接下来，我们将编写一个非常小的应用程序，它会产生随机数，并配有这些数字的发布者和订阅者。

但在开始之前，创建一个名为 `Ch23b.purs` 的文件：

```purescript

module Ch23b where

import Prelude

import Effect (Effect)

import Effect.Class.Console (log)

test :: Effect Unit

test = do

  log "placeholder"

```

另外，修改你的 `main`，使其调用 `Ch23b.test`：

```purescript

module Main where

import Prelude

import Effect (Effect)

import Ch23b as Ch23b

main :: Effect Unit

main = Ch23b.test

```

我们将在 `Ch23b` 中编写的应用程序，会在一个包含 `ReaderT` 和 `StateT` 的 `Monad Stack` 中，为每个发布者和订阅者分别运行独立的 `Fibers`。由于我们是在 `Fiber` 中运行，我们的 `Stack` 将以 `Aff` 为基础。

发布者会生成随机数，但在生成之前会延迟 1 秒。然后，当随机生成的数字通过某个谓词时，它们会向 `Bus` 发布一条 `String` 消息。

然后，发布者会在 `State` 中对 `count` 进行倒计时，并且仅当 `count` 为正数时才继续。

将会有 3 个发布者。

一个会检查大于 0.5 的值。另一个会检查小于 0.5 的值。最后一个会检查值是否大于 0.1。

订阅者将监听 `Bus`，并将从 `Bus` 获取的数据记录到控制台。将会有 1 个订阅者。

在此稍作停留，花点时间重新阅读这些规格。

完成之后，问问自己是否已经知道得足够多来编写这个程序。我猜你会觉得还不够，而事实正是如此。你仍然需要弄明白或回忆一些事情。

所以，我将一步一步地引导你完成整个过程。

首先，写下所有你还不知道如何实现的需求。这就是我所说的技术障碍。在继续阅读之前，花几分钟列一个清单。

我将列出一份技术障碍清单，其中包含我们在前几章中已经讨论过的一些内容。这是因为你很可能忘记了一些东西，或者可能有些生疏，或者还没有完全掌握：

- 如何创建随机数
- 如何构建 `Monad Stack`
- 如何创建 `Fiber`
- 如何在 `Fiber` 中运行 `Monad Stack`
- 如何创建 `Bus`
- 如何向 `Bus` 发布
- 如何订阅 `Bus`

希望我已经把你清单上的所有内容都列出来了。如果没有，也别担心，因为我们接下来会逐一讲解如何编写。

列出技术障碍的全部意义在于，为我们提供一份在编写眼前这个程序之前必须解决的问题清单。一旦我们攻克了这份清单，编写程序就已成定局，而且应该相当容易。

### 23.2.1. 创建随机数

我们如何创建随机数？

如果你没有读这本书，你会如何弄明白这一点？

我想到 2 种方法。首先是使用 Google。这种方法的问题在于 `PureScript` 相当冷门，我不认为 `StackOverflow` 上会有一个问题能帮我们解答。

在撰写本文时，Google 搜索并没有给出这样简单的答案。你可以试一试，看看世界是否已经改变。

下一种方法是在 `Pursuit` 中搜索 `random` 这个词。当我这么做时，我希望找到某个同名函数。在继续阅读之前，你自己搜索一下，看看是否走运。

这种方法并不总是有效，尤其是当你为这个函数猜错了名称时。幸运的是，`random` 的同义词并不多。当我们搜索 `random` 时，会发现我们要找的函数位于列表首位：

```purescript

import Effect.Random (random)

random :: Effect Number

```

你能看出这个函数的问题吗？如果看不出来，请回到前面重新阅读规格说明。

问题是 `random` 在 `Effect Monad` 中运行，但规格说明我们将有 3 个发布者，每个都运行在各自的 `Fiber` 中。

但根据上一章，我们了解到 `Fibers` 是在 `Aff` 中运行，而不是 `Effect`。那么我们该如何解决这个问题？

我们可以找一个在 `Aff` 中运行的 `random` 版本。所以，去找找看，看看你能不能找到。

结果发现，并没有这样的版本。

那么，现在该怎么办？

`Forks an Aff from an Effect context and also takes a callback to run when it completes, discarding the Fiber.`

这会返回一个新的 `Fiber`。不完全是我们想要的，因为它有点过度设计。但如果必须的话，我们也可以让它工作。

让我们回到 `makeAff`，希望它更符合我们的需求：

```
makeAff
  :: ∀ a. ((Either Error a -> Effect Unit) -> Effect Canceler)
  -> Aff a
```

让我们看看它的文档：

```
Constructs an Aff from low-level Effect effects using a callback. A Canceler
effect should be returned to cancel the pending action. The supplied callback
may be invoked only once. Subsequent invocation [sic] are ignored.
```

要消化这些内容有很多，所以让我们一次吃一口：

```
Constructs an Aff from low-level Effect effects using a callback...
```

这听起来正是我们想要的。我们有一个 `Effect Number`，我们想要一个 `Aff Number`。继续阅读：

```
...A Canceler effect should be returned to cancel the pending action...
```

好的，这个要求似乎可以做到。我们可以返回一个什么都不做的 `Canceler`。在 `Pursuit` 上搜索 `Effect.Aff` 页面中的 `Canceler`，看看是否能找到一个可以在继续阅读前使用的。

如果你找到了 `nonCanceler`，那么你就找对了。所以我们可以把它作为我们的 `Canceler` 返回。

继续阅读：

```
...The supplied callback may be invoked only once. Subsequent invocation [sic]
are ignored.
```

这告诉我们我们的 `Callback` 可能只会被调用一次。这让我觉得它可能永远不会被调用。什么时候它永远不会被调用还不是很清楚。也许他们指的是 `Fiber` 可能不会

```purescript

import Effect.Aff (Aff) ①

randomAff :: Aff Number

```

① 导入 `Aff`。

现在，使用 `makeAff` 写下剩余部分。这里是参考：

```
makeAff
  :: ∀ a. ((Either Error a -> Effect Unit) -> Effect Canceler)
  -> Aff a
```

在你完成或卡住之前不要继续阅读。

这段代码并不简单。在它变得自然之前需要一些练习。让我们一步一步来。我们知道我们会使用 `makeAff`。所以，让我们加上它：

```purescript

import Effect.Aff (Aff, makeAff) ①

randomAff :: Aff Number

randomAff = makeAff ???

```

① 将 `makeAff` 添加到导入列表中。

接下来，我们知道 `makeAff` 接受一个单一参数，它是一个函数。并且该函数接受一个单一参数，我们确定它是回调函数。所以让我们写下这么多：

```purescript

randomAff :: Aff Number

randomAff = makeAff \cb -> ??? ①

```

① `cb` 代表我们的回调函数。

我们知道我们的 `Lambda` 将返回一个 `Effect Canceler`，这意味着我们的代码将在 `Effect Monad` 中运行。所以，让我们加上 `do` 关键字：

```purescript

randomAff :: Aff Number

randomAff = makeAff \cb -> do

  ???

```

现在我们可以返回 `Canceler`：

```purescript

import Effect.Aff (Aff, makeAff, nonCanceler) ①

randomAff :: Aff Number

randomAff = makeAff \cb -> do

  pure nonCanceler

```

① 将 `nonCanceler` 添加到导入列表中。

嗯，这可以编译。但等等。`random` 是怎么被调用的？我们该如何处理我们收到的回调函数 `cb`？

让我们一步一步来攻击这些问题。首先，让我们调用 `random`：

```purescript

import Effect.Random (random) ① ②

randomAff :: Aff Number

randomAff = makeAff \cb -> do

  n <- random ③

  pure nonCanceler

```

① 不要忘记导入 `random`。

② 你需要在 `spago.dhall` 中添加 `random`。

③ 我们可以在这里调用 `random`，因为我们在这个 `do` 块中以 `Effect Monad` 编码。

由于我们需要在 `spago.dhall` 中添加 `random`，你将必须运行以下命令以使代码在编辑器中编译，即如果你使用 `VSCode`：

```
npx spago build
```

保存文件会显示我们现在忽略的警告。

现在，我们对这个随机数 `n` 该怎么办？我们仍然没有使用我们的回调 `cb`。你觉得呢？

如果你卡住了，这里是回调函数的类型签名：

```
Either Error a -> Effect Unit
```
