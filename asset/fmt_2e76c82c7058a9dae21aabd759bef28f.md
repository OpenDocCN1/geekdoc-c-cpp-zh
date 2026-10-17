
```
type Family r =
  { fatherName :: String
  , motherName :: String
  , childName :: String
  | r
  }
```

① 我们必须将 `r` 作为将扩展此记录的行传递，因此术语可扩展记录。

② 我们使用此语法指定 `r` 是扩展记录的行类型。

这很棒，因为它消除了重复，但它也给了我们另一个巨大的好处。它在创建 `Family` 时给了我们一些灵活性，例如我们可以添加其他字段：

```
Family ( fatherOccupation :: Occupation, motherOccupation :: Occupation )
```

或者我们可以添加零个字段：

```
Family ()
```

注意 `()` 是空行的语法，即没有字段。注意不要将其与 Haskell 或 Elm 中的 unit 类型和值混淆。

现在我们可以看到使用行的好处，让我们先用行来定义我们的字段，然后将它们组合起来构造一个名为 `Family` 的记录。首先，将 `FamilyAgesRow` 添加到你的代码中，然后在继续之前自己编写 `FamilyNamesRow`。

完成后，你应该有如下内容：

```
type FamilyAgesRow
  = ( fatherAge :: Int, motherAge :: Int, childAge :: Int )

type FamilyNamesRow
  = ( fatherName :: String, motherName :: String, childName :: String )
```

现在我们准备使用它们来创建 `Family`。你将如何从这两个行创建 `Family`？

你可能会认为可以像这样将它们添加到 `Family`：

```
-- NOT VALID PureScript SYNTAX!!!
newtype Family = Family { | FamilyNamesRow, FamilyAgesRow }
```

或者也许：

```purescript
-- NOT VALID PureScript SYNTAX!!!

newtype Family = Family { | FamilyNamesRow | FamilyAgesRow }
```

不幸的是，这些都不起作用。要实现这一点的方法是为我们的行类型 `FamilyAgesRow` 和 `FamilyNamesRow` 添加一个行参数。请在阅读之前先这样做。

如果你在这方面遇到困难，不要担心。你只是还没有看到足够的语法。所以这里是：

```purescript
type FamilyAgesRow r =

  ( fatherAge :: Int, motherAge :: Int, childAge :: Int | r )

type FamilyNamesRow r =

  ( fatherName :: String

  , motherName :: String

  , childName :: String | r )
```

1. 将 `r` 参数添加到两个类型构造子。
2. 使用 `| r` 语法扩展行。

花点时间更新你的代码。

事实证明，当我创建行时，我总是这样创建。然后我可以将它们组合起来制作更复杂的行，例如：

```purescript
FamilyNamesRow (FamilyAgesRow ())
```

这里我们用 `FamilyAgesRow` 扩展 `FamilyNamesRow`，而 `FamilyAgesRow` 用空行 `()` 扩展。

继续创建一个名为 `Family` 的 `newtype`，它是一个包含两个行字段的记录，然后继续阅读。

以下是定义：

```purescript
newtype Family = Family { | FamilyNamesRow (FamilyAgesRow ()) }
```

这里我们有名为 `Family` 的 `newtype`，它有一个数据构造子，接受一个记录，该记录具有 `FamilyNamesRow` 和 `FamilyAgesRow` 中的所有字段。

让我们看看我们目前拥有的内容：

```
type FamilyAgesRow r

  = ( fatherAge :: Int, motherAge :: Int, childAge :: Int | r )

type FamilyNamesRow r

  = ( fatherName :: String, motherName :: String, childName :: String | r )

newtype Family = Family { | FamilyNamesRow (FamilyAgesRow ()) }
```

为了让它更真实一些，让我们不要对年龄使用 `Int` 或对全名使用 `String`。

继续创建名为 `Age` 和 `FullName` 的 `newtype`，然后更新 `FamilyAgesRow` 和 `FamilyNamesRow` 以使用它们。请在尝试之前不要阅读解决方案。

以下是 `Age` 的 `newtype`，它只是包装一个 `Int`：

```
newtype Age = Age Int
```

以及包装 `String` 的 `FullName`：

```
newtype FullName = FullName String
```

以及我们更新后的行：

```
type FamilyAgesRow r

  = ( fatherAge :: Age, motherAge :: Age, childAge :: Age | r )

type FamilyNamesRow r =

  ( fatherName :: FullName

  , motherName :: FullName

  , childName :: FullName

  | r

  )
```

既然我们在这里，继续为 `Age`、`FullName` 和 `Family` 创建 `Show` 实例，然后再阅读。

我们只需要派生 `Generic` 实例，我们就可以使用 `genericShow`：

```
newtype Age = Age Int

derive newtype instance showAge :: Show Age

age :: Age

age = Age 10

--

newtype Age' = Age' Int

derive instance genericAge' :: Generic Age' _

instance showAge' :: Show Age' where

  show = genericShow

age' :: Age'

age' = Age' 10

--

log $ show age  -- Prints 10

log $ show age' -- Prints (Age' 10)
```

使用 `derive newtype`，编译器只是委托给底层类型，对于 `Age` 来说是 `Int`。这就是为什么只显示数字 10，而相比之下，使用 `genericShow`，我们得到完整的类型，`(Age' 10)`。

对于我们的目的，我们将利用 `genericShow`，所以没有必要更新你的代码。

为了让我们的示例更简单，我们只会集中在年龄的验证上。所以让我们创建一个名为 `FamilyAges` 的 `newtype`，它镜像 `Family` 但只包含年龄。别忘了让它也能显示。在阅读以检查你的工作之前先编写它。

类型定义几乎与 `Family` 相同：

```
newtype FamilyAges = FamilyAges { | FamilyAgesRow () } ①

derive instance genericFamilyAges :: Generic FamilyAges _

instance showFamilyAges :: Show FamilyAges where

  show = genericShow
```

① 这里唯一的差别是我们只包含来自 `FamilyAgesRow` 的字段，它用空行，即 `()` 扩展。

我们现在准备创建我们将用于验证 `Age` 的函数。编写一个名为 `validateAge` 的这样的函数的类型签名，检查年龄是否在指定范围内，然后继续查看它与我的比较如何。记住，我们希望它使用我们的 `Validation` 类型，所以我们可以收集到所有的错误。

实现这种功能的方法有很多，但下面是我想出来的方法：

```
validateAge :: Int -> Int -> Age -> String

    -> Validation (Array String) Age
```

让我们逐部分查看这个签名。首先，告诉我这部分是什么意思：

```
validateAge :: Int -> Int -- partial Type Signature
```

哪个 `Int` 是上限和下限？你可能根据惯例猜测下限在前上限在后，但我以前就是这么做的，结果错了。

为了解决这个问题，我们将为 `LowerAge` 和 `UpperAge` 创建 `newtype`：

```
newtype UpperAge = UpperAge Int

newtype LowerAge = LowerAge Int
```

请将此添加到你的代码中并更改你的 Type Signature。我来更改我的：

```
validateAge :: LowerAge -> UpperAge -> Age -> String

    -> Validation (Array String) Age
```

好了，现在它清晰多了，而且是类型安全的。此时，前 3 个参数都很清楚。`String` 参数是什么？

那是一个字符串，用来说明白个人的年龄无效，例如 "Father"、"Mother" 和 "Child"。这从 Type Signature 中并不明显。我们是否应该在这里创建另一个类型？可以，但它只会在这里使用，而且由于没有其他 `String` 参数，我就把它留下了。我未来可能会为此后悔，不过，如果我后悔了，到时候再改。

返回参数是这里最重要的一部分。它不是 `Either`，因为我们想要所有错误，而不仅仅是第一个。这就是我使用我们的 `Validation` 类型的原因。此外，我使用 `Array String` 作为 `Semigroup` 错误类型。如果我使用 `String`，它也是一个 `Semigroup`，那么它会连接错误消息，使其很难阅读，因为没有任何东西可以分隔一个错误和另一个错误。

最后，结果类型是 `Age`，因为我们正在验证的就是它。

你的解决方案可能与此同构，但为了让我们保持在同一页面上，请用这个 Type Signature 替换你的。阅读之前先这么做。

```
createFamilyAges

  :: Int

  -> Int

  -> Int

  -> Validation (Array String) FamilyAges ①

---

createFamilyAges

  :: Age

  -> Age

  -> Age

  -> Validation (Array String) FamilyAges ②

---

createFamilyAges

  :: { fatherAge :: Age, motherAge :: Age, childAge }

  -> Validation (Array String) FamilyAges ③

---

createFamilyAges

  :: { | FamilyAgesRow () } -> Validation (Array String) FamilyAges ④
```

① 使用 `Int` 使其很容易意外交换年龄或使用任何数字，例如温度值，即没有类型安全。

② 很难分辨哪个参数是母亲的年龄。

③ 重复了一个 `Record` 定义。

④ 利用 `FamilyAgesRow` 的定义来避免重复。

在这里我们看到了独立于 `Record` 定义 `Row` 的好处。第一个参数并不是一个 `FamilyAges`。相反，它是任何具有类似标签的年龄记录，但这些不是相同的类型。`FamilyAges` 将与此类型统一，这意味着你可以将 `FamilyAges` 传递给这个函数。但你也可以传递无限多种不同的记录，只要它们具有与 `FamilyAgesRow` 相同的标签即可。

`createFamilyAges` 通常被称为智能构造函数。当你想要确保你的代码的用户不能意外创建你的类型的无效版本时，就会创建智能构造函数。在这种情况下，绝对不要导出数据构造函数 `FamilyAges`。 你只想导出类型构造函数 `FamilyAges`。如果这听起来令人困惑，那是因为数据构造函数和类型构造函数具有相同的名称。

这就让我们的模块客户端别无选择，只能调用 `createFamilyAges`，而正如我们很快会看到的，它只会返回有效的 `FamilyAges`。

实现方法如下：

```
module Ch17

( Age (..) ①

, FamilyAges ②

, FamilyAgesRow ③

, Validation ④

, createFamilyAges ⑤

, test ⑥

) where ⑦
```

① 如果没有它，我们会收到编译器错误，告诉我们要导出 `FamilyAgesRow`，我们也需要导出 `Age`。我们使用 `(..)` 同时导出类型构造函数和数据构造函数。

② 我们只导出类型构造函数，这意味着你不能直接构造该类型。

③ 我们导出类型别名 `FamilyAgesRow`。

④ 如果没有它，编译器会抱怨我们也需要导出 `Validation`。这是因为如果不能引用 `Validation` 类型，就无法使用 `createFamilyAges`，而 `createFamilyAges` 返回的就是 `Validation` 类型。请注意，我们选择不导出 `Validation` 数据构造函数。我们以后可能想要这样做，但现在我们就把它留在这里。

⑤ 我们导出我们的智能构造函数，以便可以“安全地”构造 `FamilyAges`。

⑥ 我们导出 `test`，这样我们的 `main` 仍然可以调用测试代码。

⑦ 请注意 `where` 关键字的所在位置，它目前直接跟在 `module` 名称之后。这是因为我们还没有显式导出任何内容。在这种情况下，模块中的所有内容都会被导出。在这种情况下，只有列出的内容会被导出。

将此添加到你的模块定义中，以便作为如何执行此操作的示例。

然后编写该函数的其余部分。记住，我们正在练习 `Applicative`s。所以回去看看上一章中的 `fullNameEither` 示例，刷新你的记忆。然后，使用我们在那里使用的相同技术完成这个函数。在这里停止阅读并试试看。

让我们一如既往地从 Type Signature 开始：

```
createFamilyAges

  :: { | FamilyAgesRow () } -> Validation (Array String) FamilyAges
```

我们将接受一个年龄记录并返回 `FamilyAges` 或一个错误字符串的 `Array`。

接下来，让我们添加函数参数：

```haskell
createFamilyAges
  :: { | FamilyAgesRow () } -> Validation (Array String) FamilyAges
createFamilyAges { fatherAge, motherAge, childAge } = ???
```

请注意，我们在它用完后立即解构记录。

接下来，我们从 `FamilyAges` 类型的 Data Constructor 开始，也称为 `FamilyAges`：

```haskell
createFamilyAges
  :: { | FamilyAgesRow () } -> Validation (Array String) FamilyAges
createFamilyAges { fatherAge, motherAge, childAge } = FamilyAges ???
```

此时，提醒一下 Data Constructor `FamilyAges` 期望的参数可能会有所帮助：

```haskell
type FamilyAgesRow r = ( fatherAge :: Age, motherAge :: Age, childAge :: Age | r )

newtype FamilyAges = FamilyAges { | FamilyAgesRow () }
```

所以，它想要一个记录。我们需要构建一个包含值的记录。但不仅仅是任何值。我们希望它们是经过验证的值。

如果你回顾了 `fullNameEither`，你就知道我们将使用 `<$>` 和 `<*>`。而且这个 `Applicative` 序列的第一部分总是从一个函数开始，要么在 Context 中，要么不在。如果它在 Context 中，那么我们立即使用 `<*>`，否则我们使用 `<$>`，然后对所有后续参数使用 `<*>`。

很多时候，我们可以使用 Data Constructor 作为该函数，但在这种情况下，`FamilyAges` 只有一个参数，那就是一个记录，该记录有 3 个字段，每个字段都必须经过验证。我们需要一个接受 3 个参数并返回经过验证的记录的函数。

让我们在代码中添加这个神奇的函数，暂时称它为 `magic` 作为占位符：

```haskell
createFamilyAges
  :: { | FamilyAgesRow () } -> Validation (Array String) FamilyAges
createFamilyAges { fatherAge, motherAge, childAge } =
  FamilyAges <$> magic ???
```
