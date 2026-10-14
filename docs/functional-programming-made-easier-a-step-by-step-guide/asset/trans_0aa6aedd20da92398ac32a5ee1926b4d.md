

使用 `head` 和 `tail` 之后，我们下一步要考虑一般情况，所以让我们尝试这种方法，看看是否适用于编写 `last`。

回顾一下我们在 `last` 的提示部分中的策略，我们需要丢弃 head，直到只剩下单个元素的列表。所以让我们写下它：

```
last :: ∀ a. List a -> Maybe a
last Nil     = Nothing
last (_ : xs) = if length xs == 1 then head xs else last xs
```

+   1. 不要忘记将 `(==)` 添加到 `import Prelude` 导入列表中。
+   2. head 在模式匹配中通过简单地不命名它来丢弃，即使用 `_`。
+   3. 如果长度为 1，则我们取出 `xs` 中唯一的元素，否则我们继续递归直到耗尽除最后一个元素之外的所有元素。请注意，由于 `head` 返回一个 `Maybe`，并且我们知道 `xs` 不为空，事实上其长度为 1，我们将得到一个包含唯一元素的 `Just`，因此不需要添加它。

为了好玩，看看这段代码，看看它是否是尾递归？记住，一个递归函数如果最后做的事是递归，则为尾递归。

事实证明它确实是尾递归的，但在用 `if` 编写时很难看出。而且事实证明，对于这种情况，有一种更优雅的解决方案，它不使用 `if` 而是使用模式匹配。

你能想到怎么做吗？在继续之前，回到并尝试对单个元素的 `List` 使用模式匹配。

`length xs == 1` 的情况，即我们有一个只有一个元素的 `List`，与以下情况相同：

```
last (x : Nil) = Just x
```

+   1. `if` 部分作为模式匹配，即 `length` 等于 1。
+   2. `(x : Nil)` 做了 if-then-else 版本中 `head` 做的事情，但我们在这里没有得到一个 `Maybe`，因此必须自己添加 `Just`。

并且将此情况添加到我们的代码中后，我们就不需要 `if` 了。基本上，模式匹配为我们做了 `if`。所以我们只需要编码 `else` 情况：

```
last (_ : xs) = last xs
```

+   1. `else` 部分作为模式匹配。

并把它们全部放在一起：

```
last :: ∀ a. List a -> Maybe a
last Nil      = Nothing
last (x : Nil) = Just x ①
last (_ : xs) = last xs ②
```

① 此匹配必须在一般情况之前，否则包含 1 个元素的列表将匹配一般情况，我们将永远不会执行此逻辑。记住，使用模式匹配时，编译器会按我们定义的顺序为我们进行 if 检查。

② 这里是尾递归。

现在我们可以清楚地看到这个函数是尾递归的，因为它只在一个案例中递归，并且它所做的只是递归。

你可能没有注意到的一件事是，我们不再像第一个版本那样调用 length。这意味着我们不再多次遍历列表，使得这个版本对于大型列表来说比我们之前的版本更高效。

记住 length 会遍历列表一次。之前的版本会对列表中的每个元素都调用 length。这意味着大小为 n 的列表将遍历 n² 次，尽管每次迭代的列表越来越小。

这个改进绝对值得做，因为它效率更高，而且更易于阅读和理解。这是一个三赢的局面。

## 5.19. 编写 init

init 就像 tail 一样，只是返回的列表是开头减去最后一个元素。

你可能已经猜到了，head 与 tail 的关系就像 last 与 init 的关系。

![](img/8c0e9b687c62642e828ccb5481e11313_184_0.png)

以下是你应该添加到测试中的代码：

```
```purescript
log $ show $ init Nil ❶
log $ show $ init (1 : Nil) ❷
log $ show $ init (1 : 2 : Nil) ❸
log $ show $ init (1 : 2 : 3 : Nil) ❹
```
```

+   ❶ 打印 `Nothing`。
+   
+   ❷ 打印 `(Just Nil)`。
+   
+   ❸ 打印 `(Just (1 : Nil))`。
+   
+   ❹ 打印 `(Just (1 : 2 : Nil))`。

再次，在跳入代码之前，尝试制定一个策略。

### 5.19.1. `init` 的提示

正如我们在 `last` 中所做的那样，我们希望递归直到得到一个单例 `List`，即只有一个元素的 `List`。但与 `last` 不同，我们不想在途中丢弃元素。相反，我们希望在递归时收集元素到一个新的 `List` 中。

另外，回想一下我们之前编写的几个函数。我们总是问这个问题：“失败情况是什么”。

如果你还没有写出来，带着这些提示再试一次。

### 5.19.2. `init` 的代码

一如既往，我们从类型签名开始：

```
```purescript
init :: ∀ a. List a -> Maybe (List a)
```
```

仅通过查看它并知道 `init` 应该做什么，我们能确定什么？

首先，我们知道它会接受一个 `List`，根据我们之前对 `head`、`tail` 和 `last` 的经验，这告诉我们我们将进行迭代，即我们的函数将是递归的。这意味着我们需要一种方法来终止递归，即一个基本情况。

就像在 `last` 中一样，我们的基本情况是一个单例 `List`：

```
```purescript
init :: ∀ a. List a -> Maybe (List a)
init (x : Nil) = Just Nil ❶ ❷
```
```

+   ❶ 我们返回一个列表，其中包含除最后一个元素 `x` 之外的所有内容，即 `Nil`。
+   
+   ❷ 不要忘记 `Just`。

我们的失败情况是空列表：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing ①
init (x : Nil) = Just Nil
```

① 如果我们最初得到一个空列表，我们将无法生成一个减去其不存在的最后一个元素的列表。

最后，我们需要处理非空列表的一般情况。我们希望删除列表的 head 并递归地将其添加到 tail 的 init 中：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init (x : Nil) = Just Nil
init (x : xs) = x : init xs  -- COMPILER ERROR!! ①
```

① 为什么这是错误？

编译器抱怨：

![](img/8c0e9b687c62642e828ccb5481e11313_186_0.png)

虽然这种方法过去有效，但在这里不起作用，因为 init 不返回一个列表。相反，它返回一个 Maybe 列表。请注意，这两个类型是我们类型不匹配错误中的类型。

我们需要比之前函数采用的不同策略。

让我们把代码回滚到仅我们的失败情况：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
```

我们已经处理了空列表的情况。我们需要编写的所有其他情况都将是我们拥有非空列表的情况。

`init` 返回 `Maybe List` 的唯一原因是它最初可能被传递一个空 `List`。在编写递归情况时，我们不再有这个限制。

所以让我们编写一个本地函数，习惯上命名为 `go`，它返回一个 `List`，因为我们保证它永远不会得到一个空 `List`：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init l = go l where ❶
  ???
```

❶ 这里 `l` 是一个非空 `List`，多亏了上一行代码捕获了空 `List` 情况并返回 `Nothing`。

现在我们只需要弄清楚如何编写 `go`。再次，我们知道我们将递归，并且我们将最终将非空 `List` 减少到只剩下 1 个元素：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init l = go l where
  go (_ : Nil) = Nil ❶
  ???
```

❶ 就像我们之前做的那样，我们排除了列表的最后一个元素 `x`，这正是 `init` 的目的。这是我们递归的基本情况。

我们已经编写了基本情况，现在必须编写递归情况。

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init l = go l where      -- COMPILER ERROR!!
  go (_ : Nil) = Nil
  go (x : xs) = x : go xs ❶
```

❶ 这个情况正是我们之前用 `init` 尝试编写的情况。现在编译器不再抱怨，因为 `go` 返回一个 `List`，而不是 `init` 返回的 `Maybe List`。

但现在我们有一个不同位置的不同编译器投诉：

![](img/8c0e9b687c62642e828ccb5481e11313_188_0.png)

这里 go 返回一个列表但 init 返回一个 Maybe。我们需要添加 Maybe 的数据构造函数，即我们需要将 Just 添加到我们对 go 的调用中，将一个列表变成一个 Maybe 列表：

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init l = Just $ go l where      -- COMPILER ERROR!! ①
  go (_ : Nil) = Nil
  go (x : xs) = x : go xs
```

① 现在 init l 返回一个 Maybe 列表。注意使用 $ 而不是括号。

再次，我们有一个不同的错误：

![](img/8c0e9b687c62642e828ccb5481e11313_188_1.png)

此错误表示我们缺少 go 在列表为空，即 Nil 时的情况。

这乍一看似乎是错误的，因为我们知道 go 永远不会得到一个空列表。为什么？因为我们永远不会用空列表初始调用它，并且我们将在列表只剩下 1 个元素时终止递归。

但问题是编译器不知道这些。PureScript 中有一个非空列表类型，我们还没有学过，但那会不必要地使这个特定函数复杂化。

所以最简单的方法就是添加该情况来取悦编译器，即使我们知道它永远不会被执行。

