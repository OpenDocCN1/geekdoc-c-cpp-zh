
技艺。

让我们看一个命名函数：

```haskell
add :: Int -> Int -> Int
add x y = x + y
```

类型签名是右结合的，这意味着该函数是柯里化的。

所有类型签名都隐含有右结合的括号，即向右结合：

```haskell
add :: Int -> (Int -> Int)
add x y = x + y
```

当隐式括号被显式定义后，我们可以看到这个函数如何只接受 1 个参数，并返回一个同样只接受一个参数的函数——一个 Int 并返回一个 Int。

这是另一个包含更多参数以及显式右结合括号的函数：

```haskell
add3 :: Int -> (Int -> (Int -> Int))
add3 x y z = x + y + z
```

有了显式括号，我们可以看到函数只接受单个参数，并返回一个只接受 1 个参数的函数，直到最终值被返回，在上面的例子中最终值是一个 Int。

另一个带有显式括号的例子：

```haskell
show3 :: Int -> (Int -> (Int -> String))
show3 x y z = show x <> "," <> show y <> "," <> show z
```

show 将我们的 Int 转换为 String。

`<>` 用于拼接我们的 String。

当括号没有右对齐时，含义会改变：

```haskell
f :: Int -> (Int -> String) -> String
```

- 第一个参数是 `Int`。
- 第二个参数是 `Int -> String`。
- 结果是 `String`。

这意味着第二个参数是一个函数，使得 `f` 成为高阶函数。

那么像这样的函数呢：

```haskell
g :: ((Int -> Int) -> Int) -> Int
```

- 第一个参数是 `((Int -> Int) -> Int)`，它接受一个从 `Int -> Int` 的函数并返回一个 `Int`。
- 结果是 `Int`。

下面这些函数的隐式括号是什么：

```haskell
h :: Int -> String -> String -> String
```

记住它们是右结合的，即使用括号向右结合。

所以从右侧开始，添加第一组括号：

```haskell
h :: Int -> String -> (String -> String)
```

然后再次添加：

```haskell
h :: Int -> (String -> (String -> String))
```

一旦我们得到一个只接受 1 个参数的函数就可以停止。在这种情况下，`h` 接受一个 `Int` 并返回一个类型为 `String -> (String -> String)` 的函数，所以我们可以停止。

这些隐式括号之所以存在，是因为函数只能接受单个参数。需要注意的重要一点是，变量会在此过程中被绑定。例如，回到 `add3`：

```haskell
add3 :: Int -> Int -> Int -> Int
add3 x y z = x + y + z
```

当我们用一个参数调用 `add3` 时：

```haskell
add3 1 :: Int -> Int -> Int
```

`x` 被绑定到 `1`。当我们用单个参数调用该结果函数时：

```haskell
(add3 1) 2 :: Int -> Int
```

`y` 被绑定到 `2`。用单个参数调用该结果函数：

```haskell
((add3 1) 2) 3 :: Int
```

`z` 被绑定到 `3`。该函数现在已*完全应用*，并返回值 `6`，其类型为 `Int`。

### 2.5.1. 部分应用

回到我们的 `zeroPad` 函数：

```haskell
zeroPad :: Int -> String -> String
zeroPad = padLeft '0' ① ②

padLeft :: Char -> Int -> String -> String
padLeft padCh size s = ... ③
```

① `padLeft` 只被赋予了它产生最终结果所需的众多参数中的 1 个。

② 我们已经部分应用了 `padLeft`。

③ 我们目前不关心 `padLeft` 的实现。

> *部分应用*是指函数以少于其所有参数的数量被调用。

当我们认为函数有多个参数时，部分应用就说得通了。然而，当我们考虑柯里化函数时，由于只有一个参数，就不存在所谓部分应用。

部分应用的力量可能不会立即显现，但考虑一个简单的例子：

```haskell
pad :: Boolean -> Char -> Int -> String -> String
pad rightSide padCh size s = ... ①

padLeft :: Char -> Int -> String -> String
padLeft = pad false ②

padRight :: Char -> Int -> String -> String
padRight = pad true ②

zeroPad :: Int -> String -> String
zeroPad = padLeft '0' ③

spacePad :: Int -> String -> String
spacePad = padRight ' ' ④

dotPad :: Int -> String -> String
dotPad = padRight '.' ④
```

① 我们目前不关心 `pad` 的实现。

② 对 `pad` 的部分应用。

③ 对 `padLeft` 的部分应用。

④ 对 `padRight` 的部分应用。

我喜欢把部分应用看作是对一个更通用函数的配置。我们有点像在“烘焙”配置值。

请注意，部分应用之所以可行，仅仅是因为那些“配置参数”被放在前面。`pad` 的 Boolean 参数让我们能够定义 `padLeft` 和 `padRight`，然后它们的 Char 参数让我们能够定义 `zeroPad`、`spacePad` 和 `dotPad`。

这里顺序很重要。想象一下 Char 在 Boolean 之前：

```haskell
pad :: Char -> Boolean -> Int -> String -> String
pad padCh rightSide size s = ...

padZero :: Boolean -> Int -> String -> String
padZero = pad '0'

padSpace :: Boolean -> Int -> String -> String
padSpace = pad ' '

zeroPad :: Int -> String -> String
zeroPad = padZero false

spacePad :: Int -> String -> String
spacePad = padSpace true

padDot :: Boolean -> Int -> String -> String
padDot = pad '.'

dotPad :: Int -> String -> String
dotPad = padDot true
```

1. 我们必须编写这 3 个函数来首先烘焙填充字符。
2. 接下来，我们编写这 3 个函数来指定在哪一侧填充。
3. 为了实现 `dotPad`，我们必须编写一个额外的函数 `padDot`，因为填充字符是 `pad` 的第一个参数。

这种方法迫使我们为每个新的填充字符编写一个新函数。我们原来的方法更好，因为它让我们能够在添加填充字符之前就创建 `padLeft` 和 `padRight`。现在，每当我们要添加一个新的填充字符函数时，我们都可以利用这些函数。

正因如此，花些时间规划参数顺序是值得的。

> 参数顺序的一般规则是：变化*最少*的参数放在*最左边*，变化*最多*的参数放在*最右边*。

重新审视我们的填充函数的更好版本：

```haskell
pad :: Boolean -> Char -> Int -> String -> String
pad rightSide padCh size s = ...

padLeft :: Char -> Int -> String -> String
padLeft = pad false

padRight :: Char -> Int -> String -> String
padRight = pad true

zeroPad :: Int -> String -> String
zeroPad = padLeft '0'

spacePad :: Int -> String -> String
spacePad = padRight ' '

dotPad :: Int -> String -> String
dotPad = padRight '.'
```

如果你看 `pad`，会注意到 `size` 参数在 `s`（我们想要填充的 String）之前。这是因为我们可能想要编写以下函数：

```haskell
dotPad20 :: String -> String
dotPad20 = dotPad 20
```

现在，我们可以向 `dotPad20` 传递大量的 `String`。我们想要填充的 `String` 是变化最大的部分，因此应该位于参数列表的最后。

所有其他参数都可以视为配置参数，用来告诉 `pad` 如何填充，而 `s` 是要填充什么，由于它变化最大，它是最右边的参数。

有时你会有两个总是变化的参数，在这种情况下，只需确保它们位于最后。它们各自的顺序无关紧要。

## 第 3 章 PureScript 基础

Kernighan 和 Ritchie 的《C 程序设计语言》开创了一个传统：学习新语言时，从打印 `Hello, World!` 的程序开始。

所以这就是：

```haskell
module Main where ①

import Prelude ②

import Effect (Effect) ③
import Effect.Console (log)

main :: Effect Unit ④
main = log "Hello, world!" ⑤
```

① 每个 `module` 都以它的定义开始。这里我们称它为 `Main`，它应该放在文件 `Main.purs` 中。

② 你使用 `import` 导入库。这里我们导入名为 `Prelude` 的标准基础库。

③ 我们还导入了一些额外的库来处理副作用，例如打印到控制台。我们将在本书的后面详细重新讨论副作用。

④ 这表示 `main` 是一个副作用函数，其计算结果是 `Unit`，这与其它语言（如 C、C++ 和 Java）中的 `void` 在函数式意义上是等价的。

⑤ 这会将我们的世界问候语记录到控制台。

像这样的 I/O 在函数式编程中是一个高级主题，因为它是一种副作用，这里有很多你现在还无法完全理解的内容。

但这不应阻止我们使用 `log` 函数来快速而粗略地测试我们为练习而编写的函数。我保证一旦我们学完 Monad，这段代码会更有意义。

从 Monad 开始就像在幼儿园之前先上高中，所以你只能暂时相信我表面的解释。

我们不会深入探讨 `Hello, world!`，而是从学习类型开始，这是 PureScript 和 Haskell 中最重要的部分之一，因为它们都是静态类型语言。

我们将在本书的高级部分回到 `Hello, world!` 的微妙之处。

### 3.1. 类型

PureScript 的大部分代码都是开源的，可以通过 GitHub 仓库轻松查阅，但

