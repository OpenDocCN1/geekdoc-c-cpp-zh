
```purescript
g x = lastStep $ x
  # step1    -- COMPILER ERROR!!
  # step2
  # step3
```

但如果我们稍微思考一下这段代码，就会发现我们其实并不希望 `#` 垫底。我们只希望它排在最后，正好在 `$` 之前。

而我们的解决方案正在于此：

```purescript
infixl 1 applyFlipped as #
```

我们让 `#` 的优先级为 `1`，这意味着当它与其他运算符一起使用时，它将在最后求值，而 `$` 则会在垫底求值。

我们最终的解决方案是：

```purescript
applyFlipped :: ∀ a b. a -> (a -> b) -> b
applyFlipped = flip apply

infixl 1 applyFlipped as #
```

我们应将下面这一行添加到测试函数中来测试这段代码：

```purescript
flip const 1 2 # show # log
```

但随后编译器会报错：

```purescript
test :: Effect Unit
test = do
  log $ show $ flip const 1 2   -- COMPILER ERROR!!
  flip const 1 2 # show # log
```

① `do` 块是一种特殊语法，我们将在本书更高级的部分学习它。

这个错误似乎毫无来由，令人费解：

```text
Unknown value discard. You’re probably using do-notation, which the compiler replaces with calls to the discard function. Please import discard from module Prelude
PureScript(UnknownName)
Peek Problem  No quick fixes available
log $ show $ flip const 1 2
flip const 1 2 # show # log
```

有一些内部函数通常由 `Prelude` 导入，用于 `do` 语法。由于我们决定在模块中只从 `Prelude` 导入几项，因为我们正在重写一些 `Prelude` 函数，所以我们没有导入 `do` 语法函数。

根据错误消息，我们可以通过将 `discard` 添加到 `Prelude` 导入列表来修复此问题：

```purescript
import Prelude (Unit, show, discard)
```

现在我们的程序可以编译了，运行时应该会打印两次 `2`。

### 5.9. 准备编写 Data.List 函数

本章我们将编写的其余函数将来自 `Data.List`。

我们需要有选择地从 `Data.List` 导入，这样我们就不必把一切都写出来。

要包含 `List` 功能，请将以下内容添加到导入中，并保持导入列表按字母顺序排列（`Prelude` 除外，它排在第一位）：

```purescript
import Data.List (List(..), (:))
```

① `List(..)` 是一种简写，表示导入 `List` 类型及其所有数据构造器。其完整写法是 `List(Nil, Cons)`。

② `(:)` 导入 `Cons` 运算符。

你的导入现在应该如下所示：

```purescript
import Prelude (Unit, show, discard)

import Data.List (List(..), (:))
import Effect (Effect)
import Effect.Console (log)
```

① 这应该会产生一个编译器错误。

原来我们还没有 `List` 包。如果你在 `Pursuit` 中搜索 `Data.List`，你会找到包含此类型的包：

**模块 Data.List**

该模块定义了一种 *严格* 链表类型，以及相关的辅助函数和类型类实例。

*注意：* 根据你的用例，你可能更倾向于使用 `Data.Sequence`，它在某些用例下可能会提供更好的性能。在纯函数式环境中处理不可变数据列表时，该模块是对 `Data.Array` 的改进，但它不具备良好的随机访问性能。

**包：`purescript-lists`**

在底部，我们看到 `purescript-lists` 是包名。

要向构建中添加包，我们需要编辑 `spago.dhall` 文件。添加包时，我们总是去掉 `purescript-` 前缀。因此，我们需要将 `lists` 添加到 `dependencies` 中：

```dhall
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "console"
  , "effect"
  , "lists"
  , "prelude"
  , "psci-support"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 这将添加包含我们所需模块（`Data.List`）的包。

完成此操作后，重新构建你的程序：

```bash
npx spago build
```

这将安装 `purescript-lists` 包并编译它。

你会得到一堆警告。原因有两点。

首先，我们还没有使用 `Data.List`，因此出现以下警告：

```text
Warning 9 of 9:

    in module Ch5
    at src/Ch5.purs:5:1 - 5:33 (line 5, column 1 - line 5, column 33)

    The import of Data.List is redundant

    See
https://github.com/purescript/documentation/blob/master/errors/UnusedImport.md
for more information,
    or to contribute content related to this warning.
```

其余 `8` 个警告是因为 `PureScript` 库中某些内容尚未跟上。

### 5.10. List 类型

```purescript
Cons 1 (Cons 2 (Cons 3 Nil))
```

你还可以使用 `Cons` 二元运算符：

```purescript
1 : 2 : 3 : Nil
```

### 5.11. 编写 singleton

现在将下面这一行添加到测试中：

```purescript
log $ show $ singleton "xyz"
```

① 应该打印出 `("xyz" : Nil)`。

现在，在继续阅读之前，先编写 `singleton` 函数。

#### 5.11.1. singleton 的代码

这个函数非常简单：

```purescript
singleton :: ∀ a. a -> List a
singleton x = x : Nil
```

① 使用 `Cons` 运算符。

也可以使用 `Cons` 来编写：

```purescript
singleton :: ∀ a. a -> List a
singleton x = Cons x Nil
```

① 这仅仅是前缀版本，而运算符版本是中缀版本。

我更喜欢运算符版本，因为它更简洁。

### 5.12. 编写 null

如果你来自一个存在 `NULL` 的语言，我希望你意识到这里所说的不是一回事。这个函数用于检查列表是否为空。

虽然你可以用 `if` 或 `case` 来编写这个函数，但更地道的做法是使用模式匹配。所以请尝试采用这种方法。

另外，将下面几行添加到测试中来测试你的代码：

```purescript
log $ show $ null Nil
log $ show $ null ("abc" : Nil)
```

① 应该打印出 `true`。

② 应该打印出 `false`。

在继续之前，先试一试编写它。

#### 5.12.1. null 的代码

你能仅通过查看其类型签名就判断出 `null` 是什么类型的函数吗？

```purescript
null :: ∀ a. List a -> Boolean
```

任何签名形式为 `a -> Boolean` 的函数都是谓词。在这种情况下，我们谓词类型签名中的 `a` 代表 `null` 类型签名中的 `List a`。

下面是使用模式匹配编写的 `null` 代码：

```purescript
null :: ∀ a. List a -> Boolean
null Nil = true
null _ = false
```

① 空列表的情形。

② 全匹配（兜底）情形。

注意，我们没有使用 `if` 或 `case` 表达式。模式匹配要干净得多。

### 5.13. 编写 snoc

这个函数的名字是 `Cons` 反转而来。既然 `Cons` 将元素放在 `List` 的头部，那你认为 `snoc` 会做什么呢？

它将元素放在末尾。在编码之前，先想想你打算如何解决这个问题。

另外，将下面这一行添加到测试中来测试你的代码：

```purescript
log $ show $ snoc (1 : 2 : Nil) 3
```

① 应该打印出 `(1 : 2 : 3 : Nil)`。

#### 5.13.1. snoc 的提示

你是否尝试过写类似下面的代码：

```
snoc :: ∀ a. List a -> a -> List a
snoc l x = l : x   -- COMPILER ERROR!!
```

之所以行不通，是因为 `l` 是列表而 `x` 是元素。这不是 `Cons` 运算符想要的。它期望在列表头部放置一个元素，而不是尾部。

记住，列表本质上是链表。在列表头部添加元素很容易且快速。在列表尾部添加元素需要以下策略：

+   1. 解开列表直到到达末尾。这需要递归。

+   2. 在列表末尾，返回只包含一个元素的列表，即我们要添加到末尾的元素。

+   3. 在返回递归调用时，一次一个元素地将列表重新组合起来。

希望这有所帮助。尝试使用此策略再次编写该函数。

#### 5.13.2. snoc 的代码

根据我们的策略，让我们先实现递归的基例（#2）：

```
snoc :: ∀ a. List a -> a -> List a
snoc Nil x = singleton x ① ②
```

① 这是我们策略中的基例（#2）。我们已到达列表末尾（或从空列表开始），并且我们只需返回一个包含我们想要放在列表末尾的元素的单例列表。

② 我们还没有完成。这个函数是一个部分函数，编译器会抱怨因为并非所有情况都已穷尽。

> 递归函数的基例是终止递归调用的情况。如果递归函数没有基例，那么它就是无限递归的，永远不会产生输出值。

下一步是弄清楚下一个模式匹配应该是什么。查看到目前为止的函数，我们可以看到我们已经处理了空列表的情况，所以我们需要一个非空列表的模式匹配。

让我们只添加这一部分：

```
```purescript

snoc :: ∀ a. List a -> a -> List a

snoc Nil x       = singleton x

snoc (y : ys) x = ???

```
```

> ❶ 这将匹配具有模式 `(y : ys)` 的非空列表。

我们需要问自己的下一个问题是是否还有其他情况。我们有空 `List` 情况和非空 `List` 情况。由于这涵盖了所有情况，我们现在有一个总函数。

现在我们要做的就是弄清楚 `???` 应该放什么。

重新审视我们的策略 #1，它说：

> 解开 `List` 直到到达末尾。这需要递归。

解开列表本质上就是我们在非空 `List` 情况下从 `tail` 中取出头部所做的事情：

```
```purescript

snoc :: ∀ a. List a -> a -> List a

snoc Nil x       = singleton x

snoc (y : ys) x = ???

```
```

> ❶ 取出头部。

但我们仍然需要递归以继续向下遍历 `List` 直到到达 `List` 的末尾：

```
```purescript

snoc :: ∀ a. List a -> a -> List a

snoc Nil x       = singleton x

snoc (y : ys) x = snoc ys x

```
```

> ❶ 递归以便到达 `List` 的末尾。我们使用 `List` 的尾部 `ys`，它在每次对 `snoc` 的递归调用中会变得越来越小，直到为空，这将终止递归。

如果你用这段代码运行程序，你会看到假设你在 `test` 函数末尾添加测试时打印的最后一件事：

```
```text

(3 : Nil)

```
```

> ❶ 不是正确答案！！

我们遗漏了什么？

我们没有重新组装列表，即我们策略中的 #3。让我们检查这种情况以弄清楚哪里出了问题：

```
snoc (y : ys) x = snoc ys x
```

请注意，我们没有对 `y` 做任何事情。我们取出头部然后不使用它。所以我们实际上是在丢弃它。

一旦我们通过 `snoc ys x` 将 `x` 添加到 `ys`，我们应该将 `y` 放回列表的头部：

```
snoc :: ∀ a. List a -> a -> List a
snoc Nil x     = singleton x
snoc (y : ys) x = y : snoc ys x ❶
```

> ❶ 我们将 `y` 放在列表的头部。

现在当我们运行程序时，我们得到：

```
(1 : 2 : 3 : Nil)
```

这有效！

但让我们确保我们理解它是如何工作的。通常，递归部分总是令人最困难的：

```
snoc (y : ys) x = y : snoc ys x
```

我们可以按如下方式推理这行代码：

> 我们从列表中取出头部，然后将元素 `x` 添加到尾部。

> 然后我们将头部放回该新列表。

以下是完整的实现：

```
snoc :: ∀ a. List a -> a -> List a
snoc Nil x     = singleton x ❶
snoc (y : ys) x = y : snoc ys x ❷
```

接下来，让我们通过从初始调用开始并使用上面注释的两个不同方程进行简单的数学替换来看看每次调用是如何工作的：

```
snoc (1 : 2 : Nil) 3 =     -- original call
1 : snoc (2 : Nil) 3 =     -- substitute using ②
1 : (2 : snoc Nil 3) =     -- substitute using ②
1 : (2 : singleton 3) =     -- substitute using ①
1 : (2 : (3 : Nil))   =     -- singleton definition
1 : 2 : 3 : Nil            -- remove redundant Parentheses since
                           -- `:` is Right-Associative
```

请注意，每次我们进行数学替换时，都相当于对程序中 `snoc` 的一次递归调用。我们替换 3 次，我们递归 3 次。

### 5.14. 编写 length

在处理了 `snoc` 之后，下一个函数应该更容易。它是计算列表长度的 `length` 函数。

确保你在搜索 `Pursuit` 时查看的是来自 `Data.List` 的正确版本的 `length`。

将此行添加到你的 `test` 函数中以测试 `length`：

```
log $ show $ length $ 1 : 2 : 3 : Nil ①
```

① 打印 `3`。

另外，为了避免剧透解决方案，将 `(+)` 运算符添加到 `Prelude` 导入列表中：

```
import Prelude (Unit, (+), show, discard)
```

现在，尝试在继续之前编写 `length`。

#### 5.14.1. length 的提示

想象我告诉你我有一个列表，你必须确定其长度，但你不允许查看该列表。而且我还告诉你，你可以问我关于该列表的一个问题，但不能问其长度。

你可能会问什么问题？

你可能会想一分钟，然后通过问我列表尾部的长度来对我耍个花招。

为什么这是个花招？好吧，你没有问原始列表的长度，而是问了尾部的长度。

为什么这是作弊？好吧，你只需将答案加 1 就可以知道原始 `List` 有多长。

重申一下，`List` 的长度是其尾部长度加 1。

在阅读后续内容之前，使用此方法帮助你编写 `length`。

#### 5.14.2. `length` 的代码

像往常一样，我们从类型签名开始：

```
length :: ∀ a. List a -> Int
```

然后我们写出平凡的情况，即 `Recursive Function` 的 `Base Case`：

```
length :: ∀ a. List a -> Int
length Nil = 0
```

> 空列表的长度为 0。

最后，我们写出一般或 `Recursive` 情况，即非空 `List`：

```
length :: ∀ a. List a -> Int
length Nil      = 0
length (x : xs) = ???
```

但我们如何编写 `???` 部分？

如果我们知道 `xs` 的长度，那么我们只需加 1 就可以得到我们 `List` 的长度：

```
length :: ∀ a. List a -> Int
length Nil      = 0
length (_ : xs) = 1 + length xs
```
