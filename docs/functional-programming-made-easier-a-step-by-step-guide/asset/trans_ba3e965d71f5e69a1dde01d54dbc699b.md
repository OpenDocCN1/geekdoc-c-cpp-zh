
我们也可以这样做，但不能选择性地将该结果赋值给变量，因为这假设了两种情况之一：要么变量已经有值，这意味着我们会在修改它；要么它没有值，因此为 NULL。

这两种情况在 PureScript 中都是不允许的。这就是为什么我们只有 if 表达式。

### 3.3.2. case 表达式

我们可以使用 case 表达式进行逻辑分支，但它仅限于模式匹配：

```haskell
data ContactMethod
  = Phone
  | Email
  | Fax

keepModern :: ContactMethod -> ContactMethod
keepModern preferredContactMethod =
  case preferredContactMethod of
    Phone -> Phone
    Email -> Email
    Fax -> Email ①
```

① 如果首选联系方式是 Fax（传真），我们将使用 Email（电子邮件）替代。

从技术上讲，我们可以使用 case 重写 keepPositive：

```haskell
keepPositive :: Int -> Int
keepPositive x = case x < 0 of
  true -> 0
  false -> x
```

虽然这在技术上是有效的，但与 if-then-else 版本相比，这个版本显得笨拙。

### 3.3.3. 模式匹配

模式匹配与使用 case 非常相似：

```haskell
data ContactMethod
  = Phone
  | Email
  | Fax

keepModern :: ContactMethod -> ContactMethod
keepModern Phone = Phone
keepModern Email = Email
keepModern Fax = Email
```

> ① 这个版本比 `case` 表达式版本稍微更容易阅读。

仅使用模式匹配是无法编写 `keepPositive` 的。我们需要一种类似于 `if` 的操作方式，而模式匹配不允许这样做。

要是还有别的办法就好了……

### 3.3.4. 守卫

守卫（Guards）是一种以简洁且可读的方式指定 `if` 逻辑的方法。初次遇到时语法有点奇怪：

```haskell
keepPositive :: Int -> Int
keepPositive x
  | x < 0      = 0
  | otherwise  = x
```

> ① 注意使用守卫时没有等号。这一点很容易忘记。

> ② 竖线 `|` 就是守卫。后面是一个布尔表达式、一个等号，以及在布尔表达式为 `true` 时该表达式的值。

> ③ 这一行表示如果 `x < 0` 为 `true`，则返回 `0`。

> ④ `otherwise` 被定义为等于 `true`，其存在只是为了更好地阅读守卫。它是兜底情况，我们直接返回 `x`。

我们也可以在 `case` 表达式中使用守卫：

```haskell
data ContactMethod
  = Phone
  | Email
  | Fax

keepModernIfYoung :: Int -> ContactMethod -> ContactMethod
keepModernIfYoung age preferredContactMethod =
  case preferredContactMethod of
    Phone -> Phone
    Email -> Email
    Fax | age < 40  -> Email ① ③
      | otherwise -> Fax ② ③
```

① 我们首先对 Fax 进行模式匹配，然后守卫开始生效。如果年龄小于 40，我们使用 Email。

② 我们的兜底情况适用于 40 岁及以上的人，我们将使用 Fax。

③ 别忘了在 case 表达式中，守卫使用的是 `->` 而不是 `=`。这一点同样容易忘记。

下面是守卫在 case 中的另一个示例：

```haskell
noBiggerThan10 :: Maybe Int -> Int
noBiggerThan10 x = case x of
  Just x | x > 10    -> 10 ①
        | otherwise -> x
  Nothing            -> 0
```

① 模式匹配在 `|` 的左侧，然后是条件，接着是箭头，最后是值。注意模式 `Just x` 中的 `x` 可以用于守卫的右侧。

守卫和模式匹配可以协同工作：

```haskell
takeWhile :: ∀ a. (a -> Boolean) -> List a -> List a ①
takeWhile p (x : xs) | p x = x : takeWhile p xs ②
takeWhile _ _ = Nil ③
```

① 接收一个谓词（Predicate）和一个列表（List），并在谓词满足时从列表头部开始取值。一旦谓词返回 false，它就停止，并返回到目前为止所取的所有元素组成的列表。

② `p x` 用谓词 `p` 检查列表头部 `x`。如果为 true，则将 `x` 添加到对 `takeWhile` 进行递归调用（使用尾部）的头部。如果为 false，由于没有兜底守卫，因此会转到另一个版本的 `takeWhile`。

③ 这个版本涵盖两种情况。首先，它是第一个带守卫版本中条件为 false 的情况。其次，它是空列表的情况，因为 `Nil` 不匹配第一个 `takeWhile` 版本的第二个参数，即 `(x : xs)`。

让我们回顾一下模式 `x : xs` 将匹配什么：

```haskell
1 : 2 : 3 : Nil    (x = 1, xs = 2 : 3 : Nil)
1 : 2 : Nil        (x = 1, xs = 2 : Nil)
1 : Nil            (x = 1, xs = Nil)
Nil                (NO MATCH)
```

> **谓词**（**Predicate**）是一个函数，它接收一个值，并根据有关该值的某种条件返回布尔值。例如，`isOdd :: Int -> Boolean` 接收一个 Int，如果它是奇数则返回 true。

## 3.4. Lambda 函数

之前，当我们稍微了解 Lambda 演算时，我们看到了 PureScript 中与 Lambda 演算函数等价的形式：

```haskell
\x -> x + 1
```

这个函数是一个匿名函数，即没有名称。我们可以通过将其命名为 `f` 来给它一个名称：

```haskell
f :: Int -> Int
f = \x -> x + 1
```

既然我们将其命名为 `f`，就没有理由再使用 Lambda。我们也可以轻松地将参数写在等号另一侧来编写 `f`：

```haskell
f :: Int -> Int
f x = x + 1
```

那么，为什么支持这种语法呢？Lambda 的真正好处是什么？

当你需要将一个函数传递给另一个函数，但它又不值得拥有一个正式名称，因为只会使用一次时，这种语法很有用：

```haskell
filter (\x -> x < 10) [1, 2, 3, 10, 20, 30] == [1, 2, 3]
```

这里 Lambda 函数是一个谓词，用于检查值是否小于 10。

`filter` 会保留 `Array` 中通过测试的所有元素。它会遍历我们的 `Array`，调用我们的 Lambda，并将 `Array` 中的元素传入；如果 Lambda 返回 `true`，则 `filter` 会保留该元素，否则它会被过滤掉。

请记住，没有变更（mutation），因此从 `filter` 返回的 `Array` 将是一个新的 `Array`。

在 Lambda 中指定多个参数与普通函数非常相似：

```haskell
\x y -> x + y
```

它是以下写法的语法糖：

```haskell
\x -> \y -> x + y
```

如果你习惯使用 JavaScript，你已经见过类似的手动编写柯里化函数的模式：

```javascript
x => y => x + y // Javascript
```

有时函数拥有的参数比类型签名中指定的要多。当你第一次遇到这种情况时可能会感到困惑，但考虑到 Lambda 会有所帮助。

为了说明这一点，让我们检查一下 `compose` 函数，通常通过其二元运算符 `<<<` 调用，它组合两个函数：

```haskell
compose :: ∀ a b c. (b -> c) -> (a -> b) -> (a -> c)
compose f g x = f (g x)
```

- 1. `compose` 接受 2 个参数，都是函数，并返回一个函数。
- 2. 我们在这里指定了 3 个参数。怎么回事？
- 3. `f (g x)` 的类型是 `c`，与类型签名中的返回值不匹配。这是怎么回事？

事实证明，这个函数等价于用 Lambda 编写：

```haskell
compose :: ∀ a b c. (b -> c) -> (a -> b) -> (a -> c)
compose f g = \x -> f (g x)
```

- 1. 现在它只接受 2 个参数。
- 2. 现在它返回一个从 `a` 到 `c` 的函数。等号右侧的 Lambda 接受一个类型为 `a` 的 `x`，并返回类型为 `c` 的 `f (g x)`。

## 3.5. 通配符

到目前为止，我们已经看到 `_` 被用作“不关心”变量。有时它也用作通配符。

### 3.5.1. case 表达式

```haskell
data ContactMethod
  = Phone
  | Email
  | Fax

-- verbose version

keepModernIfYoung :: Int -> ContactMethod -> ContactMethod
keepModernIfYoung age preferredContactMethod =
  case preferredContactMethod of ①
    Phone -> Phone
    Email -> Email
    Fax | age < 40  -> Email
        | otherwise -> Fax

-- simpler with a wildcard

keepModernIfYoung' :: Int -> ContactMethod -> ContactMethod
keepModernIfYoung' age = case _ of ②
  Phone -> Phone
  Email -> Email
  Fax | age < 40  -> Email
      | otherwise -> Fax
```

① 注意，我们必须为一个参数提供名称，该参数会立即在 case 表达式中使用，之后不会再使用。

② 这里我们以 Point-free 风格编写该函数。这允许 `_` 代表第二个参数。它仍然是一个“不关心”变量，因为我们没有命名它，但作为通配符，我们实际上使用了这个值。

以下两行代码是等价的：
