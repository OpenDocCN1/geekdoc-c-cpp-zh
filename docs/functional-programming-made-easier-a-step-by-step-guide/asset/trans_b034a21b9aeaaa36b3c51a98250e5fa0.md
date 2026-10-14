

### 23.4. 使用 AVars 和 Busses 的 JavaScript 运行时

```text
Logger: Found a value that is greater than 0.5 (42.0)
Logger: Found a value that is greater than 0.1 (42.0)
```

如果你和我一样懒得数数，可以把程序的输出复制粘贴到一个新文件中，让编辑器帮你统计行数。

因为我们的数字是 42.0，所以这只测试了 3 个 Publisher 的谓词函数中的 2 个。我们把数字改成 0.0，这样就可以测试那个用于检测值是否小于 0.1 的 Publisher：

```
constant :: Aff Number
constant = pure 0.0
```

现在，运行时，我们应该得到下面这样的输出 10 次：

```
Logger: Found a value that is less than 0.5 (0.0)
```

继续，删除或注释掉 `constant`，并把 `delayRandom` 恢复为原始代码：

```
delayRandom :: Aff Number
delayRandom = delay (Milliseconds 1000.0) *> randomAff
```

现在，运行时，你应该会得到类似下面的输出：

```
Logger: Found a value that is greater than 0.5 (0.938567838460007)
Logger: Found a value that is greater than 0.1 (0.3812324304953467)
Logger: Found a value that is greater than 0.1 (0.5058969659785102)
Logger: Found a value that is less than 0.5 (0.17046551999308068)
Logger: Found a value that is greater than 0.1 (0.42600641653043736)
Logger: Found a value that is greater than 0.5 (0.5824010610612658)
Logger: Found a value that is less than 0.5 (0.4375844856369162)
Logger: Found a value that is greater than 0.1 (0.5148930040569029)
Logger: Found a value that is less than 0.5 (0.3261672886687357)
Logger: Found a value that is greater than 0.1 (0.3168855112054627)
Logger: Found a value that is greater than 0.1 (0.7445062999508418)
Logger: Found a value that is greater than 0.1 (0.15464478518018088)
```

由于我们使用的是随机数，你的输出显然会有所不同。如果我们使用的随机数生成器可以用某个值作为种子（Seed），那么就可以让程序可预测地运行。

有一个名为 `purescript-quickcheck` 的包，它带有伪随机生成器。它的 API 一点都不直观。在本书后面，我们会用它来为密码哈希生成盐值（Salt）。不过，这个库也可以用来让程序产生可预测的输出，只要为它提供相同的种子即可。

顺便提一下，Pursuit 上有一个名为 `purescript-pseudo-random` 的包。它提供了好得多的随机值生成 API，但它并未包含在 spago 的包集合中。这些包集合是经过精选的库，会随着编译器和其他生态系统的变化而保持更新。

回顾一下我们刚写的程序，可以看到它确实会终止。但它是在何时终止的？又为何终止？我们的 `logger` 函数通过 `forever` 永远运行，难道它不应该一直运行下去吗？

为了回答这个问题，让我们看看已经启动的 Fiber。首先来看我们的 Publishers：

```
randomGenerator :: String -> (Number -> Boolean) -> FiberM Unit
randomGenerator valueType pred = do
  { count } <- get
  unless (count <= 0) do
    { bus } <- ask
    liftAffToFiberM do
      n <- delayRandom
      when (pred n) $ flip Bus.write bus
        $ "Found a value that is "
          <> valueType <> " (" <> show n <> ")"
    modify_ _ { count = count - 1 }
    randomGenerator valueType pred
```

注意我们是怎样有条件地进行递归的。一旦 `count` 达到 0，我们就会直接从这个函数返回，从而退出该 Fiber。

现在，让我们看看 Subscriber：

```
logger :: FiberM Unit
logger = forever do
  { bus } <- ask
  liftAffToFiberM do
    s <- Bus.read bus
    log $ "Logger: " <> s
```

这个 Fiber 永远不会退出。那么，既然这个 Fiber 永远不会退出，为什么我们的程序还是会退出呢？

事实证明，原因在于对 `Bus.read` 的调用。让我来解释。

在底层，`Bus` 使用 `AVar`。以下是 `Bus` 的完整定义：

```
data Bus (r :: Row Type) a = Bus (AVar a) (AVar (List (AVar a)))
```

我们在 `Pursuit` 文档中看不到数据构造器，因为它没有从这个模块中导出。相反，我们使用的是智能构造器 `make`。

但从这个内部实现细节可以看出，`Busses` 在很大程度上依赖于 `AVars`。我们的程序之所以退出，真正原因正是 `AVars` 的工作方式。

看看下面这个程序：

```
main :: Effect Unit
main = launchAff_ do
  avar <- AVar.empty
  log "before"
  x <- AVar.take avar
  log "after"
```

你觉得这个程序会输出什么？

如果你得知它永远不会输出 `after`，并且程序会直接退出，你会感到惊讶吗？我确实很惊讶。

在与其中一位库开发者交谈时，他向我解释说，`take` 调用的回调被保存在库内部的一个队列中。

它不是 JavaScript 回调，因此当库将控制权交还给 JavaScript 主事件循环时，不会有任何待处理的东西。

当 Node 中没有未完成的 JavaScript 回调，并且主线程已经交出控制权时，Node 就会退出程序。

这在浏览器中运行时是个问题吗？大概不是，因为你的代码除非崩溃，否则不会真正退出。

但是，我们的 Publisher/Subscriber 程序运行在 Node 中。在这种情况下，事件循环没有更多可处理的内容，也没有待处理的 JavaScript 回调，所以 Node 直接就退出了。

由于 `Busses` 使用 `AVars`，而 `AVars` 表现出这种行为，因此 `Busses` 也会表现出同样的行为。这就是为什么 `logger` 不足以让程序保持存活；一旦 Publishers 退出，我们的程序也随之退出。

你可能想知道，为什么 Publishers 不会遇到和 Subscriber 一样的问题。为了弄清原因，让我们回顾一下 Publisher 的代码：

```
delayRandom :: Aff Number
delayRandom = delay (Milliseconds 1000.0) *> randomAff

randomGenerator :: String -> (Number -> Boolean) -> FiberM Unit
randomGenerator valueType pred = do
  { count } <- get
  unless (count <= 0) do
    { bus } <- ask
    liftAffToFiberM do
      n <- delayRandom ①
      when (pred n) $ flip Bus.write bus
        $ "Found a value that is "
          <> valueType <> " (" <> show n <> ")"
    modify_ _ { count = count - 1 }
    randomGenerator valueType pred
```

① 这会通过 JavaScript 调度一个回调，这意味着在本次调用返回之前，我们的代码不会退出。

注意对 `delayRandom` 的调用。在 `delayRandom` 中，我们调用了 `delay`，而 `delay` 最终会调用 JavaScript 的 `setTimeout`。这会让我们有一个 JavaScript 知道的未完成回调，从而让程序保持存活。

一旦我们从 `delayRandom` 返回，就会递归，要么退出，要么再次调用 `delayRandom`，从而继续让程序存活。

在 `logger` 的情况下，存在一个只有 `AVar` 库才知道的待处理回调。JavaScript 对此毫不知情。所以，当所有 Publishers 都退出时，JavaScript 运行时发现没有未完成的请求，便立即退出了。

对于这类古怪的问题，我并不太喜欢在后端使用 PureScript。如果有机会，我几乎总会选择用 Haskell 编写后端。但如果你打算用 PureScript 编写并在 Node 下运行，就需要把这类问题牢记在心。

## 第 24 章 JSON 与 Ajax

在许多与后端服务器通信的浏览器应用中，JSON 被用作调用 API 的格式。这通常通过 HTTP POST 完成，而这也是我们在接下来的章节中开发应用时要采用的方式。

PureScript 中有一个用于 HTTP 请求的权威库，名为 `purescript-affjax`。JSON 编码和解码有两大主要方式。

第一种方式是使用 PureScript 的泛型表示（Generic Representation），将 PureScript 类型直接映射到 JavaScript 类型。这是使用起来最简单的库，内置于 `Foreign.Generic` 模块中。它的简单性既是优点也是缺点，例如，你无法对 `Either` 或 `Tuple` 进行编码。

另一种方式是使用一个灵活得多的库，名为 *Argonaut*，它可以在 `purescript-argonaut` 包中找到。由于我们已经编写了自己的 `Parser`，JSON 解码对我们来说会非常熟悉。我们可以使用 Applicative 和 Monadic 代码来编写解码器，这与我们编写 Applicative 和 Monadic 解析器的方式非常相似。

### 24.1. 泛型 JSON 的编码与解码

泛型 JSON 编码和解码意味着我们不必编写代码来显式地编码和解码类型。虽然这听起来好得令人难以置信，但它实际上在许多情况下都是可行的。不过，它确实有自己的局限性。

你只能对以下类型进行编码：

```
Void ①
Unit
Foreign ②
String
Char
Boolean
Number
Identity a
Array a
Maybe a
Object v
Record r
```

① 实际上永远无法被创建。

② `Foreign` 表示一个 JSON 数据块，也就是某些我们不想显式编码或解码的 JSON 数据。

注意 `Either` 并不在其中。因此，如果你的类型中包含 `Either`，就无法使用泛型 JSON 编码或解码。这时就该 `Argonaut` 登场了。

