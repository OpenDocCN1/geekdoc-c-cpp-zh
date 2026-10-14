

![](img/8c0e9b687c62642e828ccb5481e11313_209_0.png)

根据错误信息，缺少的 case 是 (Cons Nil _)。所以让我们添加它：

```
concat :: ∀ a. List (List a) -> List a
concat Nil = Nil
concat (Nil : xss) = ??? ①
concat ((x : xs) : xss) = x : concat (xs : xss)
```

① 这是我们耗尽了头部 List 的情况。这也是我们在 List of Lists 中遇到空 List 的情况，就像我们在测试代码中的最后一个 List。

一旦我们耗尽了头部 List 并处理了它的所有元素，它将变为空，我们就可以直接丢弃它并继续处理其余的 Lists：

```
concat :: ∀ a. List (List a) -> List a
concat Nil = Nil
concat (Nil : xss) = concat xss ①
concat ((x : xs) : xss) = x : concat (xs : xss)
```

① 我们继续对 List of Lists 的剩余部分进行 concat。

## 5.28. 编写 filter

我第一次学习 Functional Javascript 时，学习了 3 个函数，map、reduce 和 filter。filter 是那些函数之一，如果不能将函数作为参数传递给另一个函数，就无法实现。

像 Java 这样的非函数式语言很长一段时间都无法做到这一点，所以这个函数对我来说似乎很神奇，因为我从来没有能够写出像 filter 这样的函数。我总是必须写一个 for-loop。

但在函数式语言中情况并非如此，因为我们有高阶函数，即接受或返回函数的函数。

filter 接受一个谓词函数，在谓词返回 true 时保留或过滤入元素。看一下

花点时间重读上一句话。我们是过滤入而不是过滤出。这与我们在英语中说 filter 时的意思相反。通常，我们在思考我们不想要的东西。

记得在 `Pursuit` 上查找类型签名，并确保你查看的是来自 `Data.List` 的定义。直接阅读后面的内容以获取类型签名可能更容易，但练习在 `Pursuit` 上查找东西是有益的，因为当你不使用本书中的问题时，这就是你会做的事情。

添加以下测试代码：

```
log $ show $ filter (4 >_) $ (1 : 2 : 3 : 4 : 5 : 6 : Nil) ❶
```

> ❶ 打印 `(1 : 2 : 3 : Nil)`

你需要从 Prelude 导入 `(>)`。

这个函数很简单。在阅读后续内容之前先试试。

### 5.28.1. `filter` 的代码

这个函数足够简单，我们可以直接进入代码。首先是签名：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
```

由于这是一个迭代函数，即递归，我们将有一个基本情况：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil ❶
```

> ❶ 不能从空 `List` 中过滤出任何东西。

最后是递归情况：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil
filter pred (x : xs) = if pred x then x : filter pred xs else filter pred xs
❶
```

> ❶ 如果 `x` 通过了 `pred` 的测试，那么我们保留它并继续过滤 `xs`。否则我们就继续过滤 `xs`，即 `List` 的其余部分。

### 5.28.2. `filter` 的替代编码

这里是使用 Guards 编写 `filter` 的另一种方法：

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil
filter pred (x : xs)
  | pred x     = x : filter pred xs
  | otherwise  = filter pred xs
```
```

你可能会发现这个版本更容易阅读。我觉得它有点冗长。我发现当一个单一的 `if expression` 就足够时使用 Guards，不值得这种冗长。但是，一旦我需要开始嵌套 if 时，我就会求助于 Guards。

这基本上是个人偏好。你可能喜欢 `if expression` 但不喜欢它全部在一行上：

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil
filter pred (x : xs) =
  if pred x then x : filter pred xs
  else filter pred xs
```
```

或者你可能不介意用更多行来表达这一点：

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil
filter pred (x : xs) =
  if pred x then
    x : filter pred xs
  else
    filter pred xs
```
```

对我来说，这个最后一个版本是最糟糕的，因为它占用了屏幕上宝贵的垂直空间。

代码格式不仅仅是个人偏好。它也是你习惯看的东西。如果你来自 Elm，你可能会发现最后一个版本最好，因为你习惯于查看 Elm 代码。

我建议你尝试习惯查看更简洁的代码，这将有助于你在查看 PureScript 和 Haskell 编写的代码时。

## 5.29. `filter` 的尾递归版本

你可能已经注意到，我们的 `filter` 版本不是尾递归的：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter _ Nil = Nil
filter pred (x : xs) =
  if pred x then x : filter pred xs else filter pred xs
```

> ¹ `x : filter pred xs` 必须从 `filter` 返回以完成 `Cons` 操作，使其成为非尾递归。

让我们使其尾递归。通常，你通过在递归之前执行操作，在本例中为 `Cons` 来做到这一点。这将需要一个额外的参数来跟踪我们递归时过滤的 `List`。这就是我们的局部 `go` 函数的作用：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred l = go Nil l where
  ???
```

> ¹ `Nil` 是我们新 `List` 的初始值。我们将把通过谓词的元素添加到这个 `List` 中。
> 
> ² 等号两边最右边的参数是 `l`。我们可以对它进行 ETA-Reduce（在右边取消）。

无点版本：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred = go Nil where
  ???
```

> ¹ 我们移除了 `l`。

现在我们需要 `go` 的基本情况：

```
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred = go Nil where
  go nl Nil = nl
```

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred = go Nil where
  go nl Nil       = nl
  go nl (x : xs)  = if pred x then go (x : nl) xs else go nl xs
```
```

❶ 请记住，我们不需要将 `pred` 传递给 `go`，因为它在 `go` 的作用域中。

❷ 如果 `x` 通过了 `pred` 的要求，那么我们首先将其添加到我们的新 `List` `nl` 中，然后用 `List` 的剩余部分 `xs` 进行递归。否则，我们就继续使用 `xs`。现在我们先进行 `Cons`，我们的函数是尾递归的。

但现在我们有一个大问题。我们正在以**相反的顺序**将元素添加到我们的新列表中。第一个元素被放到列表的头部，然后下一个元素被放到头部，依此类推。这将导致我们的结果与原始顺序相比被反转。

我们如何修复这个问题？

由于我们只能添加到 `List` 的头部**并且**我们希望这个版本是尾递归的，我们只有一个选择，那就是在最后反转列表。

我们可以用我们编写的 `reverse` 函数来做到这一点，但在这样做之前，我们应该确保 `reverse` 是尾递归的，否则如果 `reverse` 会溢出我们的栈，编写 `filter` 尾递归就没有意义了：

```
```purescript
reverse :: List ~> List
reverse Nil = Nil
reverse ol = go Nil ol where
  go rl Nil       = rl
  go rl (x : xs)  = go (x : rl) xs
```
```

❶ 它通过调用 `go` 进行递归，而没有其他操作。所以这是尾递归的。

现在我们可以看到 `reverse` 是尾递归的，我们可以将其添加到 `filter` 中：

```
```purescript
filter :: ∀ a. (a -> Boolean) -> List a -> List a
filter pred l = reverse $ go Nil l where
  go nl Nil       = nl
  go nl (x : xs)  = if pred x then go (x : nl) xs else go nl xs
```
```

❶ 我们现在正在反转 `go` 的结果。

❷ 注意我不得不把我删除的 `l` 参数放回来，当我使其无点时。

要再次使这个版本无点，我们需要使用函数组合 `<<<` 而不是函数应用 `$`。

```
filter :: (a -> Boolean) -> List a -> List a
filter pred = reverse <<< go Nil where
  go nl Nil     = nl
  go nl (x : xs) = if pred x then go (x : nl) xs else go nl xs
```

> `[]` 参数又消失了。`go Nil` 等待 1 个参数，即我们删除的 `[]`。然后 `go` 的结果被传递给 `reverse`，它也等待 1 个参数。记住，组合只适用于等待单个参数的函数。

## 5.30. 时间与空间

在我们的尾递归 `filter` 版本中，我们被迫处理列表两次。一旦在过滤期间，再次在反转期间。这比非尾递归版本花费更多时间。但它占用更少的空间。

在编程中，我们总是需要在时间和空间之间进行权衡。非尾递归函数在时间上更高效，而尾递归版本在空间上更高效。

理解差异至关重要，这样你才能在编写自己的函数时做出正确的选择。

## 5.31. 编写 `catMaybes`

`catMaybes` 接受一个 `Maybe a` 的 `List`，过滤掉 `Nothing` 并解包 `Just a`，给你一个 `a` 的 `List`。

如果你有一个可能失败的项目的 `List`，并且只想要成功的结果，这非常有用。

添加以下测试代码：

```
log $ show $
  catMaybes (Just 1 : Nothing : Just 2 : Nothing : Nothing : Just 5 : Nil)
```

> 打印 `(1 : 2 : 5 : Nil)`

在参考下一节之前先尝试编写它。

### 5.31.1. `catMaybes` 的提示

你需要使用 `case` 表达式。除此之外，这是一个相当直接的函数。

### 5.31.2. `catMaybes` 的代码

一如既往，从类型签名开始：

