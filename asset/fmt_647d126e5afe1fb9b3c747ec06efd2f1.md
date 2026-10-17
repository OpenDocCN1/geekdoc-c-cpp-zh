
这就是我们实现适当结合性的方式。这也是传递给 `foldr` 的函数是传递给 `foldl` 的函数的翻转版本的原因：

```
foldr :: ∀ a b. (a -> b -> b) -> b -> f a -> b
foldl :: ∀ a b. (b -> a -> b) -> b -> f a -> b
```

记住，`flip` 交换函数的前两个参数。

## 10.4. List 的 Foldable

让我们查看 `List` 的 `Foldable` 实现的细节。

首先，我们来看实例定义：

```
instance foldableList :: Foldable ??? where
```

我们在其他类型类中放入 `???` 的内容是具有其所有参数的类型，例如 `List a` 或 `Maybe a`，如：

```
instance eqMaybe :: Eq a => Eq (Maybe a) where
  ... ①
```

① 实现细节在这里不重要。

这是因为如果我们查看 `Eq` 类型类的定义，我们会发现：

```
class Eq a where
  eq :: a -> a -> Boolean
```

`Eq` 类的类型参数是 `a` 并且其 `Kind` 是 `Type`。

> 类型以与 `Kind` 对类型相同的方式对值进行分类，即值具有类型，类型具有 `Kind`。换句话说，值的类型称为类型，而类型的类型称为 `Kind`。

将上面的 `Eq` 定义与 `Foldable` 进行比较：

`class Foldable f where`

  `foldr :: ∀ a b. (a -> b -> b) -> b -> f a -> b`

  `foldl :: ∀ a b. (b -> a -> b) -> b -> f a -> b`

  `foldMap :: ∀ a m. Monoid m => (a -> m) -> f a -> m`

`Foldable` 类的类型参数是 `f`，当我们查看方法类型签名中 `f` 的使用方式时，可以看到 `f` 接受另一个类型，即 `a`。

这意味着 `f` 的 `Kind` 是 `Type -> Type`，即 `f` 是一个**类型构造子**。就像数据构造子一样，我们可以将类型构造子视为函数，只是其参数是类型。

这里 `f` 是一个类型构造子，它期望一个 `Type` 类型的单个参数，并返回一个 `Type`。

为了更好地理解类型构造子与数据构造子之间的相似性，让我们看看一些常见数据构造子的类型签名：

```
Just  :: ∀ a. a -> Maybe a
Left  :: ∀ a. a -> Either a b
Right :: ∀ b. b -> Either a b
```

注意数据构造子接受一个值并返回一个值。

而现在一些类型构造子的 *Kind 签名* 示例：

```
Maybe   :: Type -> Type
Either  :: Type -> Type -> Type
```

注意类型构造子接受类型并返回类型。

现在我们理解了这些差异，应该很清楚我们需要以不同的方式指定类定义：

```
instance foldableList :: Foldable List where
```

`List` 的 `Kind` 是 `Type -> Type`，这与 `f` 的类型签名匹配。注意我们没有在任何地方提到 `a`。

当 `f` 被 `List` 替换时，方法的类型签名专门化为：

```
instance foldableList :: Foldable List where
  foldr :: ∀ a b. (a -> b -> b) -> b -> List a -> b
  foldl :: ∀ a b. (b -> a -> b) -> b -> List a -> b
  foldMap :: ∀ a m. Monoid m => (a -> m) -> List a -> m
```

注意我们所做的只是将 `f` 替换为 `List`。我们可以这样做，因为 `f` 接受一个单一的类型参数 `a`，而 `List` 也是如此。我们同样可以轻松地将 `f` 替换为 `Array` 或 `Maybe`。

但我们不能用 `Either` 替换它，因为它的 `Kind` 签名是 `Type -> Type -> Type`。相反，我们必须固定第一个参数并用 `Either a` 替换 `f`。这可行，因为我们正在用其第一个参数部分应用类型构造子。`Either a` 的 `Kind` 签名是 `Type -> Type`，这现在与 `List`、`Array`、`Maybe` 和 `f` 匹配。

现在开始编写 `foldr`。首先是基本情况：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil = acc
```

这里我们只是提供累积结果。这是我们初始状态，如果我们从空列表开始，或者我们在耗尽列表时被传递的状态。

接下来，我们编写递归情况：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = ???
```

在确定等号右侧要写什么之前，我们必须记住要使其为右结合。让我们再看看它是什么样子：

```
foldr (-) 99 [1, 2, 3] == 1 - (2 - (3 - 99)) == -97
```

注意我们的初始值 `99` 直到我们到达列表末尾才在计算中使用。这意味着我们需要递归地传递这个初始值，直到耗尽列表。我们可以看到基本情况将简单地把这个初始值返回给我们，然后我们就可以开始进行计算。

这很好，因为我们希望最后一个元素在我们执行的第一个计算中被使用。这就是右结合的含义。如果你计算上面的例子，你会做的第一件事是 `3 - 99`。我们的函数需要以相同的方式执行。

所以我们的策略是，保持递归，传递我们的初始值，只有当我们到达末尾时，我们才会执行函数（在我们的例子中是减法）并将结果返回给之前的调用，然后它会用前一个值执行函数，以此类推：

```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
```

❶ 基本情况返回初始值。

❷ 这里我们可以看到我们推迟了函数调用 `f`，直到 `(foldr f acc xs)` 被计算。并且每次后续递归都会这样做，直到最后一个元素与初始值一起计算（从基本情况返回的值）。

为了从不同角度了解其工作原理，让我们通过代数替换逐步查看执行过程：

```haskell
foldr (-) 99 [1, 2, 3] =                 -- initial call
(-) 1 (foldr (-) 99 [2, 3]) =             -- substitution into ❷
(-) 1 ((-) 2 (foldr (-) 99 [3])) =        -- substitution into ❷
(-) 1 ((-) 2 ((-) 3 (foldr (-) 99 []))) = -- substitution into ❷
(-) 1 ((-) 2 ((-) 3 99)) =                -- substitution into ❶
(-) 1 ((-) 2 (3 - 99)) =                  -- rewrite prefixed as infixed
(-) 1 (2 - (3 - 99)) =                    -- rewrite prefixed as infixed
1 - (2 - (3 - 99)) =                      -- rewrite prefixed as infixed
```

注意 `99`，我们的初始值，被一路传递下来，直到它在与最后一个元素 `3` 的计算中被需要。

接下来，我们编写 `foldl` 的基本情况：

```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
```

然后是递归情况：

```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = ???
```

在确定等号右侧要写什么之前，我们必须记住要使其为左结合。让我们再看看它是什么样子：

```
foldl (-) 99 [1, 2, 3] == ((99 - 1) - 2) - 3 == 93
```

在这种情况下，我们立即使用初始值并将其结果作为新的累加器值传递给递归调用：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc ①
  foldl f acc (x : xs) = foldl f (f acc x) xs ②
```

让我们通过代数替换逐步查看执行过程：

```
foldl (-) 99 [1, 2, 3] =                 -- initial call
foldl (-) ((-) 99 1) [2, 3] =           -- substitution into ②
foldl (-) ((-) ((-) 99 1) 2) [3] =     -- substitution into ②
foldl (-) ((-) ((-) ((-) 99 1) 2) 3) [] = -- substitution into ②
(-) ((-) ((-) 99 1) 2) 3 =             -- substitution into ①
(-) ((-) (99 - 1) 2) 3 =                -- rewrite prefixed as infixed
(-) ((99 - 1) - 2) 3 =                   -- rewrite prefixed as infixed
((99 - 1) - 2) - 3 =                     -- rewrite prefixed as infixed
```

在继续 `foldMap` 之前，我们可以做一些观察。当我们使用 `foldl` 或 `foldr` 时，我们正在使用 `acc` 变量传递状态。我们一直称之为累加器，但它实际上是我们的状态。

由于函数式编程中没有全局状态，我们能做的最好的就是从一次调用传递到下一次调用：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc ①
  foldr f acc (x : xs) = f x (foldr f acc xs) ②
  foldl _ acc Nil      = acc ③
  foldl f acc (x : xs) = foldl f (f acc x) xs ④
```

- ① 这里 `acc` 是我们的初始状态。
- ② 我们的初始状态被传递。
- ③ 这里 `acc` 是我们的最终状态。
- ④ 新状态被传递。

在 `foldl` 的情况下，我们将新状态传递给递归调用，而在 `foldr` 的情况下，我们从递归调用返回新状态。

花点时间让这一点沉淀下来。在函数式编程中，我们只能传递状态更改或返回状态更改。这将是我们查看状态单子时要重访的概念。

现在，我们准备编写 `foldMap`。

首先，我们添加基本情况：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
```

- 基本情况。

幸运的是，`Monoid` 有一个空元素。所以当我们得到一个空列表时，我们有一个值可以返回，即 `Monoid` 的空元素，`mempty`。

最后，我们添加递归情况：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f (x : xs)   = ???
```

- 递归情况。

在填充 `???` 时我们可以采取两种可能的方法。我们可以右结合或左结合：

```
foldMapL f = foldl (\acc x -> acc <> f x) mempty
foldMapR f = foldr (\x acc -> f x <> acc) mempty
```

- 以无点表示法编写，其中列表未明确定义。
- 累加器在 `<>` 的左侧，因此为左结合。
- 累加器在 `<>` 的右侧，因此为右结合。

在 PureScript 库中，有 2 个函数，`foldMapDefaultR` 和 `foldMapDefaultL`，其效果与上述代码相同。

事实证明，`Array` `Foldable` `Typeclass` 的作者选择了右结合，而 `List` 的作者选择了左结合。

虽然这很不幸，但我们可以将 `List` 和 `Array` 之间相互转换，因此我们可以选择其中一个。我们也可以显式地对 `Lists` 调用 `foldMapDefaultR`。但这些非默认的解决方案无法受益于 `Typeclasses`。

因此，让我们选择左结合以匹配库作者的选择：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f l          = foldl (\acc x -> acc <> f x) mempty l ①
```

① 我们在使用模式匹配时无法写成 Point-free 形式。

## 10.5. 使用 Folds 重写 length

由于 `foldl` 和 `foldr` 传递 `State`，我们可以使用 `Fold` 来重新编码 `length` 的尾递归版本。在此之前，让我们回顾一下 `length` 的那个版本：

```
length :: ∀ a. List a -> Int
length l = go 0 l where ①
  go :: ∀ a. Int -> List a -> Int ①
  go acc Nil      = acc
  go acc (x : xs) = go (acc + 1) xs ②
```

① 第一个参数是我们的 `State`，即当前计数，它从 `0` 开始。
② 每次迭代我们将计数加 `1`。

要使用 `foldl` 或 `foldr`，我们需要确定 2 件事。首先，`State` 是什么以及其初始值是什么。在这种情况下，它是 `List` 中元素的计数，其初始值为 `0`。

需要确定的第二件事是每次迭代我们将执行什么操作。在这种情况下，我们只需将计数加 `1`。

需要确定的最后一件事是我们是否关心结合性。由于我们的操作是 `+`，它是可交换的，即顺序无关紧要，我们不关心结合性。

因此我们可以选择 `foldl` 或 `foldr`，结果将相同：

```
(((1 + 1) + 1) + 1) = (1 + (1 + (1 + 1)))
```

但还有一个因素需要考虑。这里是我们为 `List` 实现的 `Foldable`：

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f l          = foldl (\acc x -> acc <> f x) mempty l
```

比较 `foldr` 和 `foldl` 的实现，看看你是否能找到使用其中一个而不是另一个的理由。

如果你看不出为什么一个会比另一个更受青睐，看看哪一个更高效。

事实证明 `foldl` 比 `foldr` 更高效，因为 `foldl` 是尾递归的，而 `foldr` 不是。因此我们选择它来使用 `foldl` 重写 `length`：

```
length :: ∀ a. List a -> Int
length = foldl (\count _ -> count + 1) 0 ①
```
