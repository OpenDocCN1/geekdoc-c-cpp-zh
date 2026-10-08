
当 `customer` 为 `Nothing` 时，因为在调用 `Iif` 函数之前，三个表达式都会评估并放入求值栈。

```
Iif(customer Is Nothing, customer.Name, "<unknown>")
```

条件 `If` 表达式测试一个表达式并返回值。使用 `Iif` 运行时函数，条件表达式仅在需要时才评估其操作数。在没有发生异常时，在代码中使用 `If` 往往是的。

该运算符有两种形式：

- `If(CondExpr, Expr1, Expr2)` — 评估 `CondExpr`，当它为真时，评估 `Expr1` 作为操作结果；评估 `Expr2`。
- `If(Expr, NullExpr)` — 评估方式等于 `(Expr Is Not Nothing, Expr, NullExpr)`。

## 总结

Visual Basic 目前是一种具有函数编程特征的面向对象语言，它起源于 20 世纪 90 年代，是一种结构非常简单的通用高级语言。Visual Basic 的祖先是 John G. Kemeny 和 Thomas E. Kurtz 于 1964 年开发的 BASIC；今天，你仍然可以识别出那种无结构语言的根源。

在 20 世纪末，Visual Basic 6.0 成为了一种非常流行的编程语言，拥有大量的开发者。.NET 将 Visual Basic 变成了一种真正的面向对象语言，并引发了社区内关于它仍然是同一种语言还是新语言的争论。

Basic 与 .NET Framework 并演进。除了框架的类库外，CLR 中的新功能和变化启发了语言在面向对象编程 (OOP) 原则之外嵌入了新的范式。

在第 22 章中，你将学习 Visual Basic 2010 的新功能，包括自动实现属性、多行表达式、动态支持、协变和逆协变。

## 22

## Visual Basic 10.0 语言改进

在第 21 章中，你了解到 Visual Basic 在 Windows 平台上已经有 19 年的历史。在这段漫长的岁月里，Visual Basic 从一种通用的 .NET 高级编程语言演变为多范式语言。Visual Basic.NET 的第一个版本将该语言变成了真正的面向对象语言，并引发了社区内关于它仍然是面向对象的 Visual Basic 还是一个新语言的争论。

Visual Basic 2005 增加了对泛型的支持，并获得了巨大的性能提升特性（如部分类型、运算符声明、`Using` 语句和可空类型）。Visual Basic 2008 开始接受函数编程原则，例如 LINQ 和查询表达式，并向语言添加了 XLM 字面量表达式 —— 这在核心 .NET 语言中是独一无二。

最新版本 Visual Basic 2010 旨在增强其功能特性，提供与动态编程语言的无缝协作。虽然几年前微软有不同的团队负责 Visual Basic 和 C#，但今天托管语言团队（Managed Languages Team）正为这两种语言的共同演进做出巨大努力。在第 24 章中将 Visual Basic 2010 的新特性与 C# 4.0 的改进进行对比，你可以看到这种共同演进。

阅读本章后，你将熟悉 Visual Basic 2010 语言的改进：

- 隐式行延续 — 当你的语句延续到下一行时，你可以省弃行尾使用的下划线字符。
- 自动实现属性 — 你可以快速指定类的属性，而无需编写 Get 和 Set 属性的代码。
- 集合初始化器 — 这些提供了一种简短的语法，允许你创建一个集合并用一组初始值填充它。当你从已知值创建集合时，集合初始化器非常有用。
- 多行 Lambda 表达式 — Lambda 表达式现在支持子程序和多行函数。
- 处理动态对象 — 在动态语言运行时 (DLR) 的帮助下，Visual Basic 可以绑定来自 Python 和 Ruby 等动态语言的对象。
- 变异 — NET 开发者曾受限于 `IEnumerable(Of Object)` 无法替换 `IEnumerable(Of String)` 的事实。现在，这种替换可以实现了！Visual Basic 实现了类型安全的协变和逆协变，常见的基类类型（主要是泛型集合接口）也已更新以支持这种行为。

## 新的提高生产力的语法

语言中有些新特性既没有改变你使用 Visual Basic 编程的方式，也不是全新的范式。然而，它们仍然非常有用，因为它们让你的代码更短、更易读，并总体提高了你的生产力。本节提供了它们的概述。

## 隐式行延续

长期以来，代码行尾的下划线 (`_`) 字符一直是 Visual Basic 的标志，通常被 C# 程序员称为一种“嘈杂的语言”。即使在 Visual Basic 2008 中，你也必须使用下划线，如下：

```
Dim fruits() As String = "Apple", "Peach", "Orange", "Banana", "Lemon", \
"Pear", "Grapefruit", "Watermelon"

Dim filteredFruits = \
From fruit \
Where fruit.StartsWith("P") And fruit.Length < 20 \
Order By fruit \
Select fruit
```

显式行延续有几个问题：

- 使用它很麻烦。
- 下划线对开发者没有真正的价值（有些人甚至怀疑它是否有价值）。它是为了帮助语言解析器识别连续的行，可能源于 Basic 程序逐行分析和编译为 P 代码的时代。
- 随着语言的演进并向函数原则发展，开发者自然地希望将语句断行以提高可读性（看看之前的查询表达式）。在行尾输入额外的下划线违背了这种愿望。

长期以来，托管语言团队实现了了巨大飞跃。Visual Basic 2010 允许在大多数情况下省略行延续字符。例如，你可以像这样写之前的代码：

```
Dim fruits() As String =
  "Apple", "Peach", "Orange",
  "Banana", "Lemon", "Pear",
  "Grapefruit", "Watermelon", "Plum"

Dim filteredFruits =
From fruit In fruits
Where fruit.StartsWith("P") And fruit.Length < 20
Order By fruit
Select fruit
```

以下可以在无下划线的情况下将语句延续到下一行的位置列表：

- 逗号 (,) 之后
- 左括号 `(` 之后或右括号 `)` 之前
- 左括号 `{` 之后或右括号 `}` 之前
- XML 字面量中嵌入表达式的 `<=` 之后或 `>` 之前
- 连接运算符 `&` 之后
- 赋值运算符 (`=`, `+=`, `-=`, `*`, `/`, `^`, `<<`, `>>`) 之后
- `Is` 和 `IsNot` 运算符之后
- 成员限定符 `.`。在使用 `With` 语句或在类型初始化列表中提供值时，必须在成员限定符字符后包含行延续字符 (`_`)。
- XML 轴限定符 (`.` 或 `.` 或 `...`) 之后。然而，在使用 `With` 关键字时，指定成员限定符必须包含行延续字符 (`_`)。
- 在指定属性时，小于号 `<` 之后或大于号 `>` 之前。此外，在指定程序集级或模块级属性时，大于号 `>` 也需要行延续字符。
- 查询运算符之前和之后。不能在由多个关键字组成的查询运算符（`Order By`, `Group Join`, `Take While` 和 `Skip While`）之间断行。
- `For` 语句中 `In` 关键字之后。
- 集合初始化器中 `From` 关键字之后（你将在本章稍晚时候学习这些内容）。

