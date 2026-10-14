

## 18.18. Writer 辅助函数

当一个 Monad 拥有允许计算与副作用交互的辅助函数时，我喜欢将它们统称为该 Monad 的 API。

而 Writer 就有这样的 API：

```
tell :: ∀ w. w -> Writer w Unit
listen :: ∀ a w. Writer w a -> Writer w (Tuple a w)
pass :: ∀ a w. Writer w (Tuple a (w -> w)) -> Writer w a
```

在这些 API 函数中，`tell` 使用最频繁，因此我们将更仔细地查看该函数。我们在这里学到的内容同样适用于 `listen` 和 `pass`，以及任何其他 Monad API 函数。

`tell` 让我们可以指定要附加到我们的 "日志" 的内容，例如：

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = do
  tell ["We did nothing"]
  pure 0
```

① 这里无需丢弃提取的类型，因为它是 `Unit`，而 `Unit` 由于其 `Discard` 实例是可以丢弃的。

注意 `tell` 的纯计算的类型。它是 `Unit`。为什么我们要在纯函数式编程语言中调用一个只返回 `Unit` 的函数？这个函数的意义何在？我们不能直接使用 `unit` 而不是这个函数吗？

回想一下这个 Javascript 函数：

```
console.log("Hello, world!");
```

它也什么都不返回。那为什么还要调用它呢？

因为我们想要它的副作用，即在控制台上写入。而 `tell` 也是如此。它的副作用是向 Monoid 追加内容。为了更好地理解 `tell` 是如何实现这一点的，让我们看看它的实现：

```
tell :: ∀ w. w -> Writer w Unit
tell l = Writer (Tuple unit l)
```

好吧，这告诉我们什么都没有（双关语无意）。`tell` 是如何执行其副作用的呢？

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = bind
  (Writer (Tuple unit ["We did nothing"])) (\_ -> pure 0)
```

接下来，我们将用其定义替换 `pure`，即 `pure x = Writer (Tuple x mempty)` 并将其应用于 `0`：

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = bind
  (Writer (Tuple unit ["We did nothing"])) (\_ -> Writer (Tuple 0 mempty))
```

然后我们将用其定义替换 `bind` 并应用 2 个参数。首先，这里是 `bind` 的定义：

```
instance bindWriter :: Monoid w => Bind (Writer w) where
  bind (Writer (Tuple x l1)) f =
    f x # \(Writer (Tuple y l2)) -> Writer (Tuple y (l1 <> l2))
```

现在我们进行替换：

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = (\_ -> Writer (Tuple 0 mempty)) unit
  # \(Writer (Tuple y l2)) -> Writer (Tuple y (["We did nothing"] <> l2))
```

然后我们应用第一个函数：

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = (Writer (Tuple 0 mempty))
  # \(Writer (Tuple y l2)) -> Writer (Tuple y (["We did nothing"] <> l2))
```

然后我们使用 `#` 应用，其中 `0` 绑定到 `y`，`mempty` 绑定到 `l2`。

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = Writer (Tuple 0 (["We did nothing"] <> mempty))
```

最后，我们应用 `<>`：

```
```haskell
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = Writer (Tuple 0 ["We did nothing"])
```
```

有时，很容易忘记当你查看使用 `do` 记法的代码时 `bind` 正在发生，这既好又坏。好的一面是 `do` 记法大大减少了认知负担和代码冗余。但坏的一面是，副作用看起来像是 *超距作用*，尽管事实并非如此。

当我们用 `>>=` 编写的代码来看时，它提醒我们 `bind` 实现正在发挥其魔力，对于 `Writer` 来说，这就是向日志追加。

我们也可以认为这种行为发生在 `do` 记法编写的代码的行与行之间：

```
```haskell
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = do
  tell ["We did nothing"]
    -- 将前面的日志，即 ["We did nothing"]
    -- 追加到后面的日志，即空日志
  pure 0
```
```

这是因为在 `do` 记法中，每行之间都隐含着 `>>=`。而由于 `>>=` 是 `bind` 的实现，其行为对我们是隐藏的，看起来像是魔法。但它不是。它更像是 *并行计算*。

## 18.19. 并行计算

每个 Monad 中都存在 2 个计算。第一个是纯计算，即你在计算中编写的代码，例如：

```
```haskell
gauntlet :: Int -> Either String Int
gauntlet x = do
  o <- oddTest x
  let y = o + 1
  void $ greaterThanTest 10 y
  lessThanTest 20 y
```
```

这里，纯计算是对 `oddTest`、`greaterThanTest` 和 `lessThanTest` 的调用，以及对 `o` 加 `1`。

第二个计算是 Monad 计算，即 `bind` 实现正在做的事情。在上面的例子中，它是在检查错误：

```
instance bindMaybe :: Bind Maybe where
  bind Nothing _ = Nothing ①
  bind (Just x) f = f x
```

① 编译器正在生成用于检查模式的 if 逻辑，这有效地在此实现中检查错误。

由于 Monad 的 `bind` 实现为我们做了这项工作，我们就可以在不过多思考的情况下编码。

以下是一些常见的 Monad 及其 Monad 计算：

```
Identity  -> 无计算
Maybe     -> 错误检查
Either    -> 错误检查
Writer    -> 日志追加
Reader    -> 线程只读值
State     -> 线程状态
```

我们还没有看到 Reader 或 State，所以它们的 Monad 计算可能还不 make sense，但以后会明白。

但请看 Maybe 或 Either，注意我们所说的副作用实际上是一种并行计算，即每次使用 `bind` 时执行的 Monad 计算。视觉上，它对我们是隐藏的，埋藏在 `>>=` 的实现中，并且由于 `do` 记法而更加如此。

但它确实存在，编译器也绝不会忘记它。

另一个需要思考的重要事情是，Monad 的 API 函数有助于弥合并行计算之间的差距。这里有一张图来说明 `tell` 是如何做到这一点的：

![](img/8c0e9b687c62642e828ccb5481e11313_720_0.png)

纯计算产生类型为 `a` 的值，而 Monad 计算产生类型为 `w` 的值。它们由 Writer 以元组形式返回。

Monad API 函数 `tell` 通过允许从纯计算向 Monad 计算进行写入来架起桥梁。这是有意义的，因为 Writer 是一个用于写入日志的 Monad，而我们只能从纯计算中做到这一点。

但关于从 Monad 计算中读取呢？

## 18.20. Reader Monad

想象我们编写了一个应用程序，在运行时使用配置文件信息，通过从文件读取、调用 Web 服务器下载包含适当配置的 JSON 文件，甚至只是读取命令行参数或环境变量。

在命令式程序中，我们可能会将此信息存储在一个或多个全局变量中。然后程序中的每个函数在需要时都可以查阅它们。即使在面向对象的语言中，我们也可以通过使用单例类或静态类变量来实现全局访问，具体取决于语言。

但在函数式语言中，我们已经将全局变量 relegated 到我们很久以前丢弃 `goto` 命令的同一个垃圾堆。所以，我们唯一的办法就是将其传递给几乎每个函数。至少，我们必须将其传递给调用栈顶部的所有函数，通常我们必须将其传递得更深。

这是一项艰巨的任务，会污染它遇到的每个类型签名。但现在我们知道 Monad

可以维护自己的计算，也许我们可以利用它们来完成传递此配置信息的繁琐工作。

事实证明，某人很久以前就有这个同样的绝妙想法，并产生了一个名为 Reader 的 Monad。这里是它的定义：

```
newtype Reader r a = Reader (r -> a)
```

查看类型构造器，即左边的 Reader，我们看到它接受 2 个类型参数。`r` 是 Reader 将维护并为我们传递给每个函数的类型，而 `a` 是纯计算的结果。

将注意力转向数据构造器，即右边的 Reader，我们看到它接受 1 个参数，那就是一个类型签名为 `r -> a` 的函数。此函数接受一个 `r`，即某个只读值，并产生一个 `a`，即其纯计算。

让我们看看它将如何使用，以更好地理解 Reader：

```
type Config = ①
  { numDecimalPlaces :: Int
  , debug :: Boolean
  }

funcWithConfig :: Int -> Reader Config Int ②
funcWithConfig v = do
  { numDecimalPlaces } <- ask ③ ④
  ... ⑤

main :: Effect Unit
main = do
  value <- runReader (funcWithConfig 42) ⑥
    { numDecimalPlaces = 2
    , debug = false
    }
  ... ⑦
```

① 这是我们的配置类型。

② `funcWithConfig` 接受一个 `Int` 并返回一个 Reader。请记住，像我们的 Parser 一样，我们需要使用运行函数来运行它。

③ `ask` 是一个 Reader API 函数，它返回整个只读值。注意反向箭头。那是因为 `ask` 返回一个 `Reader r a`，而我们想要提取类型为 `a` 的值。

④ 我们正在解构提取的值以仅从 Config 中获取 `numDecimalPlaces`。这是因为 `funcWithConfig` 不需要来自 Config 记录的其他字段。

