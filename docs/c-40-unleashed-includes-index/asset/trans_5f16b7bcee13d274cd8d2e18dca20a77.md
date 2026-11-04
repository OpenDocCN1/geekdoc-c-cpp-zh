
## 理由

但为什么要使用它？对于类型像 string 或 int 这样简单的局部变量，它并不会给你带来多少好处。事实上，恰恰相反，你可能会发现代码更难阅读，因为你必须自己推断类型。引入此功能应该有更好的理由。尽管语言最初的代码名称如此，C# 语言设计团队并不是因为功能“很酷”就添加功能。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_245_0.png)

我们还没有讨论泛型类型，但它们其实很容易理解。本质上，它们允许类型由其他类型参数化。一个具体的例子会让事情更清晰：

```csharp
Dictionary<string, List<int>> lotteryNumbers
    = new Dictionary<string, List<int>>();
```

这里我声明了一个名为 lotteryNumbers 的局部变量，它包含一个字典，将每个字符串键映射到整数值的列表。Dictionary 和 List 都是泛型类型，我们为其指定了类型参数。现在不要太担心细节；在本次讨论的上下文中，更重要的是代码的外观。

## 阅读代码的技巧

编程语言需要可发音。不仅仅是为了在极客深夜俱乐部里的讨论，更是在课程等情境下如此。例如，你如何发音泛型类型？所需的英语连接词是 of 和 and。在前面的例子中，我们声明了一个类型为 Dictionary of string and List of int 的局部变量。

有些语言在语法上比其他语言更简洁。C# 绝对相当简洁，使用简短的关键字、花括号块语法和符号运算符，而不是更多的关键字。Visual Basic 更接近英语，并且有更多的关键字。是的，写代码似乎需要更多时间（尽管像 Visual Studio 这样好的编辑器在自动完成支持方面帮助极大），但另一方面，它更容易阅读。例如，我们在 Visual Basic 中的泛型类型看起来像这样：

```vb
Dictionary(Of String, List(Of Integer))
```

听起来熟悉吗？

你看到了吗？是的，我们必须指定那个过长的类型名称两次才能声明特定类型的局部变量。在左侧，我们通过告诉编译器变量的类型来取悦编译器。在右侧，我们使用构造函数语法创建字典类型的实例。构造函数具体是什么现在并不重要，但关键在于右侧表达式的类型正是我们在左侧指定的类型。

在 .NET 1.0 中，在泛型类型出现之前，这并不是什么大问题：使用时类型名称不会任意变长。然而，由于泛型类型本质上是基于其他类型参数化的，你可以混合搭配各种类型来构建新类型：

```
List<HashSet<Dictionary<string, Tuple<int,int>>>>
```

反复指定如此长的类型名称不仅乏味，还会显著降低代码可读性。从 C# 3.0 开始，可以使用局部变量的类型推断来缩短代码：

```
var lotteryNumbers = new Dictionary<string, List<int>>();
```

现在它又能在一行内显示，大大减少了语法噪音。

## 关于分号和失业的下划线

如果还不明确，C# 允许代码跨多行拆分。语句的结束由分号字符表示，这在 C 风格语言中很常见。其他语言，例如 Visual Basic，最初选择了相反的方法：要拆分代码行，使用行延续标记。在 Visual Basic 的情况下，那是下划线字符。我在这里使用过去时，因为在 Visual Basic 10 中行延续的需求几乎完全被移除。在经济困难时期，为了帮助失业的下划线找到下一个挑战，为它们创建了一个网站：www.unemployedunderscores.com。

但还有更多。尽管泛型类型的用法简化是引入这种类型推断形式带来的非常方便的效果，但它并不是必需的。你完全可以没有它（尽管可能只是有点恼火）。然而，在 C# 3.0 中，作为 LINQ 使命的一部分，引入了另一个功能：匿名类型。我们将对该功能的详尽介绍推迟到第 19 章《语言集成查询精要》中的“匿名类型和对象初始化器”部分，但这里有一个示例：

```
var person = new { Name = "Bart", Age = 26 };
```

这创建了一个类型的实例，该类型有两个属性分别称为 Name 和 Age，类型分别为 string 和 int，并用指定的数据初始化。代码特别之处在于我们根本没有指定类型名称。相反，我们让编译器即时烘焙一个类型，具有所需的“形状”来容纳包含的数据。但是如果编译器为我们生成了一个类型，而我们无法知道其名称，因为我们不必指定它，那么我们如何引用它呢？解决办法在于使用 var 让编译器代表我们插入类型名称。

要亲眼看看这一点，在某个 C# 项目中输入上述代码，并再次观察 Visual Studio 中的 IntelliSense，如图 4.23 所示。如你所见，该工具精确地知道我们在谈论什么；我们没有丢失任何类型信息。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_247_0.png)

**图 4.23** 匿名类型的类型推断工作情况。

匿名类型作为编写 LINQ 查询表达式的先决条件而引入，特别是投影和分组子句：

```csharp
var expensive = from p in products
    where p.Price > 100
    select new { p.Name, p.Price };
```

要了解 expensive 变量的推断类型是什么，你必须等到我们在第 19 章深入介绍 LINQ 时再说。

### 何时使用它

这种语言特性的适当用例一直是冗长的在线和离线讨论组辩论的话题。意见涵盖了整个可能性光谱：

- 保守派对明显的静态类型缺乏感到不安，尽管他们意识到（希望如此）使用 var 根本不会改变语言的静态类型本质。有些人甚至会进一步禁止完全使用 var。
- 现实主义者构成中间阵营，承认在某些情况下 var 是不可避免的，特别是使用匿名类型时，并且在其他情况下是有益的（例如，减少对冗长泛型类型名称的需求）。
- 极端主义者会在可能的地方到处使用 var。这接近懒惰的边缘，并且可能使代码比最初更难读：类型名称是代码内部良好的文档来源（尤其是在赋值右侧包含复杂表达式时）。

我个人更喜欢这里的中间立场。始终站在阅读代码的人的角度思考。如果变量的类型不能从右侧立即看出，不要使用 var 进行隐式类型化。示例包括以下内容：

```
// Required
var person = new { Name = "Bart", Age = 26 };
var expensive = from p in products
    where p.Price > 100
    select new { p.Name, p.Price };

// Good
var lotteryNumbers = new Dictionary<string, List<int>>();
var name = person.ToString();

// Bad
var mystery = GetSomething(); // what's the return type of GetSomething?
var x = 2159940436;           // answer immediately: int or long?
```

## 哲学注记

C 风格语言传统上在标识符前面写类型：int x, string y, List<Person> z。我个人想不出很多选择这种方法的好理由，但现在一切都已成定局。

尽管类型至关重要，但通过名称轻松找到变量的声明位置并随后查看其类型更为方便。由于在标识符前面有可变长度的类型名称，名称无法对齐。这导致我在阅读代码时称之为“布朗眼动”（取自流体中粒子随机运动的物理现象名称）：

```
int x = 42;
string y = "Hello";
List<Person> z = new List<Person>();
```

其他语言采用了不同的方法，将类型写在名称之后。示例包括具有 Dim... As... 语法的 Visual Basic 以及 Haskell、ML 和 F# 等各种函数式语言：

```
' Visual Basic
Dim x As Integer = 42
Dim y As String = "Hello"
Dim z As New List(Of Person)

(* F# *)
let x : int = 42
let y : string = "Hello"
let z : Person list = []
```
