

```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = f unit -- WRONG!
```

这可以编译，但它并不会延迟求值。这是因为 `f unit` 会立即被求值。

要让它被延迟，我们需要像之前那样创建一个全新的 `Parser`：

```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> ???
```

现在，我们要通过向函数 `f` 传入 `unit` 来取出 `Parser`：

```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> f unit -- COMPILER ERROR!!
```

由于我们还没有完成，这里会得到一个编译器错误。所以，我们先忽略它。

因为 `f unit` 是一个 `Parser`，我们需要使用 `parse` 并传入要解析的 `String`（即 `s`）来运行它：

```haskell
instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \\s -> parse (f unit) s
```

让我们稍微后退一步，欣赏一下刚刚构建的东西。我们现在有了一个 `Parser`，它在运行时只会执行另一个 `Parser`，除此之外不做任何事。从表面上看，外层 `Parser` 似乎是多余的，也确实如此，但正是因为它会在外层 `Parser` 被执行之前延迟内层 `Parser` 的执行。

外层 `Parser` 的优点在于，它在功能上等价于内层 `Parser`，但并不与内层 `Parser` 完全相同。这意味着我们可以在任何时间、任何地方安全地用它替换任何 `Parser`，并且不会影响解析结果。

但是，使用这个 `Parser` 代理的真正好处只在于，当我们能够打破像 `some` 和 `many` 这样的相互递归定义时。

顺便说一句，如果 `Lazy` 类型类不存在，我们完全可以编写一个名为 `defer` 的 `Parser` 组合子来实现相同的目标：

```haskell
defer :: ∀ e a. (Unit -> Parser e a) -> Parser e a
defer f = Parser \s -> parse (f unit) s
```

这不如 `Lazy` 类型类那么通用，因此也不那么优雅，但效果完全一样。

现在，请将以下代码添加到你的代码中：

```haskell
import Control.Lazy (class Lazy)

instance lazyParser :: Lazy (Parser e a) where
  defer :: (Unit -> Parser e a) -> Parser e a
  defer f = Parser \s -> parse (f unit) s

some :: ∀ e a. Parser e a -> Parser e (Array a)
some p = (:) <$> p <*> many p

many :: ∀ e a. Parser e a -> Parser e (Array a)
many p = some p <|> pure []
```

现在，我们想要在 `some` 的实现中延迟对 `many` 的调用。我们将用一个延迟的 `Parser` 来替换它：

```haskell
import Control.Lazy (class Lazy, defer) ①

some :: ∀ e a. Parser e a -> Parser e (Array a)
some p = (:) <$> p <*> defer \_ -> many p ②
```

> ① 我们需要将 `defer` 添加到导入列表中。
> 
> ② `defer \_ -> many p` 是我们的替代 `Parser`，它在功能上等价于 `many p`。

请对你的代码进行此修改。

现在，编写返回 `Parser e String` 的 `some'` 和 `many'`。你可以回顾一下我们之前用 `count'` 和 `range'` 的做法。继续之前请先完成这一步。

以下是实现：

```scala
some :: V e a f. Unfoldable f => Parser e a -> Parser e (f a)
some p = (:) <$> p <*> defer \_ -> many p   // COMPILER ERROR!!
```

+   1. 将 `f` 添加到 `V`。
+   2. 为 `f` 添加 `Unfoldable` 约束。
+   3. 用 `f` 替换 `Array`。

我们之所以遇到错误，是因为还没有替换 `Array` 的 `Cons` 运算符 `(:)`。

现在让我们这样做：

```scala
some :: V e a f
     " Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (f a)
some cons p = cons <$> p <*> defer \\_ -> many p   // COMPILER ERROR!!
```

为类似 cons 的函数添加了一个额外参数。

编译器正在对以下内容提出报错：

![](img/8c0e9b687c62642e828ccb5481e11313_839_0.png)

注意，它给 `many` 的调用加了红色下划线。这是因为我们还没有修改 `many`。

现在让我们来修改它：

```haskell
many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a) ①
-> Parser e a
-> Parser e (f a)
many cons p = some cons p <|> pure [] -- COMPILER ERROR!! ②
```

① 这些与我们对 `some` 的类型签名所做的修改相同。

② 我们之所以需要 cons 参数，唯一的原因是 `some` 需要它。

现在我们需要用 `none` 替换 `[]`：

```haskell
many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
many cons p = some cons p <|> pure none ①
```

① 用 `none` 替换了 `[]`。

现在 `many` 可以编译了，但 `some` 出现了一个新错误：

```haskell
some :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
some cons p = cons <$> p <*> defer \\_ -> many p -- COMPILER ERROR!!
```

这就是那个错误：

![](img/8c0e9b687c62642e828ccb5481e11313_840_0.png)

当编译器检查我们对 `many` 调用的第一个参数时，它发现了一个 `Parser`（即 `p`），但预期的是一个 `Function`。这是因为我们给 `many` 添加了 `cons` 参数，却忘了在调用中传入它。

现在让我们修复这个问题：

```haskell
some :: ∀ e a f
     . Unfoldable f
     => (a -> f a -> f a)
     -> Parser e a
     -> Parser e (f a)
some cons p = cons <$> p <*> defer \\_ -> many cons p ①
```

> ① 将 `cons` 添加为 `many` 的第一个参数。

现在，编译器对 `many` 提出了类似的抱怨，我们也会用类似的方式修复：

```haskell
many' :: ∀ e. Parser e Char -> Parser e String
many' p = fromCharArray <$> many (:) p ①
```

> ① 将 `(:)` 运算符作为我们类似 cons 的函数。

我们不妨在编译器也对 `some'` 抱怨之前修复它：

```haskell
some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <$> some (:) p ①
```

> ① 将 `(:)` 运算符作为我们类似 cons 的函数。

到目前为止我们可以停下来了，但退一步看看我们写过的代码，会发现 `some` 永远不会返回空的 `Unfoldable`，因为它应该解析一个或多个。

我们如何修改它以体现这一限制呢？

你还记得 `NonEmpty` 吗？这是它的定义：

```haskell
data NonEmpty f a = NonEmpty a (f a)
```

我们可以在 `some` 上使用它，但不能在 `many` 上使用，因为 `many` 可能为空（它是 0 个或多个）。这意味着当 `many` 调用 `some` 时，我们必须将拿到的 `NonEmpty` 转换为可以为空的东西。

好的，我们一次处理一个问题。首先修改 `some`，让它返回 `NonEmpty`：

```haskell
import Data.NonEmpty (NonEmpty, (:|))

some :: V e a f
  :| Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (NonEmpty f a)
some cons p = (:|) <$> p <*> defer \\_ -> many cons p
```

+   1. 添加了这条导入语句。
+   2. 将 `f a` 改为 `NonEmpty f a`。
+   3. 将第一个 `cons` 替换为 `NonEmpty` 的 Cons 运算符，但保留第二个 `cons` 不变，因为 `many` 需要使用它。

现在，编译器正在对 `many` 报错：

![](img/8c0e9b687c62642e828ccb5481e11313_842_0.png)

从错误信息和红色下划线可以清楚地看出，它报错是因为我们还没有将 `some` 的返回值（即 `NonEmpty`）转换为非 `NonEmpty` 的东西，而 `many` 返回的正是非 `NonEmpty`。

我们需要一种将 `NonEmpty f a` 转换为 `f a` 的方法。在 `Pursuit` 中搜索 `NonEmpty f a -> f a` 没有什么有用的结果。在 `Pursuit` 中搜索 `NonEmpty` 会显示所有 `NonEmpty` 函数，如果你仔细浏览，会发现一个可能的候选函数 `fromNonEmpty`。

这是它的类型签名：

```haskell
fromNonEmpty :: ∀ a r. (a -> f a -> r) -> NonEmpty f a -> r
```

这个类型签名并不是我们搜索的东西，但如果把 `r` 替换成 `f a`，那就正是我们想要的。我们只需要给它一个 `cons` 函数，幸运的是，我们正好有。

让我们在 `many` 中使用 `fromNonEmpty` 来转换 `some` 的返回值：

```haskell
import Data.NonEmpty (NonEmpty, (:|), fromNonEmpty) ①

many :: ∀ e a f
  . Unfoldable f
=> (a -> f a -> f a)
-> Parser e a
-> Parser e (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none ②
```

① 将 `fromNonEmpty` 添加到导入列表。

② 我们将 `fromNonEmpty cons` 映射到 `some` 上。

现在，我们在 `some'` 上遇到了一个错误：

![](img/8c0e9b687c62642e828ccb5481e11313_843_0.png)

错误提示它拿到了 `NonEmpty Array`，而预期的是 `Array`。看起来我们也需要在这里转换返回值：

```haskell
some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <<< fromNonEmpty (:) <$> some (:) p ①
```

> ① 将 `fromNonEmpty (:)` 与 `fromCharArray` 组合，并映射到 `some` 的返回类型（即 `NonEmpty Array Char`）上。

编译器终于安静了。

以下是我们最终泛化后的代码：

