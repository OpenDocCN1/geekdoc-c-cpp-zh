

同一个变量名后面加上一个 s，即 xs，用来表示尾部。

你可以把 head 想象成单个的 x，把 tail 想象成 x 的复数形式，即 xs。

让我们看看如何将 Cons 与模式匹配一起使用：

```
head :: ∀ a. List a -> Maybe a
head Nil        = Nothing
head (Cons x _) = Just x ①

tail :: ∀ a. List a -> Maybe (List a)
tail Nil        = Nothing
tail (Cons _ xs) = Just xs ②
```

① 我们就像匹配任何其他带有两个参数的数据构造器一样进行匹配。这里第一个参数 x 就是头部。

② 这里 Cons 的第二个参数 xs 就是尾部。

花点时间将其与使用运算符的 head 和 tail 进行比较。就个人而言，我更喜欢运算符版本。事实证明，你会更频繁地使用运算符来做模式匹配，而不是 Cons。

## 3.2.5. 数组与列表的对比

对数组进行模式匹配时，需要知道它的确切大小。同时，你还得一次性处理数组的所有部分：

```
addThree :: Array Int -> Maybe Int
addThree [x, y, z] = Just (x + y + z)
addThree _        = Nothing
```

对于列表，我们可以编写能够处理任意长度列表的函数，而且在这种情况下，我们只需处理头部，然后通过递归继续处理列表的尾部：

```
sum :: List Int -> Int
sum Nil      = 0 ①
sum (x : xs) = x + sum xs ②
```

① 这个模式匹配匹配空列表，其长度为零。

② 我们通过模式匹配提取头部和尾部。然后把头部 x 与尾部的总和 sum xs 相加。

这个函数是递归的，但如果你不太擅长递归也不用担心。在接下来的章节中，我们会编写许多递归函数，它会变得越来越容易。

这里的关键点是，对于列表，我们不需要知道列表的大小，也不必像处理数组那样一次性处理列表中的所有元素。

数组在模式匹配上的限制意味着，无法使用模式匹配来为数组编写 sum 函数：

```
sum :: Array Int -> Int
sum ???? -- 这里无法写出一个模式
```

我们无法匹配任意大小的数组。这个问题有许多其他解决方案，其中之一是改用列表，或者将数组转换为列表，然后使用列表模式匹配。

稍后，当我们学习 Fold（折叠）时，我们会看到对数组求和的最佳解决方案。

## 3.2.6. 记录模式

让我们从下面这些记录开始：

```
type Address =
  { street :: String
  , city :: String
  , state :: String
  , zip :: Int
  }

type Employee =
  { name :: String
  , jobTitle :: String
  , yearsAtCompany :: Int
  , address :: Address
  }

type Company =
  { name :: String
  , yearsInBusiness :: Int
  , address :: Address
  }
```

现在，让我们看看编写一个函数来检查员工是否为 CEO 的各种不同方式。首先，最直接的方式：

```
isCEO :: Employee -> Boolean
isCEO employee = if employee.jobTitle == "CEO" then true else false ①
```

① 访问 Employee 记录的字段使用 employee.jobTitle。

PureScript 中访问记录的语法使用点表示法，这与你在许多其他语言（例如 JavaScript）中看到的相同。但与 JavaScript 不同的是，你不能在运行时创建访问器。

我们继续，移除多余的 if 表达式：

```
isCEO :: Employee -> Boolean
isCEO employee = employee.jobTitle == "CEO"
```

现在让我们用模式匹配来写：

```
isCEO :: Employee -> Boolean
isCEO { jobTitle } = jobTitle == "CEO" ①
```

① { jobTitle } 模式匹配 jobTitle 字段，并将其绑定到同名的局部变量。

当我们使用 { jobTitle } 时，这被称为记录简写（Record Pun）。

由于我们只关心 Employee 记录中的 jobTitle，所以我们只指定了它。我们本可以指定该记录中的其他字段：

```
isCEOAndGates :: Employee -> Boolean
isCEOAndGates { name, jobTitle } = jobTitle == "CEO" && name == "Bill Gates"
```

让我们编写一个函数来检查公司是否在加利福尼亚州：

```
isCalifornia :: Company -> Boolean
isCalifornia { address: { state } } = state == "CA" ①
```

① 这就是如何对嵌套记录进行模式匹配。address 的类型是 Address，而 Address 是一个记录。不要漏掉 address 后面的冒号，这点很容易忘记。

如果我们想要函数同时检查公司和员工的所在州，会发生什么：

```
isCompanyCalifornia :: Company -> Boolean
isCompanyCalifornia { address: { state } } = state == "CA"

isEmployeeCalifornia :: Employee -> Boolean
isEmployeeCalifornia { address: { state } } = state == "CA"
```

这两个函数几乎一模一样。想象一下，我们还有其他带有 Address 字段的记录，也想检查它们所在的州。我们不得不一遍又一遍地重复这种样板代码。

有一种更通用的方式来编写这两个函数：

```
isCalifornia :: ∀ r. { address :: Address | r } -> Boolean ① ②
isCalifornia { address: { state } } = state == "CA"
```

① 我们必须记得定义 ∀ r。别忘了变量定义后面的点号。

② 类型 { address :: Address | r } 表示我们有一个记录，其中至少有一个名为 address 的字段，其类型为 Address。| r 表示可能还有其他字段，但我们不关心它们是什么。

这个定义的妙处在于，即使 Company 和 Employee 的其他字段不同，它也能同时匹配两者。那些其他字段由 r 表示，由于这个定义适用于所有 r，即 ∀ r，因此它能匹配任何字段集合。

r 的技术术语是行类型。后面会详细讨论。

在对记录进行模式匹配时，还有一件重要的事情可以做，那就是重命名字段参数：

```
isCalifornia :: ∀ r. { address :: Address | r } -> Boolean
isCalifornia { address: { state: s } } = s == "CA"
```

重命名在字段名与作用域中的其他变量冲突时很有用，例如与同一模块中的函数名冲突。

在我们的例子中，可以想象我们重命名字段变量是因为在 isCalifornia 函数所在的模块中有一个名为 state 的函数。

我们还可以将记录中的字段匹配到特定值：

```
isCalifornia :: ∀ r. { address :: Address | r } -> Boolean
isCalifornia { address: { state: "CA" } } = true ①
isCalifornia _ = false ② ③
```

① 模式匹配 `state` 等于 "CA"。
② 使用这种方法，我们不得不提供同一函数的其他版本。在这种特定情况下，这种方式更加冗长。
③ 我们的兜底情况总是 `false`。

## 3.3. 逻辑控制

在 PureScript 中，只有少数几种方式进行逻辑决策：

- `if-then-else` 表达式
- `case` 表达式
- 模式匹配
- 守卫

### 3.3.1. If-Then-Else 表达式

注意，我在描述 `if-then-else` 时使用了“表达式”这个词。因为它不像许多语言中那样是语句。一个 `if` 必须始终有 `else` 部分。要理解原因，让我们看一个简单的例子：

```
keepPositive :: Int -> Int
keepPositive x = if x < 0 then 0 else x ①
```

① 如果 x 为负数，我们强制将其设为 0，否则保持不变。

如果没有 `else` 部分，那么当 x 为 -1 时，`keepPositive x` 会求值成什么呢？

在 JavaScript 中，有一个类似的 `if` 表达式需要 else 部分：

```
const keepPositive = x => x < 0 ? 0 : x
```

JavaScript 也有一个 `if` 语句，但在 PureScript 中一切都是表达式，不可能在一种情况下求值某物而在另一种情况下什么都不做。我们总是求值一个表达式或调用一个函数，然后对该结果进行一些处理。

如果你有一个没有 `else` 的 `if` 语句，那么你通常是在做以下某件事：执行计算或调用函数并将结果存储到变量中，或者为了副作用而调用函数，等等。

首先，在纯函数式编程中没有副作用，所以这种情况对我们来说不适用。

其次，调用一个函数获取其返回值，或者进行计算获取其结果，本质上是一回事。而且

