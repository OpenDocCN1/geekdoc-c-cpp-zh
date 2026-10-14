
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f = State \s -> fx s # \(Tuple x s') -> ???
```

现在，我们可以对 x 调用 f，这正是 bind 的意义所在：

```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> f x -- COMPILER ERROR!
```

我们对此编译器错误并不感到意外，因为我们记得 f 是一个 Monad 函数，这意味着我们需要对 f x 调用 runState。我们还记得需要将新的 State s' 作为第二个参数传给 runState：

```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s' ???
```

现在我们对 runState 的结果进行解构，它是一个 Tuple：

```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s'
      # \(Tuple y s') -> ???
```

现在我们可以把所有内容重新组合起来，完成定义：

```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s'
      # \(Tuple y s'') -> Tuple y s'' ❶
```

❶ 这里发生了什么？

看看最后一个 Lambda，\(Tuple y s'') -> Tuple y s''，我们可以发现它实际上就是 identity（恒等函数）。

看起来我在这里有点跑题了。当我们加上 runState 时其实已经完成了。所以，让我们稍微回退一下：

```haskell
instance bindState :: Bind (State s) where
    bind (State fx) f =
        State \s -> fx s # \(Tuple x s') -> runState (f x) s'
```

最后但同样重要的是，我们还有 Monad 实例：

```haskell
instance monadState :: Monad (State s)
```

以下是我们为 State 编写的代码：

```haskell
newtype State s a = State (s -> Tuple a s)

instance functorState :: Functor (State s) where
    map f (State fx) = State \s -> fx s # \(Tuple x s') -> Tuple (f x) s'

instance applyState :: Apply (State s) where
    apply (State ff) (State fx) = State \s -> ff s # \(Tuple g s') -> fx s'
        # \(Tuple x s'') -> Tuple (g x) s''

instance applicativeState :: Applicative (State s) where
    pure x = State \s -> Tuple x s

instance bindState :: Bind (State s) where
    bind (State fx) f =
        State \s -> fx s # \(Tuple x s') -> runState (f x) s'

instance monadState :: Monad (State s)
```

而且毫不意外，这里并没有多少代码。为了编写这么一点点代码，我们投入了大量的思考。

但我们还没有完全完成。我们仍然需要编写 State API：

```haskell
get :: ∀ s. State s s
put :: ∀ s. s -> State s Unit
modify :: ∀ s. (s -> s) -> State s s
modify_ :: ∀ s. (s -> s) -> State s Unit
```

其中 get 会获取当前的 State，而 put 会替换当前的 State。

modify 将使用一个函数来修改当前的 State，该函数接收旧的 State 并返回新的 State。modify 同时也会返回新的 State；而 modify_ 与 modify 行为相同，但返回 Unit。

在实践中，modify_ 使用得更频繁，因为它在 do 块中不需要 void，而且我们很少需要拿回新的 State。但当我们需要时，modify 可以省去一次对 get 的调用。

让我们从 get 开始：

```haskell
get :: ∀ s. State s s
get = ???
```

我们需要返回一个 State，因此我们会使用我们的模式：

```haskell
get :: ∀ s. State s s
get = State \s -> ???
```

现在，我们要做的就是将 State 原封不动地返回在 Tuple 的两个槽位中，因为最终的纯计算结果就是该 State：

```haskell
get :: ∀ s. State s s
get = State \s -> Tuple s s
```

这里 Tuple 的第一个 s 是纯计算结果，第二个 s 是 Monad 计算结果。这就像 Reader 中的 ask 一样。

现在我们来编写 put：

```haskell
put :: ∀ s. s -> State s Unit
put s = ???
```

这会稍微棘手一些。put 接收一个新的 State s，它将被用来替换传入的任何 State。所以，我们将从我们一贯用于返回 State 的模式开始，但在这里我们会丢弃那个通常被称为 s 的参数：

```haskell
put :: ∀ s. s -> State s Unit
put s = State \_ -> ??? ①
```

① _ 通常会被命名为 s，但我们并不关心旧 State 的值，因为我们要替换它。

现在，我们可以返回新 State s 和 unit，将它们包装在一个 Tuple 中：

```haskell
put :: ∀ s. s -> State s Unit
put s = State \_ -> Tuple unit s ①
```

① unit 是纯计算结果，s 是 Monad 计算结果。

你能想到为什么返回类型是 State s Unit 吗？我们还可以用其他什么来替代 Unit？

我们本可以使用 Int，也就是说返回 Tuple 0 s 而不是 Tuple unit s。但这里没有理由使用 0，也没有理由使用任何 Int 值。

Unit 在这里起作用有两个原因。第一，它是一个“无关紧要”的值；第二，它有一个 Discard 实例，这意味着当我们在 do 块中使用 put 时，不必使用 void 来丢弃返回的值。

现在我们来编写 modify：

```haskell
modify :: ∀ s. (s -> s) -> State s s
modify f = ???
```

我们需要返回一个 State，所以我们会加上我们的模式：

```haskell
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> ???
```

记住，f 用于通过应用到 s 来修改 State。所以让我们将其返回的新 State 同时作为纯计算和 Monad 计算的结果：

```haskell
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> Tuple (f s) (f s)
```

好吧，我在这里可能有点吹毛求疵，但我讨厌代码重复。如果你想的话可以就此打住，但我想再进一步：

```haskell
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> let ns = f s in Tuple ns ns ①
```

① ns 是我们的新 State。

注意使用 let 表达式来避免代码重复。我不确定 PureScript 编译器是否会在上一步中优化掉重复，所以稳妥的做法是一开始就不要让它出现。

现在 modify_ 应该很简单了。我们可以复制 modify 的实现，并确保将其改为返回 unit 作为纯计算结果：

```haskell
modify_ :: ∀ s. (s -> s) -> State s Unit
modify_ f = State \s -> Tuple unit (f s)
```

下面是 State 的并行计算示意图：

![](img/8c0e9b687c62642e828ccb5481e11313_744_0.png)

在图中，get 读取当前 Monad 计算的结果，并将其提供给纯计算通道。另一方面，put 接收一个值，并用它替换 Monad 计算。

## 18.22. 使用 State 作为 Monad 校验

之前我们考虑过让 Validation 成为一个 Monad，但在编写 bind 时遇到了问题。既然现在我们有了 State Monad，应该可以用它来收集错误。那么让我们来试一试。

我们将从使用 Validation 之前的那个例子开始：

```haskell
errIfMissing :: Maybe String -> String -> Either String String
errIfMissing Nothing err = Left err
errIfMissing (Just s) _ = Right s

fullName :: String -> String -> String -> String
fullName first middle last = first <> " " <> middle <> " " <> last

fullNameEither :: Maybe String -> Maybe String -> Maybe String
                -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
           <*> (middle `errIfMissing` "Middle name must exist")
           <*> (last `errIfMissing` "Last name must exist")
```

花点时间回顾一下这段代码。

如果你还记得，我们曾将 fullNameEither 重写为使用 do 记法：

```haskell
fullNameEither :: Maybe String -> Maybe String -> Maybe String
                -> Either String String
fullNameEither first middle last = do
  f <- errIfMissing first "First name must exist"
  m <- errIfMissing middle "Middle name must exist"
  l <- errIfMissing last "Last name must exist"
  pure $ fullName f m l
```

但 fullNameEither 的两个版本都会在第一个错误处停止，因为它们使用的是 Either，而 Either 会短路。这就是为什么我们要用 State 来代替 Either。

让我们重写 errIfMissing，使它使用 State 而不是 Either。我们先从它的类型签名开始：

```haskell
errIfMissing :: Maybe String -> String -> State ???
```

现在我们必须弄清楚我们需要为 State 提供哪些类型参数。让我们选择 Array String 作为我们的 State，也就是 State 类型构造器中的第一个类型参数。这样我们就可以在一个 Array 中收集错误：

```haskell
errIfMissing :: Maybe String -> String -> State (Array String) ???
```

通过查看我们的 Either 实现，可以看到它在成功时返回了一个 String。所以对于纯计算的结果类型，让我们也尝试使用 String：
