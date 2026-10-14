

```
newtype Reader r a = Reader (r -> a)
```

这可能对 State 也适用，只需重命名几处：

```
newtype State s a = State (s -> a) -- NOT IDEAL
```

但这种定义有一个缺点。你能看出是什么吗？

对于 Reader，我们没有返回只读值，因为它从未被修改。但对于 State 来说情况并非如此。我们应该返回新的 State。虽然在计算结束时拥有它会很不错，但如果我们希望能够组合单子函数，这一点是必不可少的。

一个函数会改变 State 并连同其计算结果一起返回它。我们会取这个新的 State 并将其传递给下一个函数，以此类推。这就是 State 的函数必须也返回新的 State 的原因，否则我们只能让 State 成为一个函子。

下面是 State 的正确版本：

```
newtype State s a = State (s -> Tuple a s)
```

现在，当 State 被运行时，它会同时返回类型为 a 的计算结果和类型为 s 的新 State。

我们将从 Functor 开始，一行一行地编写代码：

```
instance functorState :: Functor (State s) where
```

请注意，我们保持 s 不变，即我们将对 a 进行映射。如果你还没注意到，在这些情况下我们总是把 a 留作最后一个类型参数。然后我们可以保持所有其他类型参数不变。

现在来看 map 的左侧：

```
instance functorState :: Functor (State s) where
  map f (State fx) = ???
```

这里的名字 fx 提醒我们它是一个返回值的函数。

让我们从右侧的模式开始：

```
instance functorState :: Functor (State s) where
  map f (State fx) = State \s -> ???
```

就像我们之前对 Reader 和 Writer 所做的那样，我们需要以某种方式对 fx 的值应用 f。我们之前通过将 s 传递给 fx 来提取值，然后对该值应用 f 的方式来做到这一点。让我们写出来：

```
instance functorState :: Functor (State s) where
  map f (State fx) = State \s -> f $ fx s  -- COMPILER ERROR!!
```

这里是编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_735_0.png)

编译器遇到了一个 Tuple a0 s1，但期望的是 a0。并且 fx s 下有一条红色下划线，这让我认为 fx s 返回的是一个 Tuple。你能看出我们做错了什么吗？

问题在于 State 的函数具有类型 s -> Tuple a s。所以，我们是对的。fx s 确实返回一个 Tuple。这意味着我们还不能调用 f。我们需要进入那个 Tuple。

但我们不能直接对 Tuple 进行映射，因为它的定义顺序不对：

```
Tuple a s ①
```

① 我们只能对 Tuple 的第二个参数进行映射，但它是一个 s 而不是 a。

我们可以通过反转类型来修复这个问题，而我会这么做。但是，Haskell 对这种类型有着悠久的历史，而实现 State 的 PureScript 库遵循了 Haskell 的做法。所以，我们也会这样做，这意味着我们不能对 Tuple 使用 map。

我们可以使用 Bifunctor 的 lmap 来映射其左侧类型，但我们只是要在 Lambda 函数中对其进行解构：

```
instance functorState :: Functor (State s) where
  map f (State fx) = State \s -> fx s # \(Tuple x s') -> ??? ① ②
```

① 我们现在暂时去掉了对 f 的调用。

② s' 是我们的新 State，因为 f x 可能修改了它。

现在 x 的类型是 a，这意味着我们终于可以对它应用 f 了。然后我们会将该结果与新的 State s' 一起包装成一个 Tuple：

```
instance functorState :: Functor (State s) where
  map f (State fx) = State \s -> fx s # \(Tuple x s') -> Tuple (f x) s'
```

接下来是 Apply 实例。我们将以通常的方式开始：

```
instance applyState :: Apply (State s) where
```

现在来看 apply 的左侧：

```
instance applyState :: Apply (State s) where
  apply (State ff) (State fx) = ???
```

我们将 ff 和 fx 命名为提醒我们第一个函数会返回一个函数，第二个会返回一个值。

由于我们返回的是一个 State，我们将从通常的模式开始右侧：

```
instance applyState :: Apply (State s) where
  apply (State ff) (State fx) = State \s -> ???
```

现在在继续之前，我们应该在 Functor 实例的经验之后保持警惕。我们调用的任何 State 函数都会返回 Tuple。所以，我们需要像在 map 中那样对其进行解构。

但最重要的是要记住，我们必须先调用 ff 再调用 fx，因为 apply 是左结合的，而 ff 可能修改 State。我们希望先调用 ff，以确保 State 以正确的顺序被修改：

```
instance applyState :: Apply (State s) where
  apply (State ff) (State fx) = State \s -> ff s # \(Tuple g s') -> ???
```

这里 g 是 ff 返回的函数，作为 Tuple 的第一部分，s' 是新的 State。

现在我们将用新的 State s' 调用 fx：

```
instance applyState :: Apply (State s) where
  apply (State ff) (State fx) = State \s -> ff s # \(Tuple g s') -> fx s'
    # \(Tuple x s'') -> ???
```

这里 x 是 fx 返回的值，s'' 是新的、新的 State。

我们要做的唯一一件事就是将 g 应用于 x 并将其包装在 Tuple 中：

```
instance applyState :: Apply (State s) where
  apply (State ff) (State fx) = State \s -> ff s # \(Tuple g s') -> fx s'
    # \(Tuple x s'') -> Tuple (g x) s''
```

这是一团糟，但它能工作。我们本可以只使用我们老朋友的 ap，因为我们知道 State 将会是一个单子。但如果我们那样做，我们就学不到那么多。

关于使用 ap 的一个重要事实是，ap 中的顺序是为左结合性正确处理的：

```
ap :: ∀ a b m. Monad m => m (a -> b) -> m a -> m b
ap mf mx = do
  f <- ff ①
  x <- fx ②
  pure $ f x
```

① 先对 ff 调用 bind。

② 第二次对 fx 调用 bind。

使用 ap 可以防止我们在手写实现中意外交换 ff 和 fx 的顺序。如果我们犯了交换它们顺序的错误，我们不会得到编译器错误。相反，我们的程序会有细微的错误，我们可能要到代码上线后才会发现。

现在我们准备编写 Applicative 实例：

```
instance applicativeState :: Applicative (State s) where
```

现在来看右侧：

```
instance applicativeState :: Applicative (State s) where
  pure x = ???
```

我们将添加那个从未让我们失望的熟悉模式：

```
instance applicativeState :: Applicative (State s) where
    pure x = State \s -> ???
```

我们所要做的就是将 x 与 State s 的无变化一起放入我们的 Tuple 中：

```
instance applicativeState :: Applicative (State s) where
    pure x = State \s -> Tuple x s
```

喜欢 Applicative 的实现。它通常相当容易。

现在我们将编写 Bind 实例：

```
instance bindState :: Bind (State s) where
```

以及右侧：

```
instance bindState :: Bind (State s) where
    bind (State fx) f = ???
```

我们正在解构以获取对 fx 的访问，即将返回值的函数。

在急于编写左侧代码之前，我们应该记住每次编写 Bind 实例时都会遇到的问题。你还记得那是什么吗？

它在于 f 是一个单子函数，而不是像 map 和 apply 中的纯函数。所以我们需要像在 Reader 中那样解包其输出。你还记得我们是如何做到的吗？

我们使用 runReader 来解包在 Reader 的 bind 中调用 f 的结果。我们将需要对 State 做同样的事情。

此时，我们应该编写 runState。我们将以 runReader 为模板：

```
runReader :: ∀ a r. Reader r a -> (r -> a)
runReader (Reader f) = f
```

我看不出 runState 不能只是用几个名字更改完全相同的原因：

```
runState :: ∀ a s. State s a -> (s -> a)
runState (State f) = f -- COMPILER ERROR!!
```

唉... 看来确实有区别。但是什么呢？

这里是编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_739_0.png)

现在，我明白为什么它们不一样了。我忘了 Tuple。那很容易修复：

```
runState :: ∀ a s. State s a -> (s -> Tuple a s) ①
runState (State f) = f
```

① 将 s -> a 改为 s -> Tuple a s。

现在我们可以完成 bind 的代码。这里是我们停下的地方：

```
instance bindState :: Bind (State s) where
  bind (State fx) f = ???
```

让我们从右侧的模式开始：

```
instance bindState :: Bind (State s) where
  bind (State fx) f = State \s -> ???
```

现在我们将通过传递 State s 来从 fx 中提取 x：

```
instance bindState :: Bind (State s) where
  bind (State fx) f = State \s -> fx s ???
```

然后解构结果，即 Tuple：

