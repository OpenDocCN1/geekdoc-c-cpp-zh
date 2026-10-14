
```
toOccupation :: String -> Maybe Occupation
toOccupation = case _ of ① ②
  "Doctor" -> Just Doctor
  "Dentist" -> Just Dentist
  "Lawyer" -> Just Lawyer
  "Unemployed" -> Just Unemployed
  _ -> Nothing ③
```

① `toOccupation`是无点的。

② 我们正在使用通配符`case`表达式。

③ 这是捕获所有情况，在这里我们有一个无法识别的`String`。

要意识到，这个转换函数很脆弱。如果未来我们添加另一个`Occupation`，我们就必须记得同时更新这个函数。编译器在这里无法帮助我们。

要理解原因，想象我们添加了一个`BusDriver`职业。注意没有任何方法让编译器知道`String`"BusDriver"应该返回`Just BusDriver`。这是因为捕获所有情况已经很好地匹配了我们新添加的职业。

现在让我们处理上面的代码中的`???`并完成解码器：

```
instance fromCSVPerson :: FromCSV Person where
  fromCSV (CSV str) = case split (Pattern ",") str of
    [name, age, occupation] -> case fromString age of
      Just age' -> case toOccupation occupation of ①
        Just occupation' -> Just $ Person
          { name: FullName name
          , age: Age age'
          , occupation: occupation'
          }
        Nothing -> Nothing ②
      Nothing -> Nothing
    _ -> Nothing
```

① 使用可能失败的机会将`String`转换为`Occupation`。

② 这是我们未能解码`occupation`的情况。

虽然这段代码可行，但很混乱。我们还没有学到足够的内容来清理它，但作为一个预览，这里是生产代码中它会是什么样子。我把它放在这里，以防你在完成这本书后再次回到这里：

```
instance fromCSVPerson :: FromCSV Person where
  fromCSV (CSV str) = case split (Pattern ",") str of
    [name, age, occupation] -> do ①
      age' <- fromString age
      occupation' <- toOccupation occupation
      pure $ Person
        { name: FullName name
        , age: Age age'
        , occupation: occupation'
        }
    _ -> Nothing
```

① 我们正在`Maybe` `Monad`中执行。未来的你会理解并欣赏这一点。

到目前为止应该很清楚，这个版本比我们的版本更干净。一旦我们学习到`Monad`，我们就能编写更简单的代码。

### 7.29. 测试 FromCSV

测试编码器和解码器的最佳方式是进行往返测试，即编码然后解码并将结果与原始值进行比较。它们应该匹配。

在继续之前，试着为`FromCSV`编写一个好的测试，但首先为`Person`编写一个`Eq`实例，以便我们可以比较编码/解码后的`Person`与原始值。在阅读后续内容之前完成此操作。

所以首先，我们必须能够比较两个`Type` `Person`的值是否相等：

```
data Person = Person
  { name :: FullName
  , age :: Age
  , occupation :: Occupation
  }
derive instance eqPerson :: Eq Person -- COMPILER ERROR!!
```

编译器抱怨因为它需要知道如何比较`Age`。我们也应该添加它。同时，我们也应该为`FullName`和`Occupation`添加`Eq`。

让我们先做`Age`：

```
newtype Age = Age Int
derive instance newtypeAge :: Newtype Age _
derive newtype instance showAge :: Show Age
derive newtype instance eqAge :: Eq Age
```

① 这是我们需要添加到现有`Age`代码中的唯一一行。

让我们将上面的`Age`与`FullName`的实现进行比较：

```
newtype FullName = FullName String

instance showFullName :: Show FullName where
  show (FullName name) = name
```

我们没有`Newtype`实例的好处。试着在阅读之前将此实现转换为与`Age`相同。

以下是使用`Newtype`的`FullName`。它替换了上面所有的代码：

```
newtype FullName = FullName String
derive instance newtypeFullName :: Newtype FullName _
derive newtype instance showFullName :: Show FullName
```

现在，像我们对`Age`所做的那样，简单地添加`Eq`实例。先试试再继续。

以下是`FullName`的`Eq`实例：

```
derive newtype instance eqFullName :: Eq FullName
```

现在我们只需要为`Occupation`添加`Eq`。阅读之前先试试。

我们可以简单地添加一行代码来实现`Occupation`的`Eq`实例：

```
derive instance eqOccupation :: Eq Occupation
```

现在我们的编译错误消失了：

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "console"
  , "effect"
  , "integers" ①
  , "lists"
  , "maybe"
  , "newtype"
  , "prelude"
  , "psci-support"
  , "strings"
  , "tuples"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 在这里添加以保持字母顺序。

当你重新运行测试时，注意到它们都`FAILED`。

不知怎么的我们破坏了测试。让我们弄清楚出了什么问题。这里是我们的测试代码：

```
test :: Effect Unit
test = do
  log $ show $ toCSV
    (Person
      { name: FullName "Sue Smith"
      , age: Age 23
      , occupation: Doctor
      }) == CSV "Sue Smith,23,Doctor"
  let person = Person
      { name: FullName "Sue Smith"
      , age: Age 23
      , occupation: Doctor
      }
  log $ show $ (toCSV person # fromCSV) == Just person
```

两个测试都打印`false`，这是不对的。这让我认为`toCSV`不能正常工作，因为两个测试都使用`toCSV`但只有一个测试使用`fromCSV`。所以，让我们测试这个理论。

将以下代码添加到测试代码顶部以打印`toCSV`的结果：

```
log $ show $ toCSV -- COMPILER ERROR! ①
  (Person
    { name: FullName "Sue Smith"
    , age: Age 23
    , occupation: Doctor
    })
```

① 没有找到`Data.Show.Show CSV`的类型类实例。

我们从未为`CSV`实现`Show`，所以让我们添加它：

```
newtype CSV = CSV String
derive instance newtypeCSV :: Newtype CSV _
derive newtype instance eqCSV :: Eq CSV
derive newtype instance showCSV :: Show CSV ①
```

① 我们只需要添加这一行。

现在使用`npx spago run`运行测试会打印：

```
"\"Sue Smith\",23,Doctor" ①
false
false
```

① `\"`看起来不对。

由于某种原因，我们的`String`中嵌入了引号。但为什么？我们又改变了什么来破坏它？

乍一看可能并不明显为什么会这样。为了看原因，让我们再次运行`REPL`：

```
npx spago repl
```

并在提示符下输入：

```
> show "Sue Smith"
"\"Sue Smith\"" ①

> ^D ②
See ya!
()
```

① 又出现了那些嵌入的引号。

② 按`Control-D`退出。

从这个测试中，我们可以看到显示一个`String`会用双引号包围该`String`。

这意味着我们在派生其`Show`实例时破坏了`FullName`。让我们看一下`BEFORE`：

```
instance showFullName :: Show FullName where
  show (FullName name) = name ①
```

① 我们不调用`show name`。我们只是返回`String`。

现在`AFTER`：

```
derive newtype instance showFullName :: Show FullName ①
```

① 委托给被包装类型的`Show`实例，即`String`。

我们可以看到派生的代码在底层值上调用`show`，即`name`。这与我们手工编写的`show`完全不同，后者只是返回`String`。

让我们通过首先删除`derive`来恢复`FullName`的旧`Show`实例：

```
derive newtype instance showFullName :: Show FullName ①
```

① 删除这一行。

然后通过添加手工编写的`Show`实例：

```
instance showFullName :: Show FullName where
  show (FullName name) = name
```

现在再次运行测试时，它会打印：

```
"Sue Smith,23,Doctor"
true
true
```

好多了。

我们将调试代码保留，但只是注释掉：

```fsharp

test :: Effect Unit

test = do

  -- log $ show $ toCSV

  --   (Person

  --     { name: FullName "Sue Smith"

  --     , age: Age 23

  --     , occupation: Doctor

  --     })

  log $ show $ toCSV

    (Person

      { name: FullName "Sue Smith"

      , age: Age 23

      , occupation: Doctor

      }) == CSV "Sue Smith,23,Doctor"

let person = Person

      { name: FullName "Sue Smith"

      , age: Age 23

      , occupation: Doctor

      }

log $ show $ (toCSV person # fromCSV) == Just person

```

### 第8章 抽象代数

函数式编程大量借鉴了数学中的许多概念。其中一个领域就是范畴论。我们将在讨论函子、应用和单子时看到这一点。

另一个领域是抽象代数。我们将对这些概念进行整体的粗略了解，因为我们只需要理解它们与编程相关的部分。这里要提醒一句。这些概念实际上非常简单。简单到你完全可以在代数课上轻松学会它们。

我猜想这些科目之所以不在中学教授，是因为它们被认为过于抽象，不适合教给每个学生，因为大多数学生未来并不需要它们。不幸的是，这种思维在一个仍然为培养工业革命工人而设立的教育体系中根深蒂固。但我们生活在信息时代，这些概念对我们程序员来说是有益的，因此值得学习。

另一点要记住的是，这些概念并非由某个人在短时间内发展起来。它们经历了数百年，由来自不同国家的人们共同发展，其中许多人研究的是数学的不同领域。

这在一定程度上解释了为什么相似概念的名称彼此差异如此之大。例如，`Monoid`（幺半群）和`Semigroup`（半群）这两个概念的差异仅在于一条规则或要求，但它们的名称却暗示着它们是截然不同的想法。

这种不幸的历史偶然事件只是我们需要克服的唯一困难。这里的名称很复杂，但概念非常简单。相信我，你在编程中做过比这里要做的困难得多的事情。

#### 8.1. 二元运算符

作为快速回顾，让我们看一下二元运算符。单词`Binary`（二元）意为2。这个2代表2个参数。`Operator`（运算符）是一个暗示特定函数的符号，例如`+`：

```
12 + 73
```

这里的2个（二元）参数是12和73。`+`（运算符）是数值加法。

以下是我们都应该非常熟悉的一些二元运算符的更多示例：

```
+
-
*
/
&&
||
```

二元运算符通常以中缀形式书写，在编程中如此，在数学中总是如此：

```
1 + 3
51 - 19
4 * 43
100 / 20
true && false
false || true
```

##### 8.1.1. 结合律

如果一个二元运算符•满足以下条件，则它是结合的：

```
a • (b • c) = (a • b) • c ①
```

> ① 括号用于结合。在左侧，括号将b与c结合，在右侧，它将a与b结合。

如果你将括号视为将运算符与其参数结合的机制，就能记住这意味着什么。

这里我们使用符号•来代表**任何**二元运算符。可以是加法、乘法或逻辑与。

当一个二元运算符是结合的时，我们可以随意重新排列括号，结果相等：

```
((a • b) • c) • d   =
 (a • (b • c)) • d   =
 (a • b) • (c • d)   =
  a • (b • (c • d))  = ...
```

我们对结合运算符太熟悉了（运算顺序无关紧要）：

```
(1 + 3) + 47 = 1 + (3 + 47)
2 * (17 * 54) = (2 * 17) * 54
```

我们对非结合运算符同样熟悉（运算顺序很重要）：

```
1 / (3 / 5) /= (1 / 3) / 5
(17 - 42) - 3 /= 17 - (42 - 3)
```

##### 8.1.2. 交换律

如果一个二元运算符•满足以下条件，则它是交换的：

```
a • b = b • a ①
```

① `a`和`b`交换或穿过二元运算符，结果不变。

同样，我们在算术中见过许多交换运算符的示例：

```
1 + 10 = 10 + 1
3 * 25 = 25 * 3
```

以及非交换运算符：

```
1 - 10 /= 10 - 1
3 / 25 /= 25 / 3
```

#### 8.2. 封闭性

在编程中，`Closure`（闭包）一词的含义与数学中的含义截然不同。

让我们研究一下数学定义。

取以下集合：

```
{ true, false }
```

让我们将二元运算符`&&`应用于集合元素的所有组合：

```
true  && true  = true
true  && false = false
false && true  = false
false && false = false
```

注意，结果总是我们集合中的一个值。当这种情况发生时，我们说该集合在`&&`运算下是封闭的。

再取另一个集合：

```
{ 1, 2, 3 }
```

这个集合在二元运算符`+`下封闭吗？

不，不封闭，因为`3 + 3 = 6`，而6不在集合中。

那减法呢？乘法呢？或除法呢？

事实证明，这些问题的答案都是否定的。

让我们考虑集合：

```
{ 1, 2, 3, ... }
```

> 正整数集合。

这个集合在二元运算符`+`下封闭吗？

是的。任意两个正整数相加产生一个正整数。

那减法、除法或乘法呢？

减法和除法不封闭，例如`1 − 3 = −2`和`1 / 3 = 1/3`。

但这个集合在乘法下封闭，因为任意两个正整数相乘是一个正整数。

#### 8.3. 原群

`Magma`（原群）是一种红色的、炽热的液态岩石。但它也是一种抽象代数结构。它可以说是我们这里讨论的所有内容的基础。我们将研究的其他代数结构都建立在此之上。

> 一个*原群*是一个在二元运算符下封闭的集合。

以下是一个原群的示例：

```
`M = { true, false } and • = &&`
```

集合**M**是所有**布尔值**的集合，二元运算符**•**是**逻辑与**运算，**&&**。

以下是一个不是原群的示例：
