
注意我们只需要对代码的 3 个部分进行修改。这要归功于我们在重构中所做的工作，将 Stack 变更的影响局部化。

现在，我们需要重写 test：

```
test :: Effect Unit
test = do
  result1 <- runApp 0 app ①
  Console.log $ show result1
  result2 <- runApp 99 app ①
  Console.log $ show result2
```

① 由于 runApp 现在运行在 Effect 中，我们需要提取它的结果。

我们新 test 函数的输出将与 Identity 作为基础 Monad 时完全一致。

## 20.7. 编写 WriterT

我们已经谈论 Monad 变换器相当长时间了，但一如既往，它们所做的一切看起来就像魔法，直到你真正查看代码为止。而当你自己动手编写时，这种感觉就更少了。

我们将一起编写 WriterT，以帮助我们理解它如何实现 Monad 变换器所特有的功能。

让我们从类型开始：

```
newtype WriterT w m a = WriterT (m (Tuple a w))
```

注意相较于我们的 Writer 实现，这里多了一个类型参数 m：

```
newtype Writer w a = Writer (Tuple a w)
```

这是因为 WriterT 的结果现在位于其底层 Monad（即 Stack 中位于它下方的那个 Monad）的上下文中。

接下来，我们逐行编写 runWriterT：

```
runWriterT :: ∀ w m a. WriterT w m a -> ???
```

写到这里很容易。但这个函数返回什么？对于 Writer，我们直接返回一个 Tuple a w，即纯计算和日志，但现在我们必须考虑底层 Monad。

请记住，底层 Monad 会在 WriterT 之后运行。因此，我们需要在底层 Monad 的上下文中返回结果。

让我们添加典型的 Writer 返回结果，即 Tuple a w，但放入底层 Monad 上下文 m 中：

```
runWriterT :: ∀ w m a. WriterT w m a -> m (Tuple a w)
```

现在，我们来编写等号左侧的部分：

```
runWriterT :: ∀ w m a. WriterT w m a -> m (Tuple a w)
runWriterT (WriterT mx) = ??? ①
```

① mx 提醒我们，在 Monad 上下文中有一个值。通过查看 WriterT 的数据构造函数，我们可以知道这一点。

考虑要返回什么时，可能性并不多，因为我们只有 mx。我想到的第一个问题是：mx 的类型签名是否与我们的返回值相符？答案是相符的。所以我们直接返回它：

```
runWriterT :: ∀ w m a. WriterT w m a -> m (Tuple a w) ①
runWriterT (WriterT mx) = mx
```

① 返回 WriterT 底层 Monad（即 m）中的一个值。

接下来，我们逐步编写 Functor 实例：

```
instance functorWriterT :: Functor (WriterT w m) where ①
```

① 和往常一样，除最后一个类型参数（即 a）外，我们保持所有类型参数不变。

现在处理等号左侧部分：

```
instance functorWriterT :: Functor (WriterT w m) where
  map f (WriterT mx) = ??? ①
```

① 我们解构 WriterT，以获得内部的 Monadic 值。

现在，我们必须将映射函数 f 作用到这个 Monadic 值上，然后重新包装进 WriterT：

```
instance functorWriterT :: Functor (WriterT w m) where
  map f (WriterT mx) = WriterT $ f <$> mx -- COMPILER ERROR!!
```

我们收到以下错误：

![](img/8c0e9b687c62642e828ccb5481e11313_907_0.png)

从这个错误中，我看出自己完全忘记了 Tuple。如果 mx :: m a 成立，我写的代码就能工作，但实际上我们有的是 mx :: m (Tuple a w)。

让我们通过在一个 Lambda 上映射来提取 Tuple，从而修复这个问题：

```
instance functorWriterT :: Functor (WriterT w m) where
  map f (WriterT mx) = WriterT $ mx <#> \(Tuple x w) -> ???
```

1 使用 <$> 的反转版本，即 <#>。当 Lambda 位于右侧时，可读性更好。

现在我们可以将映射函数 f 应用到 Tuple 的第一个元素上，同时别忘了返回一个 Tuple：

```
instance functorWriterT :: Functor (WriterT w m) where
  map f (WriterT mx) = WriterT $ mx <#> \(Tuple x w) -> Tuple (f x) w
```

请注意，在底层 Monad 中进行额外的映射，正是这个 Functor 实现与 Writer 的不同之处。我们可以预期，这一点对于我们编写的所有实例都成立。

接下来是 Apply 实例：

```
instance applyWriterT :: Apply (WriterT w m) where
```

1 和往常一样，除最后一个类型参数（即 a）外，我们保持所有类型参数不变。

现在处理等号左侧部分：

```
instance applyWriterT :: Apply (WriterT w m) where
    apply (WriterT mf) (WriterT mx) = ??? ①
```

① mf 提醒我们，底层 Monad 中有一个函数；mx 则提醒我们，底层 Monad 中有一个值。

此时，我们可以采用与 Functor 相同的方法，但我们需要 2 个 Lambda，一个用于 mf，另一个用于 mx。那样代码会变得丑陋且冗长。

但是，我们知道我们有一个底层 Monad，所以可以借助 do 表示法来让代码更简洁：

```
instance applyWriterT :: Apply (WriterT w m) where
    apply (WriterT mf) (WriterT mx) = do
        ???
```

我们要做的第一件事是从 mf 中提取 Tuple（这次我可没忘记 Tuple）：

```
instance applyWriterT :: Apply (WriterT w m) where
    apply (WriterT mf) (WriterT mx) = do
        Tuple f w1 <- mf
        ???
```

现在我们将提取 mx 的 Tuple：

```
instance applyWriterT :: Apply (WriterT w m) where
    apply (WriterT mf) (WriterT mx) = do
        Tuple f w1 <- mf
        Tuple x w2 <- mx
        ???
```

现在我们可以将 f 应用到 x，并将所有内容重新包装到 Tuple 中，然后再放入底层 Monad：

```
instance applyWriterT :: Apply (WriterT w m) where
    apply (WriterT mf) (WriterT mx) = do
        Tuple f w1 <- mf
        Tuple x w2 <- mx
        pure $ Tuple (f x) ??? ①
```

① Tuple 数据构造函数将内容包装成一个 Tuple，随后 pure 将这个 Tuple 包装在底层 Monad 中。编译器会根据底层 Monad 是什么来决定使用哪个 pure 实现。

剩下唯一要解决的问题是，如何合并日志并将它们放到 Tuple 的第二个位置。

如果日志类型是 Semigroup，这应该很容易。所以，让我们给它加上一个：

```
instance applyWriterT :: Semigroup w => Apply (WriterT w m) where
  apply (WriterT mf) (WriterT mx) = do
    Tuple f w1 <- mf -- COMPILER ERROR!
    Tuple x w2 <- mx
    pure $ Tuple (f x) (w1 <> w2)
```

+   1. 添加了 Semigroup 约束。
+   2. 使用 `<>` 组合日志。

编译器正在报错：

![](img/8c0e9b687c62642e828ccb5481e11313_909_0.png)

它在为 m3（也就是我们所说的 m）寻找 Bind 实例，因为我们在用 do 表示法来利用底层 Monad。所以让我们把 m 约束为 Bind：

```
instance applyWriterT
    :: (Semigroup w, Bind m) => Apply (WriterT w m) where
  apply (WriterT mf) (WriterT mx) = do
    Tuple f w1 <- mf -- COMPILER ERROR!
    Tuple x w2 <- mx
    pure $ Tuple (f x) (w1 <> w2)
```

+   1. 这里有一个语法说明：对于类型类实例，我们需要在括号内用逗号分隔来添加多个约束。

```
No type class instance was found for
runW
runW        Control.Applicative.Applicative m2

inst
  ma while checking that type forall a f. Applicative
      is at least as general as type t0 -> t1
inst while checking that expression pure
  ap   has type t0 -> t1
  ap in value declaration applyWriterT

    where m2 is a rigid type variable
pure $ Tuple (f x) (w1 <> w2)
```

由于我们在使用 pure，它要求 m 有 Applicative 约束。但我们已经有了 Bind 约束。如果我们将这两个约束组合起来，就得到一个 Monad 约束，因为它们都是 Monad 的超类。

让我们将 Bind 约束改为 Monad 约束：

```
instance applyWriterT
  :: (Semigroup w, Monad m) => Apply (WriterT w m) where ①
apply (WriterT mf) (WriterT mx) = WriterT do
  Tuple f w1 <- mf
  Tuple x w2 <- mx
  pure $ Tuple (f x) (w1 <> w2)
```

① 将 Bind 约束改为 Monad 约束。

回顾我们刚才所做的工作，可以看出我们始终确保在底层 Monad 中操作。这似乎是一个反复出现的主题。

你可能会问，我们是否可以跳过这些编写，直接使用 ap 来“作弊”，因为 WriterT 最终会是一个 Monad。答案是肯定的，但那样我们就学不到这么多东西了。

接下来，我们将编写 Applicative 实例：

```
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where ①
```

① 我们主动在这里添加了与 Apply 相同的约束，因为它是我们的超类。

接下来，是等号左侧的代码：
