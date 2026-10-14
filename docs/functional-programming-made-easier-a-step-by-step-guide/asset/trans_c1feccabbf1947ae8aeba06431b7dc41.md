
```
optional :: ∀ e a. a -> Parser e a -> Parser e a
```

我们有一个 Parser 和一个值。我们可以使用 `pure` 为默认的 Parser 将该值包装在一个 Parser 中。

这将给我们两个 Parser：原始的那个，以及一个总是返回我们默认值的 Parser。如果第一个失败，我们就想用第二个来解析。

你还记得我们是如何基于失败来选择两个 Parser 的结果的吗？看看我们为 `alphaNum` 写的内容，然后继续之前完成 `optional` 的编写。

下面是实现：

```
optional :: ∀ e a. a -> Parser e a -> Parser e a
optional x p = p <|> pure x
```

我们正在使用 `Alt`，如果你还记得的话，它会先尝试第一个 Parser，如果失败，再尝试第二个。嗯，这里的第二个 Parser 永远不会失败，这正是我们在 `atMost` 中想要发生的。

回到 `atMost`，使用 `optional` 让我们的 Parser 永不失败。然后继续阅读，看看你做得怎么样。

让我们看看 `atMost` 的有缺陷的版本：

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0      = pure []
  | otherwise = p >>= \c -> (c : _) <$> atMost (n - 1) p
```

我们可以看到，在错误情况下，我们返回一个总是返回 `[]` 的 Parser。而在 `otherwise` 情况下，我们返回一个 Parser：`p >>= \c -> (c : _) <$> atMost (n - 1) p`。如果那个庞大的 Parser 失败了，我们希望返回一个总是返回 `[]` 的 Parser，这正是 `optional` 会为我们做的。

所以我们只需将 `p >>= \c -> (c : _) <$> atMost (n - 1) p` 传给 `optional`：

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0      = pure []
  | otherwise = optional [] $ p >>= \c -> (c : _) <$> atMost (n - 1) p
```

这段代码看起来相当吓人。所以，让我们写一些好的测试，以确保我们没有自欺欺人地以为自己知道自己在做什么。

我们需要测试边界条件。一共有 3 个。一，当我们传入的计数为 0 或更少时。二，当我们无法解析任何内容时。三，当我们本可以解析更多，但因为达到最大值而停止时。

在编写这些测试之前，让我们编写一个名为 `atMost'` 的 `atMost` 版本，它返回 `Parser e String`。看看 `count'` 是怎么做的。在继续阅读之前，先编写那个函数。

下面是那个函数：

```
atMost' :: ∀ e. Int -> Parser e Char -> Parser e String
atMost' n p = fromCharArray <$> atMost n p
```

我们之所以把 `Parser` 写成 `Parser e a`，是为了获得最大的灵活性。我们可能想在非文本场景中使用我们的 `Parser`。但一般来说，我们主要会将它用于 `String`，这就是为什么我们要编写带撇号的版本，例如 `atMost'`。

现在将以下内容添加到你的测试代码中并运行，以确保 `atMost'` 正常工作：

```
log $ show $ parse' (atMost' (-2) alphaNum) "a1b2c3" ❶
log $ show $ parse' (atMost' 2 alphaNum) "$_$" ❷
log $ show $ parse' (atMost' 2 alphaNum) "a1b2c3" ❸
```

+   ❶ 打印 `(Right (Tuple "a1b2c3" ""))`。
+   
+   ❷ 打印 `(Right (Tuple "$_$" ""))`。
+   
+   ❸ 打印 `(Right (Tuple "b2c3" "a1"))`。

如果打印结果符合我们的预期，那么我们就可以继续学习 `range` 了。

但是……在此之前，我们答应过自己稍后要泛化 `atMost`。我们很容易看着它，然后觉得它现在这样就可以了，因为一开始写它就很难。如果你现在也有这种感觉，也许是个好时机休息一下，等你准备好了再回来。

我认为，让任何库函数都尽可能灵活是值得的。而且，`atMost` 显然是一个通用的 `Parser`。所以值得从这个角度来审视它。

这是我们当前的版本：

```
atMost :: ∀ e a. Int -> Parser e a -> Parser e (Array a)
atMost n p
  | n <= 0    = pure []
  | otherwise = optional [] $ p >>= \c -> (c : _) <$> atMost (n - 1) p
```

我们可以像在 `count` 中那样把 `Array` 改成 `Unfoldable`。那效果很好。所以，复制这个函数，并注释掉其中一个副本。我们会保留它，以防我们的实验出问题。

接下来，修改类型签名，将 `Array` 替换为 `Unfoldable`。看看 `count` 的类型签名，从中寻找如何做到这一点的线索。

在回到这里之前先完成这一步。顺便说一句，我们应该预料到会出现编译器错误。

下面是类型签名的修改：

```
atMost :: ∀ e a f. Unfoldable f => Int -> Parser e a -> Parser e (f a)
atMost n p
  | n <= 0      = pure []   -- COMPILER ERROR!!
  | otherwise = optional [] $ p >>= \c -> (c : _) <*> atMost (n - 1) p
```

下面是错误信息：

![](img/8c0e9b687c62642e828ccb5481e11313_806_0.png)

编译器发现了一个 `Array`，但期望的是类型 `f1`，也就是我们的 `f`，它是一个 `Unfoldable`。如果你还记得，我们在泛化 `count` 时见过这种情况。

有一个名为 `none` 的 `Unfoldable` 辅助函数。它使用 `Unfoldable` 的 Generating 函数来生成 0 个元素。对于 `Array`，它会返回 `[]`。对于 `List`，它会返回 `Nil`。依此类推。

所以，把 `[]` 替换为 `none`，看看它能否编译。确保在两处都把 `[]` 改为 `none`。

当然不能。下面是新代码：

```
atMost :: ∀ e a f. Unfoldable f => Int -> Parser e a -> Parser e (f a)
atMost n p
  | n <= 0      = pure none
  | otherwise = optional none $ p >>= \c -> (c : _) <*> atMost (n - 1) p
    -- COMPILER ERROR!!
```

下面是新的编译器抱怨：

![](img/8c0e9b687c62642e828ccb5481e11313_807_0.png)

它又一次抱怨说，发现了一个 `Array`，但期望的是 `f1`，也就是 `Unfoldable`。但我们不再显式地使用 `Array` 了。所以这意味着我们一定是在隐式地使用它。

我们一定是在调用一个期望 `Array` 的函数。你能看出这发生在哪里吗？

如果你说是 Cons 运算符 `:`，那你就说对了。我们之前在 `atMost` 中第一次使用它时导入了那个运算符。我们不能再使用它了，因为我们不知道我们处理的是不是 `Array`。我们还希望能够处理 `List` 或任何其他 `Unfoldable`。

我们如何解决这个难题？我们需要一个类似 Cons 但适用于任何 `Unfoldable` 的函数。PureScript 中有这样的函数吗？

如果你在 Pursuit 中仔细搜寻这样的东西，你很可能会一无所获。我就是这样。但并非全无希望。我们可以向 `atMost` 传入一个类似 cons 的函数。然后，当我们处理 `Array` 时，就传入 `Data.Array` 中的 `:`；当我们处理 `List` 时，就传入 `Data.List` 中的 `:`，等等。

所以，修改 `atMost` 的类型签名，让它接受一个类似 cons 的函数作为第一个参数。如果你不知道类似 cons 的函数的类型签名应该是什么，可以看看 `Array` 或 `List` 的 `Cons` 的类型签名，然后将其泛化。

然后添加一个名为 `cons` 的新第一个参数，并用那个变量替换 `:`。

做出这些修改，然后继续。

以下是这些修改：

```
atMost
  :: ∀ e a f
  .  Unfoldable f
  => (a -> f a -> f a)
  -> Int
  -> Parser e a
  -> Parser e (f a)
atMost cons n p
  | n <= 0    = pure none
  | otherwise = optional none $ p
                         >>> \\c -> cons c <$> atMost cons (n - 1) p
```

① 这个类似 cons 的函数接受一个 `a` 和一个由 `a` 组成的 `Unfoldable`，并返回一个由 `a` 组成的 `Unfoldable`。重读上一句话，把“类似 cons”替换为“cons”，把“Unfoldable”替换为“Array”或“List”，它依然成立。

② 我们把 `cons` 参数添加为第一个参数。把它放在第一位，这样我们可以轻松地部分应用它。

③ `(c : _)` 已被替换为 `cons c`，它是 `:` 的前缀等价形式。

④ 我们必须把 `cons` 传给递归调用。这很容易遗漏，但幸运的是，编译器会在那里提醒我们。

所以，现在 `atMost` 将解析 0 次或 n 次，但不会更多。稍后，我们将看到如何解析 0 次或更多次，以及 1 次或更多次。

但是我们在 `atMost'` 上遇到了错误。这并不奇怪，因为我们给 `atMost` 增加了一个额外的参数。所以，在继续阅读之前，先去修复它。

我们只需要在调用 `atMost` 时使用 `(:)` 作为我们的类似 cons 的函数：

```
atMost' :: ∀ e a. Int -> Parser e Char -> Parser e String
atMost' n p = fromCharArray <$> atMost (:) n p
```

① 我们在这里传递的是 `Data.Array` 中的 `:`。这不是 `Data.List` 中的同一个运算符。

现在我们准备好看看我们的代码是否正常工作了。运行程序会显示错误：

```
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- arrays
```

将 `arrays` 添加到 `spago.dhall` 中，然后重新运行程序，并验证测试代码的最后 3 行是否正常工作：
