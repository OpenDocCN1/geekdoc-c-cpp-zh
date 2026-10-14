

# 16.10. Functors 与带效应的 Applicatives

记住，基于 Functor 定律，对 Just 或 Right 进行映射始终会分别产生 Just 或 Right：

```
(5 * _) <$> Just 10 = Just 50
(5 * _) <$> Right 10 = Right 50
```

对于 Applicative 来说则不是这样：

```
Just (5 * _) <*> Nothing = Nothing
Right (5 * _) <*> Left "err" = Left "err"
```

这里我们从一个 Just 开始并应用了一个 Nothing，结果得到 Nothing。我们也把一个 Right 变成了 Left。

由此，我们可以说以下几点：

- Functors 本身 CANNOT 具有 Effect，即一旦是 Just 永远是 Just。一旦是 Nothing，永远是 Nothing。
- Applicatives CAN 具有 Effect，即一个 Just 可以变成 Nothing，而一个 Right 可以变成 Left。

map 和 apply 都是将函数应用到上下文中的值。不同之处在于，对于 apply，函数本身也在一个上下文中。因此，有机会出现 2 种不同的数据结构，例如函数在一个 Just 中而值是 Nothing，或者函数在一个 Right 中而值在一个 Left 中。

这些不同的数据结构必须以某种方式组合以产生单一的数据结构。我们别无选择，只能以某种逻辑且有用的方式在两者之间做出选择。在这种情况下，由于 Maybe 的隐式行为，即其“effect”，是短路，我们会优先考虑 Nothings 而非 Justs 以保持这种行为：

```
Just (5 * _) <*> Nothing = Nothing ①
Nothing <*> Just 2 = Nothing ①
Just (5 * _) <*> Just 2 = Just 10 ②
Nothing <*> Nothing = Nothing ③
```

① 我们优先考虑 Nothing 而非 Just。

② 因为两者都是 Just，所以无需选择。

③ 因为两者都是 Nothing，所以无需选择。

# 16.11. Applicative 效应的示例

像 Maybe 一样，Either 的“effect”也是短路：

```
instance applyEither :: Apply (Either a) where
  apply (Left f) _ = (Left f) ①
  apply _ (Left x) = (Left x)
  apply (Right f) (Right x) = Right (f x)
```

① 注意我们先匹配左侧。这意味着第一个错误会被保留。我们在之前的 combineList 示例中见过这种行为。

如果 Left 以任何方式组合，结果将是一个 Left，偏向二元运算符的左侧，即第一个 Left。

对于 Array 和 List 而言，其“effect”是多个值：

```
Tuple <$> [10,20] <*> [3, 4]
  -- [(Tuple 10 3),(Tuple 10 4),(Tuple 20 3),(Tuple 20 4)]
```

此示例返回 2 个数组的所有组合，即笛卡尔积。注意它按从左到右的顺序组合每个数组，例如结果数组的第一个元素是 Tuple (10, 3)，它是两个数组的最左侧值。而结果数组的最后一个元素是 Tuple (20, 4)，它是两个数组的最右侧值。

# 16.12. Applicative 效应与交换律

Applicative 当且仅当它是可交换的 IFF：

```
f <$> x <*> y = flip f <$> y <*> x
```

这表示如果我们将参数 x 和 y 应用于 f，并且它等于翻转函数中的参数然后以相反顺序应用 x 和 y，那么 <*> 是可交换的。

注意这个测试如何适用于 Maybe：

```
(+) <$> Just 3 <*> Just 9      -- Just 12
flip (+) <$> Just 9 <*> Just 3      -- Just 12

(-) <$> Just 3 <*> Just 9      -- Just -6
flip (-) <$> Just 9 <*> Just 3      -- Just -6

(+) <$> Just 3 <*> Nothing      -- Nothing
flip (+) <$> Nothing <*> Just 3 -- Nothing

(+) <$> Nothing <*> Just 4      -- Nothing
flip (+) <$> Just 4 <*> Nothing -- Nothing
```

① 注意 <*> 即使 (-) 不是可交换的也是可交换的。这是因为我们同时翻转了参数和函数。

但这个测试对 Either 失败：

```
(+) <$> Left "err1" <*> Left "err2"      -- Left "err1"
flip (+) <$> Left "err2" <*> Left "err1"      -- Left "err2"
```

它对 Array（或 List）也失败：

```
(+) <$> [2,3] <*> [7, 13]      -- [9,15,10,16]
flip (+) <$> [7, 13] <*> [2,3]      -- [9,10,15,16]
```

# 16.13. Traversables

让我们考虑一个我们时不时会遇到的常见场景。首先，我们有一个 Int 数组，我们想用所谓的 Effectful 函数对其进行映射，即一个函数不会产生纯值，而是产生上下文中的值：

```
half :: Int -> Maybe Int

 half x = if even x then Just (x `div` 2) else Nothing

map half [2, 4, 6]      -- [Just 1, Just 2, Just 3]

map half [2, 3, 4]      -- [Just 1, Nothing, Just 2]
```

① half 的非 effectful 版本将简单地返回 Int。

但我们不想要一个 Maybe 数组。我们想要 Int，但只有在没有失败的情况下。听起来熟悉吗？

我们可以使用我们旧的朋友 combineLists 来实现这一点：

```
import Data.List (fromFoldable)

half :: Int -> Maybe Int
half x = if even x then Just (x `div` 2) else Nothing

combine = combineLists . fromFoldable ①

map half [2, 4, 6]            -- [Just 1, Just 2, Just 3]
combine $ map half [2, 4, 6] -- Just [1, 2, 3] ②

map half [2, 3, 4]            -- [Just 1, Nothing, Just 2]
combine $ map half [2, 3, 6] -- Nothing ③
```

① 一个小助手函数以减少代码冗余。

② 这里我们得到一个数组，因为我们没有失败。

③ 这里我们得到 Nothing，因为计算失败了。这里的“effect”是我们在错误上短路并返回 Nothing。

我们的 combineList 对于这种常见场景非常方便。事实上，它如此常见，以至于它已被编纂并推广为一个名为 Traversable 的 Typeclass。

> Traversable 是一个可折叠的 Functor，可以在遍历的同时在 Applicative 中累积结果和效应。

以下是 PureScript 的 Traversable 类型类：

```
class (Functor t, Foldable t) <= Traversable t where
  traverse :: ∀ a b m. Applicative m => (a -> m b) -> t a -> m (t b)
  sequence :: ∀ a m. Applicative m => t (m a) -> m (t a)
```

这很抽象，所以让我们一步一步地解析它。

首先，类定义：

```
class (Functor t, Foldable t) <= Traversable t where
```

Traversable 类型 t 既是 Functor 也是 Foldable。在 combineList 示例中，我们有一个值数组（数组是一个 `Foldable），我们对其进行映射（要映射需要 Functor）。

接下来，让我们看看 traverse：

```
class (Functor t, Foldable t) <= Traversable t where
    traverse :: ∀ a b m. Applicative m => (a -> m b) -> t a -> m (t b) ①
```

① 这里使用变量 m 是因为 Monads 是 Applicatives 并且许多 Applicatives 也是 Monads，但如果问我，它应该叫做 f（在 Haskell 中就是这样）。

a -> m b 是我们的 effectful 映射函数，例如 half :: Int -> Maybe Int。

t a 是我们的 Foldable 数据结构，例如 Array Int。

m (t b) 是我们的最终结果，例如 Maybe (Array Int)。

但有时，我们从一个已经包含上下文中值的 Foldable 结构开始。这时 sequence 就派上用场了：

```
class (Functor t, Foldable t) <= Traversable t where
    traverse :: ∀ a b m. Applicative m => (a -> m b) -> t a -> m (t b)
    sequence :: ∀ a m. Applicative m => t (m a) -> m (t a)
```

t (m a) 是我们的上下文值的 Foldable，例如 Array (Maybe Int)。

m (t a) 是我们的最终结果，例如 Maybe (Array Int)。

sequence 只是没有映射函数的 traverse，因此：

```
sequence = traverse identity
```

换句话说，调用 sequence 等同于调用 traverse，其中映射函数是 identity，这会保持所有值不变。

仔细查看 sequence 的类型签名：

```
sequence :: ∀ a m. Applicative m => t (m a) -> m (t a)
```

注意 t 和 m 位置互换了。在 traverse 中它们也互换了，但由于涉及函数所以更难看出。这种交换看起来像魔法，但不是。它非常酷且有用。

所以想象你有以下场景，其中 Maybe 是我们的 Applicative m，Array 是我们的 Foldable 和 Functor t，a 是 Int：

```
x :: Array (Maybe Int) -- t (m a)
sequence x :: Maybe (Array Int) -- m (t a)
```

在这种情况下，如果数组中的任何 Maybe 是 Nothing，则结果将是 Nothing。同理：

```
x :: Array (Either String Int) -- t (m a)
sequence x :: Either String (Array Int) -- m (t a)
```

如果数组中的任何 Either 是 Left，则结果将是第一个 Left。

但这是如何工作的？

这是对 Maybe 和 Either 有效的原因，因为它们的 apply 实例被编码为在这些情况下短路。到目前为止，还不清楚 <*> 的代码如何影响 sequence 或 traverse。

但在我们编写 List 的 Traversable 实例时就会清楚。它也将变得清晰，为什么 m 上有 Applicative 约束。

# 16.14. List 的 Traversable

编写这个实例很难。如果你查看 PureScript 库中的源代码寻求帮助，它不会很有帮助。事实上，这里就是它：

```
instance traversableList :: Traversable List where
  traverse f = map (foldl (flip (:)) Nil)
    <<< foldl (\acc -> lift2 (flip (:)) acc <<< f) (pure Nil) ①
  sequence = traverse identity
```

① lift2 是一个助手函数，将纯函数提升到 Applicative 中。它内部执行 map 和 apply。它可以从 Control.Apply 导入。

这很难理解，因为它使用 foldl 来利用其尾递归特性，这使其在空间上高效但在时间上不高效，因为它需要遍历列表两次。

它需要两次遍历，因为使用 foldl 会以相反的顺序生成列表。map (foldl (flip (:)) Nil) 部分用于在 Applicative 内部反转列表。这是第二次遍历列表。

相反，我们将使用 foldr 编写它，这在时间上高效但不在空间上。但真正的原因是 foldr 实现要简单得多，更容易理解。

下一个困难之处在于 traversable 太抽象了。因此，为了帮助我们更清晰地思考，我们将创建一个简单的具体示例来制定策略。

