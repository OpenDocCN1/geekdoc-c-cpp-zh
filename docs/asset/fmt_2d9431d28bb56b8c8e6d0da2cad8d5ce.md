
{ `count` } <- `get`

`unless` (`count` <= 0) `do`

  `n` <- `liftAffToFiberM` `delayRandom`

  ???

```
现在我们可以将其写入 Bus。但等等。我们没有 Bus。我们必须先从 ReaderT 提供的只读数据 Reader 中获取 Bus：
```

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit

randomGenerator pred = do

  { count } <- get

  unless (count <= 0) do

    n <- liftAffToFiberM delayRandom

    { bus } <- ask ①

    ???

```
① 我们正在解构 Config Record 以获取 Bus。

现在，我们可以写入它，但前提是 pred 返回 true：
```

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit

randomGenerator pred = do

  { count } <- get

  unless (count <= 0) do

    n <- liftAffToFiberM delayRandom

    { bus } <- ask

    when (pred n) $ Bus.write (show n) bus ①

    ???

```
① 这也在 Aff 中运行。

我们需要提升 Bus.write：
```

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit

randomGenerator pred = do

  { count } <- get

  unless (count <= 0) do

    n <- liftAffToFiberM delayRandom

    { bus } <- ask

    liftAffToFiberM $ when (pred n) $ Bus.write (show n) bus

    ???

```
现在我们可以递归。等等……我们不想无限递归。所以，最好先递减计数然后再递归：
```

```
import Control.Monad.State.Trans (StateT, runStateT, get, put) ①

randomGenerator :: (Number -> Boolean) -> FiberM Unit

randomGenerator pred = do

  { count } <- get

  unless (count <= 0) do

    n <- liftAffToFiberM delayRandom

    { bus } <- ask

    liftAffToFiberM $ when (pred n) $ Bus.write (show n) bus

    put { count: count - 1 } ②

    randomGenerator pred ③

```
① 将 put 添加到导入列表中。
② 修改 State，即递减计数。
③ 递归。它将在 count 小于或等于 0 时在 unless 行终止。

注意我们使用了 put 来修改 State。看起来我们也可以在这里使用 modify_。事实证明我们可以。因为我们的 State 只有一个元素，所以在这里使用 put 等同于 modify_。

但是，我们以后可能会修改程序并向我们的 State Record 添加另一个字段。如果那样的话，我们会后悔一开始没有使用 modify_。所以，让我们现在就更改它：
```

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit

randomGenerator pred = do

  { count } <- get

  unless (count <= 0) do

    { bus } <- ask ①

    liftAffToFiberM do ②

      n <- delayRandom ③

      when (pred n) $ Bus.write (show n) bus ③

    modify_ _ { count = count - 1 }

    randomGenerator pred

```
① 将其向上移动 1 行。
② 这个 do 块在 Aff Monad 中运行。do 块的每一行都是一个 Aff a。
③ 这些行在 liftAffToFiberM 被提取出来后更容易阅读。

下一个代码改进涉及改进的不是代码，而是代码产生的输出。

现在，我们只是在它们通过谓词时输出数字。但我们将有 3 个发布者。我们将不知道哪个发布者找到了它喜欢的随机数。

让我们添加另一个参数，我们将与消息一起打印：
```

```
randomGenerator :: String -> (Number -> Boolean) -> FiberM Unit ①

randomGenerator valueType pred = do ②

  { count } <- get

  unless (count <= 0) do

    { bus } <- ask

    liftAffToFiberM do

      n <- delayRandom

      when (pred n) $ flip Bus.write bus ③

        $ "Found a value that is "

          <> valueType <> " (" <> show n <> ")" ④

    modify_ _ { count = count - 1 }

    randomGenerator valueType pred ⑤

```
① 将 String 类型作为第一个类型添加。
② 添加了我们新的参数 valueType。
③ 翻转 Bus.write 让我们可以用更干净的代码编写它，所有文本连接都在我们行的末尾进行。
④ valueType 可能的一个例子是 "less than 0.1"。
⑤ 必须将 valueType 作为参数添加到递归调用中。

现在，我们必须将此参数添加到测试代码中 randomGenerator 的调用中：
```

```
test :: Effect Unit

test = launchAff_ do

  bus <- Bus.make

  let forkFiberM = runFiberM bus

  forkFiberM logger

  forkFiberM $ randomGenerator "greater than 0.5" (_ > 0.5) ①

  forkFiberM $ randomGenerator "less than 0.5" (_ < 0.5) ①

  forkFiberM $ randomGenerator "greater than 0.1" (_ > 0.1) ①

```
① 添加 valueType 参数以改进日志输出。

现在，经过所有这些之后，我们应该能够运行它。由于是随机数，很难知道会有什么样的预期，所以让我们通过将 randomAff 更改为 delayRandom 中的常量来测试它：
```

```
constant :: Aff Number ①

constant = pure 42.0

delayRandom :: Aff Number

delayRandom = delay (Milliseconds 1000.0) *> constant ②

-- delayRandom = delay (Milliseconds 1000.0) *> randomAff ③

```
① 将始终大于 0.1 和 0.5，但永远不会小于 0.5。
② 调用 constant 而不是 randomAff。
③ 现在注释掉真实代码。

使用以下命令运行：
```

```
npx spago run
```

当你这样做时，我们得到：
```

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.

To fix this error add the following packages to the list of dependencies in your config:

- tailrec
```

修复它，现在当我们运行它时，我们应该得到以下 2 行重复 10 次，即总共 20 行：

### 23.4. 使用 AVars 和 Busses 的 JavaScript 运行时

```text

Logger: Found a value that is greater than 0.5 (42.0)

Logger: Found a value that is greater than 0.1 (42.0)

```

如果你和我一样懒得数数，可以把程序的输出复制粘贴到一个新文件中，让编辑器帮你统计行数。

因为我们的数字是 42.0，所以这只测试了 3 个 Publisher 的谓词函数中的 2 个。我们把数字改成 0.0，这样就可以测试那个用于检测值是否小于 0.1 的 Publisher：
```

```
constant :: Aff Number

constant = pure 0.0

```
现在，运行时，我们应该得到下面这样的输出 10 次：
```

```
Logger: Found a value that is less than 0.5 (0.0)
```

继续，删除或注释掉 `constant`，并把 `delayRandom` 恢复为原始代码：
```

```
delayRandom :: Aff Number

delayRandom = delay (Milliseconds 1000.0) *> randomAff
```

现在，运行时，你应该会得到类似下面的输出：
```

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

```
data Bus (r :: Row Type) a = Bus (AVar a) (AVar (List (AVar a)))
```

我们在 `Pursuit` 文档中看不到数据构造器，因为它没有从这个模块中导出。相反，我们使用的是智能构造器 `make`。

但从这个内部实现细节可以看出，`Busses` 在很大程度上依赖于 `AVars`。我们的程序之所以退出，真正原因正是 `AVars` 的工作方式。

看看下面这个程序：
```

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
```
