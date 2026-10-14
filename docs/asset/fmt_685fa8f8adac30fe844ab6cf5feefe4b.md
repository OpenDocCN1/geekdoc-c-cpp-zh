
we see that we have a `Foldable` of `String`. So this `Type Parameter` is `String`, to indicate we have `String` Elements:

```
sizer :: Moore Int String ?
```

The final `?` is the `Output Type`. We know by looking at the expected output of our test code, `"Size is 13"`, that this is also a `String`.

```
sizer :: Moore Int String String
```

Now that we have the `Type Signature` figured out, go ahead and write the `sizer` function remembering the important fact that we’re going to do some sort of mapping over the `addr`.

So we’re going to need to map `addr` to `sizer`:

```
s   a   b
Moore a a a ---> Moore Int String String
```

We know that `a` unifies with `Int` giving us:

```
s   a   b       s   a   b
Moore Int Int Int ---> Moore Int String String
```

This tells us we need to map `addr`’s `Output`, which is an `Int`, to `sizer`’s `Output`, which is a `String`.

This also tells us that we need to map `sizer`’s `Element`, which is an `String`, to `addr`’s `Element`, which is an `Int`. Notice how the previous sentence is BACKWARDS from the one before it. That’s because this is mapping an INPUT `Contravariant`. We want to leverage `addr`, so we have to map from `String` to `Int` before we can safely call `addr`.

We have specified 2 mappings. The second specification is `Contrvariant`. Does that sound familiar?

If it doesn’t, it should. It’s our old friend `Profunctor`.

Use this new perspective to finish writing the function before reading on.

## 15.19. Code for sizer

Starting with the `Type Signature` from the Hint section:

```
sizer :: Moore Int String String
```

We know we're going to use `dimap` over `addr`, which will do the summing for us:

```
import Data.Profunctor (class Profunctor, dimap) ①

sizer :: Moore Int String String
sizer = dimap ??? ??? addr
```

① Added `dimap` to the import list.

Now all we have to do is figure out what our mapping functions are.

Let's look back at the `dimap` `Type Signature`:

```
class Profunctor p where
  dimap :: ∀ a b c d. (b -> a) -> (c -> d) -> p a c -> p b d
```

We can see that the first `Function` is the `Contravariant` function. We can use it to map the `Element` `see Hint section`.

Let's do that. So, how do we map `String` to `Int`? Lots of ways, but `sizer` is for adding up LENGTHS of `Strings`. So we'll use the function, `length :: String -> Int`, to do that mapping:

```
import Data.String (length) ①

sizer :: Moore Int String String
sizer = dimap length ??? addr ②
```

① Added this import.

② Convert `String` elements that `sizer` expects into `Int` elements that `addr` expects.

Now looking back at `dimap`, we can see that the second `Function` is `Covariant`, i.e. maps OUTPUTS. This is what we'll use to map `addr`'s `Output`, the sum total, from `Int` to `String`.

But how to do that?

Let's look back at the our test code:

```
log $ show $ runFoldL sizer [ "This", "is", "the", "test" ] ①
```

① Prints `"Size is 13"`.

From the annotation, we can see that we need a function that takes the result of adding up all the lengths, which is an `Int`, and displays a message like, `"Size is 13"`. So let’s add such a function:

```
sizer :: Moore Int String String
sizer = dimap length (\n -> "Size is " <> show n) addr ①
```

① We use `show` to convert the `Int`, `n`, to a `String`.

Test out your code to see if it works.

We have now successfully leveraged `addr` to create `sizer` using `Profunctor`’s `dimap`.

## 15.20. Power of the Functor

`Functors` of `Functions` let us leverage existing functions to create new ones. With `Profunctors`, specifically `Moore`, we were able to map INPUTS and OUTPUTS to leverage the existing function `addr` to produce `sizer`.

If we didn’t have this power, we’d have to write:

```
log $ show $ (\n -> "Size is " <> show n) $
  runFoldL addr (length <$> [ "This", "is", "the", "test" ]) ②
```

① We take the result of running the `Fold` and convert it to a `String`. This is analogous to mapping OUTPUTS.

② We use `Functor` to map `length` over the `List` of `Strings`. This is analogous to mapping the INPUTS.

instead of:

```
log $ show $ runFoldL sizer [ "This", "is", "the", "test" ]
```

And we’d have to do this extra work every single time we wanted to leverage `addr`.

With the power of `Functors`, and in particular `Profunctors`, we can make our lives so much easier by both leveraging existing functions and by making the use of those new functions easy.

# 第三部分：高级

# 第16章。应用函子、遍历子和替代子

到目前为止，我们已经见过几种函子的变体来执行以下操作：

+   将函数映射到处于上下文中的值上（函子、双函子）
+   将函数映射到处于上下文中的另一个函数上（函子、反变、协变、余函子）

在两种情况下，我们都有上下文外部的函数，应用于上下文内部的值或函数。

我们尚未检查的唯一情况是值在外部而函数在内部。这看起来如何？

让我们从上下文中的一个函数开始：

```
Just (_ * 10) :: Maybe (Int -> Int)
```

现在，我们想取某个值，比如 20 并将其应用于此函数，并将结果放入我们的上下文中，这里是 `Maybe`。我们可以写：

```
(\f -> f 20) <$> Just (_ * 10) :: Maybe Int
```

这里我们的 `Lambda` 表达式将被应用于上下文中的“值”，它恰好是一个函数。然后 `f` 将被绑定到 `(_ * 10)`，然后 20 将被应用于它。

看起来我们已经可以用函子做到这一点。但如果我们有 `Just 20` 而不是 20 会怎样？

让我们尝试类似的方法：

```
(\f -> f <$> Just 20) <$> Just (_ * 10) :: Maybe (Maybe Int) ①
```

① 呃。不是我们希望的结果。

我们在这里映射了两次。第一次是在将 `f` 应用于 `Just 20` 时，然后我们将整个 `Lambda` 应用于 `Just (_ * 10)`。这就是为什么我们得到一个 `Maybe` 在另一个 `Maybe` 中的原因。

所以映射并不是一个很好的解决方案。

另一种可能性是为 `Maybe` 编写一个特殊函数：

```
applyToMaybe :: ∀ a b. Maybe (a -> b) -> Maybe a -> Maybe b
applyToMaybe Nothing _ = Nothing
applyToMaybe (Just f) x = f <$> x
```

这可行，但当 `Either` 是我们的上下文时，我们也必须为它编写一个特别命名的函数。我们以前见过这种模式，最好用类型类来处理。

`PureScript` 正好有这个类型类，叫做 `Apply`：

```
class Functor f <= Apply f where
  apply :: ∀ a b. f (a -> b) -> f a -> f b ①

infixl 4 apply as <*> ②
```

① 将上下文中的函数 `f (a -> b)` 应用于上下文中的值 `f a`。

② `apply` 二元运算符别名 `<*>` 是中缀且左结合的。

注意 `Apply` 是一个函子。

事实证明 `Maybe` 有一个 `Apply` 实例。所以，我们可以重写我们之前需要映射两次的代码来使用 `apply` 代替：

```
Just (_ * 10) <*> Just 20 :: Maybe Int ① ②
```

① 现在我们只有一个 `Maybe`。

② 结果为 `Just 200`

让我们看看另一种使用 `apply` 的运算符别名 `<*>` 的方法：

```
data Tuple a b = Tuple a b

x :: ∀ a b. Maybe a -> Maybe b -> Maybe (Tuple a b)
x ma mb = Tuple <$> ma <*> mb ①
```

① 哇？第一次看到这个时，我很困惑。别担心，我们会慢慢讲解。

所以让我们一步一步来。

首先，`ma` 是一个 `Maybe a`。这意味着我们可以将数据构造器 `Tuple` 映射到它上面：

```
ma :: Maybe a
Tuple <$> ma :: Maybe (b -> Tuple a b) ①
```

① 我们只部分应用了 `Tuple`。它期望 2 个参数但我们只给了它 1 个。

我们现在处于之前谈到的情况。我们有一个函数 `b -> Tuple a b` 在上下文 `Maybe` 中，我们想将 `mb` 应用于它。认识到 `mb` 只是同一个上下文中的 `b`。

现在我们可以使用 `apply`：

```
ma :: Maybe a
Tuple <$> ma :: Maybe (b -> Tuple a b)
mb :: Maybe b
Tuple <$> ma <*> mb :: Maybe (Tuple a b) ①
```

① 这次我们使用的是 `<*>` 而不是 `<$>`，所以我们不会得到一个 `Maybe` 包裹在另一个 `Maybe` 中。

这是一个使用 `apply` 的常见示例。首先，我们用 `<$>` 映射第一个参数，然后所有剩余的参数都使用 `<*>` 应用。

这里是另一个使用我们老朋友 `Threeple` 的示例：

```
data Threeple a b c = Threeple a b c

threeple :: ∀ a b c. Maybe a -> Maybe b -> Maybe c -> Maybe (Threeple a b c)
threeple mx my mz = Threeple <$> mx <*> my <*> mz ①
```

① 一旦我们有了上下文中的函数，即 `Maybe`，我们就可以开始使用 `<*>`。

如果 `Threeple` 已经在上下文中，即 `Maybe Threeple` 那么我们就可以立即使用 `<*>`：

```
data Threeple a b c = Threeple a b c

threeple :: ∀ a b c. Maybe a -> Maybe b -> Maybe c -> Maybe (Threeple a b c)
threeple mx my mz = Just Threeple <*> mx <*> my <*> mz ①
```

① 我们不使用 `<$>` 因为我们的函数 `Threeple`，即数据构造器，已经在上下文中。

将此版本与前一个版本进行比较。区别很微妙。

现在让我们取 `threeple` 的最后一个版本并使上下文成为一个参数，即让我们将其泛化：

```
data Threeple a b c = Threeple a b c

threeple :: ∀ a b c f. f a -> f b -> f c -> f (Threeple a b c) ①
threeple mx my mz = ??? Threeple <$> mx <$> my <$> mz ②
```

① 我们用类型参数 `f` 替换了 `Maybe`。

② `???` 是类型 `f` 的数据构造器所在的位置。

问题在于我们不知道如何将 `Threeple` 包装在上下文 `f` 中。我们知道 `f`，但 `f` 是一个类型而不是数据构造器。我们需要一个数据构造器，例如 `Just`，来包装 `Threeple`，但我们所知道的只是类型，例如 `Maybe`。

而再次，不在事先知道类型的情况下做到这一点的方法是使用类型类。

事实证明，我们可以使用 `PureScript` 中的 `Applicative` 类型类来实现这一点：

```
class Apply f <= Applicative f where
  pure :: ∀ a. a -> f a
```

这里 `pure` 接收一个纯值并将其包装到上下文中。注意 `Applicative` 是一个 `Apply`，这意味着它也是一个函子。

现在，让我们完成 `threeple` 的编写：

```
data Threeple a b c = Threeple a b c

threeple :: ∀ a b c f. Applicative f => ①
  f a -> f b -> f c -> f (Threeple a b c)
threeple mx my mz = pure Threeple <$> mx <$> my <$> mz ②
```

① 我们将 `f` 约束为 `Applicative`。

② 我们用 `pure` 替换了之前的 `???`。

所以只要 `f` 是 `Applicative`，我们就可以通过使用 `pure` 将其包装在上下文 `f` 中，然后使用 `apply` 或其二元运算符 `<$>`。

## 16.1. Haskell 中的 Applicative

在 `Haskell` 中，`Applicative` 定义为：

```
-- HASKELL Applicative
class Functor f => Applicative f where ①
  pure :: a -> f a ②
  (<*>) :: f (a -> b) -> f a -> f b ③
```

① 在 `Haskell` 中，类上的约束与函数上的约束使用相同的向前箭头。
