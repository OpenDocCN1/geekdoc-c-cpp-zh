

我给你一个提示，我们把 `Int` 替换成了 `Semiring`，使其适用于 ANY 元素。现在呢？你还能看到其他硬编码的类型吗？

没错。集合，即 `List`，也可以被抽象化。我们可以在集合上添加什么约束来使其更通用？

本章是关于 `Foldable` 的，我们一直将代码限制在 `List` 上，但还有许多其他 `Foldable` 数据结构，例如 `Array` 或树等。

在能够对 `Arrays` 进行 `sum` 之前，请在你的测试代码中添加以下行：

```
log $ show $ sum [1, 2, 3] ❶
log $ show $ sum [1.0, 2.0, 3.0] ❷
```

+   ❶ 打印 `6`。
+   ❷ 打印 `6.0`。

所以尝试修改我们的函数使其适用于 ANY `Foldable` 类型。然后通过进入下一节来查看你的成果。

## 11.24. 使用 `Foldable` 的 `sum` 代码

```
sum :: ∀ f a. Foldable f => Semiring a => f a -> a
sum = foldl (+) zero
```

❶ 我们添加了 `Foldable f` 约束，其中 `f` 是我们的可折叠类型，例如 `List`、`Array` 等。

这个最终版本的 `sum` 是我们能做到的最灵活的。我们同时抽象了数据结构和元素。

我们可以创建一个树并使其成为 `Foldable`，然后如果树持有 `Semiring`，我们就可以对其调用 `sum`，它将无需我们额外付出努力就能正常工作。这就是类型类的真正威力。

如果我们能做到，也许我们应该这么做。

## 11.25. 使用 `Tree` 的 `sum`

这是递归定义，因为 `Tree` 类型同时出现在等号的左右两侧。

`Leaf` 是基本情况。它终止递归。

`Node` 是递归情况。

这与递归函数中基本情况和递归情况的工作方式相呼应。我们的基本情况终止了递归。

现在，我们所要做的就是让我们的树成为 `Foldable`。说起来容易做起来难。

在使其成为 `Foldable` 之前，我们必须先决定一些事情。当我们遇到 `Node` 时，我们是偏向左侧还是右侧？我们是要深度优先遍历树还是广度优先遍历。

对于 `List` 我们不需要做出这些决定，因为遍历 `List` 只有一种方式，即从头到尾。但树是一种可以以几种不同方式遍历的结构。

为了让我们的代码更简单，让我们做出一个行政决定并选择 **深度优先**。

通常，停下来为你的数据结构创建一个简单示例来帮助你开发代码是值得的。这里有一个简单的 `Tree`：

![](img/8c0e9b687c62642e828ccb5481e11313_396_0.png)

让我们看看我们的 `sum` 函数在偏向 *左侧* 时会受到什么影响：

```
0 + 5 + (-1) + 14 + 99 = 117
```

如果现在我们偏向 *右侧*，我们会得到：

```
0 + 99 + 14 + (-1) + 5 = 117
```

注意结果是相同的。所以使用 `sum` 来帮助我们决定偏向哪一边对我们帮助不大。

我们还需要记住，我们正在为所有函数编写 `Foldable` 实例，而不仅仅是 `sum`。因此，我们需要考虑最佳的遍历方式，以便对所有 `Foldable` 操作都有效，例如减法。使用减法，结果将不会相同。

但是，我们没有对这个二叉树做任何特殊说明。它只是一个二叉树。它不是平衡的也不是排序的。所以我们不能基于此信息做出任何决定。

所以，让我们再做一个行政决定，只选择 *左侧*。

现在我们已经决定了遍历方式，我们就可以为 `Tree` 编写 `Foldable` 实例了。请参阅

在所有 3 种情况下，我们传递除最后一个参数之外的所有参数。这使我们能够简单地组合这些函数，因为它们都在等待单个参数。

现在我们的树是可折叠的，我们可以在它是一个 `Semiring` 时对其调用 sum，就像我们的测试树一样：

```
(Node (Node (Leaf 5) (Node (Leaf (-1)) (Leaf 14))) (Leaf 99))
```

## 11.29. 改进 `Tree` 的 `Foldable`

如果我们想支持偏向右侧和/或广度优先遍历，那么我们可以使用 newtype 来创建具有适当行为的新类型，并为其提供自己的 toList 和 Foldable 实例。

我们甚至可以创建一个名为 ToList 的自己的类型类来使该过程更容易。

我们现在不会深入探讨这一点，但为了好玩，这里是仅深度优先的左侧和右侧偏好的实现，因为我太懒了不想写广度优先遍历代码。

以下是感兴趣者的完整实现：

```
```haskell
data Tree a = Leaf a | Node (Tree a) (Tree a)

class ToList f where ❶
  toList :: ∀ a. f a -> List a

newtype RightFirstTree a = RightFirstTree (Tree a) ❷
newtype LeftFirstTree a = LeftFirstTree (Tree a)

instance toListRightFirstTree :: ToList RightFirstTree where
  toList (RightFirstTree (Leaf x)) = singleton x
  toList (RightFirstTree (Node lt rt)) =
    toList (RightFirstTree rt) <> toList (RightFirstTree lt) ❸ ❺

instance toListLeftFirstTree :: ToList LeftFirstTree where
  toList (LeftFirstTree (Leaf x)) = singleton x
  toList (LeftFirstTree (Node lt rt)) =
    toList (LeftFirstTree lt) <> toList (LeftFirstTree rt) ❹ ❺

instance foldableRightFirstTree :: Foldable RightFirstTree where
  foldr f acc = foldr f acc <<< toList
  foldl f acc = foldl f acc <<< toList
  foldMap f = foldMap f <<< toList

instance foldableLeftFirstTree :: Foldable LeftFirstTree where
  foldr f acc = foldr f acc <<< toList
  foldl f acc = foldl f acc <<< toList
  foldMap f = foldMap f <<< toList
```
```

+   1. `ToList` 类用于区分对非列表结构的遍历。
+   2. 我们将 `Tree` 包装在这些具有明确遍历的特殊类型中。
+   3. `rt` 被前置到 `lt` 以进行右偏向遍历。
+   4. `lt` 被前置到 `rt` 以进行左偏向遍历。
+   5. 我们必须在递归之前重新包装左右 `Trees` 的 `newtype`。我们本可以派生一个 `Newtype` 实例并改用 `wrap`。

注意，我们不再需要 `Tree` 的 `Foldable` 实例或我们独立的 `toList` 辅助函数了。此外，我们的测试代码也应稍作更改：

# 第 12 章. 函子

我们将最终深入探讨函子，这是一种从数学范畴论中窃取的非常强大的抽象。我们不会在这里深入探讨范畴论，但主要集中在使用这种抽象来帮助解决编程问题的动机上。

但在我们开始之前，我想先奠定一些基础，希望能带我们一直走到应用函子和单子。

## 12.1. 定义 ADTs

当我们定义代数数据类型 ADT，例如 Maybe 时，我们对该类型代表什么有一个想法。我们一直在谈论 Maybe 是可能失败的计算结果的类型：

```
data Maybe a = Nothing | Just a
```

但在这一点上，我们只有我们的意图。我们还没有指定它的使用方式。一旦我们开始添加类型类实例，我们的意图就会变得更明确：

```
data Maybe a = Nothing | Just a
derive instance eqMaybe :: Eq (Maybe a)
derive instance ordMaybe :: Ord (Maybe a) ①
```

① 这种派生连同初始类型定义将决定 Maybe 如何排序。Nothing 会小于 Just，因为它们是先定义的。

每次我们实现另一个类型类实例时，我们都在巩固该类型的行为，选择一种可能的行为而非其他行为。这并不意味着我们不能编写代码来对 Maybe 进行排序，其中 Just 在 Nothing 之前排序，尽管 Ord 派生如此。但 Ord 的全部意义在于规定比较类型值时的行为。

我们也可以决定不为我们的类型派生 Ord，从而让使用者编写大量样板代码来实现常见功能：

```
compareMaybe :: ∀ a. Maybe a -> Maybe a -> Boolean
```

但这会短视且难以维护。它可能适用于小型代码库，但它肯定无法扩展，也无法很好地与多个项目协同工作，特别是如果 compareMaybe 在不同项目之间不同。

现在，想象我们想要计算以下数学方程：

