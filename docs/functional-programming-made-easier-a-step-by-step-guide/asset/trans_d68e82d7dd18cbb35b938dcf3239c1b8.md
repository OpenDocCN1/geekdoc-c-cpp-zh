

```
errIfMissing :: Maybe String -> String -> State (Array String) String
errIfMissing Nothing err = do
  modify_ (_ <> [err])
  pure mempty
errIfMissing (Just s) _ = ???
```

我们需要做的就是返回我们得到的 String，因为这不是错误情况：

```
errIfMissing :: Maybe String -> String -> State (Array String) String
errIfMissing Nothing err = do
  modify_ (_ <> [err])
  pure mempty
errIfMissing (Just s) _ = pure s ①
```

① 再次，我们把那个 String 放在一个 Context 中，即 State。

现在我们要做的就是修改 fullNameEither。首先，我们会改它的名字，因为它会返回 State。其次，我们会把它的返回类型改成与 errIfMissing 的返回类型相匹配：

```
fullNameValid :: Maybe String -> Maybe String -> Maybe String ①
               -> State (Array String) String ②
fullNameValid first middle last = do
  f <- errIfMissing first "First name must exist"
  m <- errIfMissing middle "Middle name must exist"
  l <- errIfMissing last "Last name must exist"
  pure $ fullName f m l
```

① 名称已更改。

② 返回的是 State 而不是 Either。

很不错，我们在更改 Monad 时，即从 Either 改到 State，几乎没有需要修改 fullNameValid 的地方。

现在，如果我们要测试这段代码，可以写类似这样的内容：

```
test :: Effect Unit
test = do ①
  log $ show $ runState (fullNameValid Nothing (Just "") Nothing) []
```

① 这个 do 是不必要的，因为 do 块里只有 1 行代码。可以安全地移除它。在 Haskell 中，linter 会抱怨这种冗余。在 PureScript 中不会。那是你的工作。

运行这个测试会显示：

```
(Tuple "" ["First name must exist","Last name must exist"])
```

注意这个 Tuple 同时包含了 纯计算，即 ""，和 Monad 计算，即 ["First name must exist","Last name must exist"]。

如果我们要使用这种方法，我们希望检查 Monad 计算，即最终的 State，不是 []。这会表明存在错误。

现在我们把这个改写为使用 State 而不是 Validation，就很清楚我们其实并不需要 State。如果我们查看 errIfMissing，应该能看出它只是使用 Semigroup 进行追加：

```
errIfMissing :: Maybe String -> String -> State (Array String) String
errIfMissing Nothing err = do
  modify_ (_ <> [err]) ①
  pure mempty
errIfMissing (Just s) _ = pure s
```

① 这里调用了 append。

但这正是 Writer 所做的。这意味着我们可以用 Writer 重写它？

让我们先通过把 State 改成 Writer 来重写 errIfMissing 的定义：

```
errIfMissing :: Maybe String -> String -> Writer (Array String) String
```

现在是 Nothing 情况：

```
errIfMissing :: Maybe String -> String -> Writer (Array String) String
errIfMissing Nothing err = do
  tell [err]
  pure mempty
```

这里唯一需要改动的是调用 tell 而不是 modify_。我们完全不需要改动 pure mempty，这要归功于 Typeclass 的工作方式。现在使用的 pure 是 Writer 的而不是 State 的。编译器会为我们处理好。

现在是 Just 情况：

```
errIfMissing :: Maybe String -> String -> Writer (Array String) String
errIfMissing Nothing err = do
  tell [err]
  pure mempty
errIfMissing (Just s) _ = pure s
```

成功的情况完全没有变化，因为编译器会使用 Writer 的 pure 而不是 State 的。

现在，我们要做的就是更改 fullNameValid 上的类型签名。由于 State 和 Writer 都是 Monad，我们 do 块里的所有代码都不需要改动。这是因为编译器会使用 Writer 的方法，即 bind 和 pure，而不是 State 的方法：

```
fullNameValid :: Maybe String -> Maybe String -> Maybe String
            -> Writer (Array String) String ①
fullNameValid first middle last = do
  f <- errIfMissing first "First name must exist"
  m <- errIfMissing middle "Middle name must exist"
  l <- errIfMissing last "Last name must exist"
  pure $ fullName f m l
```

① State 改为 Writer。

这个实现同样有效。我们剩下的唯一工作就是修改我们的测试代码，即把 runState 改成 runWriter：

```
test :: Effect Unit
test = do
  log $ show $ runWriter
    (fullNameValid Nothing (Just "") Nothing) [] -- COMPILER ERROR!!
```

哦不。我们从未写过 runWriter。让我们用 runState 作为模板快速写一个：

```
runState :: ∀ a s. State s a -> (s -> Tuple a s)
runState (State f) = f
```

让我们把 State 改成 Writer，并把 s 改成 w 以匹配 Writer 的类型定义：

```
runWriter :: ∀ a w. Writer w a -> (w -> Tuple a w)
runWriter (Writer f) = f -- COMPILER ERROR!!
```

当然，编译器报错：

![](img/8c0e9b687c62642e828ccb5481e11313_750_0.png)

这告诉我们编译器遇到了一个 Tuple 但期望一个函数。当这种情况发生时，我首先会问自己 State 和 Writer 有什么不同，因为我只是复制粘贴了那段代码。

而不同之处在于 Writer 包含一个 Tuple，而 State 包含一个返回 Tuple 的函数。让我们修复它：

```
runWriter :: ∀ a w. Writer w a -> Tuple a w ①
runWriter (Writer x) = x ②
```

① 把 (w -> Tuple a w) 改为 Tuple a w。

② 把 f 重命名为 x，以反映 Writer 包含一个值而不是像 State 那样的函数。

现在我们在测试代码的这一行会得到编译器错误：

```
test :: Effect Unit
test = do
  log $ show $ runWriter
    (fullNameValid Nothing (Just "") Nothing) [] -- COMPILER ERROR!!
```

这里的编译器错误是：

```
Could not match type
Tuple
with type
Function

while applying a function runWriter (((fullNameValid' Nothing) (Just "")) Nothing)
of type Tuple t0 t1
to argument []
while inferring the type of (runWriter (((...) (...) ) Nothing)) []
in value declaration test
log $ show $ runWriter (fullNameValid' Nothing (Just "") Nothing) []
```

不确定这个错误信息是否很有帮助，但这又是从 State 的测试代码复制过来的。所以，再次，我问，State 和 Writer 有什么不同。

嗯，这里最重要的区别是 State 需要一个初始状态，这就是为什么我们把 [] 传入 runState 的原因。Writer 以 mempty 作为其初始值开始。所以不需要传入 []，而 [] 恰好是 Array a 的 mempty 值。

另一种看待方式是比较它们的类型签名。runState 接受 2 个参数，而 runWriter 只接受 1 个。无论哪种方式，我们都需要移除 [] 参数：

```
test :: Effect Unit
test = do log $ show $ runWriter (fullNameValid Nothing (Just "") Nothing)
```

现在我们可以运行这段代码，它会打印：

```
(Tuple "" ["First name must exist","Last name must exist"])
```

这个输出与我们的 State 实现完全相同，而且更优越，因为 Writer 更简单。

但退一步看大局，很明显使用 Writer 相比 Validation 并没有带来任何优势。除非出于某种奇怪的原因，我们需要使用 Monad。在那种罕见的情况下，我们现在知道怎么做了。但在实践中，Validation 应该更可取。

一般来说，我建议在求助于 Monad 之前先从 Applicative 开始，原因与我们之前更倾向于 Writer 而不是 State 相同。那就是简单性。最好使用能完成工作的最简单的工具。

## 18.23. Kleisli 范畴

我们之前谈到过 Kleisli 组合和 Kleisli 范畴。我们看到 Kleisli 组合如何组合 Monad 函数，即形如 a -> m b 的函数：

```
composeKleisli
  :: ∀ a b c m
    . Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f x = f x >>= g

infixr 5 composeKleisli as >>= 
```

Monad 函数与纯函数的区别可以通过比较 composeKleisli 与纯函数组合 compose 来看出。当关注 Semigroupoid 的函数实例实现时尤其明显：

```
class Semigroupoid a where
  compose :: ∀ b c d. a c d -> a b c -> a b d

infixr 9 compose as <<< 

instance semigroupoidFn :: Semigroupoid (->) where
  compose :: ∀ b c d. (c -> d) -> (b -> c) -> (b -> d)
  compose f g x = f (g x)
```

我们还谈到 Semigroupoid 就像一个范畴，但没有 Identity 要求。

PureScript 中有一个 Typeclass 叫做 Category。它通过为 Semigroupoid 添加 Identity 定律来建模范畴论中的范畴：

```
class Semigroupoid a <= Category a where
  identity :: ∀ t. t -> t
```

记住，一个范畴有对象和对象之间的态射。在 Hask 范畴中，对象是类型，态射是函数。

在 Kleisli 范畴中，对象也是类型，但态射是 Monad 函数，即类型为 a -> m b 的函数。

首先，让我们看一下 Hask：

