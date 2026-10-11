
`New Macaw With {.NickName = "Bella", .Age = 4)`

`New Macaw With {.NickName = "Grey", .Age = 11}`

```
Sub Main()

Dim macawsToDogs = TransformMacawTo(Macaws, AddressOf TransformMacawTo)

Dim dogsToEagles = TransformMacawTo(Macaws, AddressOf TransformMacawToEagle)

End Sub

Private Function TransformMacawTo(

ByVal pets As IEnumerable(Of Macaw),

ByVal transformation As Func(Of Macaw, Pet)) As Enumerable(Of Pet)

    Dim result As New List(Of Pet)

    For Each pet In pets

        result.Add(transformation(pet))

    Next

    Return result

End Function

Private Function TransformDogTo(

ByVal pets As IEnumerable(Of Dog),

ByVal transformation As Func(Of Dog, Pet)) As Enumerable(Of Pet)

    Dim result As New List(Of Pet)

    For Each pet In pets

        result.Add(transformation(pet))

    Next

    Return result

End Function

Private Function TransformDogTo(ByVal macaw as Macaw) As Dog

End Function

Private Function TransformToEagle(ByVal pet As Pet) As Eagle

    Return New Eagle With (.NickName = pet.NickName, .Age = pet.Age)

End Function

End Module
```

在 `TransformMacawTo` 函数中，使用了 `Func(Of Macaw, Pet)` 委托，而在 `TransformDogTo` 函数中，传递了 `Func(Of Dog, Pet)` 参数。

两个函数 `TransformToDog` 和 `TransformToEagle` 负责对宠物进行“魔法转换”。以下代码行利用了变变性：

```vbnet
Dim MacawToDogs = TransformMacawTo(Macaw, AddressOf TransformToDog)

Dim MacawToEagles = TransformMacawTo(Macaw, AddressOf TransformToEagle)

Dim dogToEagles = TransformToDog(Dog, AddressOf TransformToEagle)
```

注：

在两次 `TransformMacawTo` 调用中，`Func(Of Macaw, Pet)` 参数被替换为 `Func(Of Macaw, Dog)` 和 `Func(Of Pet, Eagle)`。在 `TransformToDog` 的调用中，`Func(Of Pet, Eagle)` 是完全有效的、强类型的，并且在背后没有任何类型转换魔法！

为什么例如，`Func(Of Dog, Pet)` 可以被替换为 `Func(Of Pet, Eagle)` 呢？`Func(Of Dog, Pet)` 返回是协变的，这意味着你可以返回一个名为 `Eagle` 的派生类型，因为 `Eagle` 是一个 `Pet`。同样的，`Func(Of Dog, Pet)` 在 `Dog` 上是逆变的，因此对 `Pet` 的操作适用于 `Dog`，因为 `Dog` 派自 `Pet`。因此，`Func(Of Pet, Eagle)` 是 `Func(Of Dog, Pet)` 的良好替换。

## 类型选项中的变变

显然，我们并不限于仅使用带有类型参数的现有泛型类型。你可以创建自己的泛型接口和委托。可以使用修饰符表示逆变，使用 `Out` 修饰符表示协变类型参数。如果没有修饰符，类型参数将保持不变。

例如，考虑以下声明：

```vbnet
Public Interface IOperations(Of T, U, V)

...

End Interface

Public Delegate MyDelegate(Of T, U, Out X)

(ByVal tpar as T, ByVal upar as U) As X
```

在这里，`X` 是协变的，而 `U` 和 `V` 是不变的类型参数。编译器会检查以确保变变类型参数的规则。例如，在下面的接口定义中，所有的声明都是无效的，因为更多的协变参数出现在错误的位置：

```vbnet
Public Interface IOperations(Of T, U, V)

Function OutputUnsafeOp1() As T

Function OutputUnsafeOp2() As U

Function OutputUnsafeOp3() As List(Of T)

Function OutputUnsafeOp4() As Func(Of V, U)

Sub OutputUnsafeOp5(ByRef tpar As T)

Sub OutputUnsafeOp6(ByRef par As Func(Of V, U))

End Interface
```

同样，在下面的接口定义中，所有的操作都是无效的，因为协变参数在输入中是无效的：

```vbnet
Public Interface IOperations(Of Out T, U)

Sub InputUnsafeOp1(ByVal t as T)

Function InputUnsafeOp2() As U

Function InputUnsafeOp3() As Func(Of V, U)

End
```

## 变变与反射

在 `TransformMacawTo` 函数中，使用了 `Func(Of Macaw, Pet)` 委托，而在 `TransformDogTo` 函数中，传递了 `Func(Of Dog, Pet)` 参数。

两个函数 `TransformToDog` 和 `TransformToEagle` 负责对宠物进行“魔法转换”。以下代码行利用了变变性：

```vbnet
Dim MacawToDogs = TransformMacawTo(Macaw, AddressOf TransformToDog)

Dim MacawToEagles = TransformMacawTo(Macaw, AddressOf TransformToEagle)

Dim dogToEagles = TransformToDog(Dog, AddressOf TransformToEagle)
```

这段代码遍历了 `System` 中的所有的泛型类型。嵌套的 `For` 循环遍历类型参数，并使用 `System.Type` 的 `GenericParameterAttributes` 属性获取有关变变的信息。

```vbnet
Imports System.Reflection

Module Module1

  Sub Main()

    Dim As = GetType(Assembly)

    Dim GenericTypes = From type In As.GetTypes()

    Where type.IsGenericDefinition And type.IsPublic

    Select type

    For Each type In GenericTypes

      Console.WriteLine("{0}: {1}", type.Name)

      For Each typeParam In type.GenericParameterAttributes And GenericParameterAttributes.VarianceMask

        If (typeParam And GenericParameterAttributes.Covariant) <> 0 Then

          Console.WriteLine("{0}: covariant", typeParam.Name)

        ElseIf (typeParam And GenericParameterAttributes.Contravariant) <> 0 Then

          Console.WriteLine("{0}: contravariant", typeParam.Name)

        Else

          Console.WriteLine("{0}: invariant", typeParam.Name)

        End If

      Next

    Next

  End Sub

End Module
```

# 第五部分

# C#

## 第 23 章：C# 历史

## 第 24 章：C# 4.0 语言改进

### 23

## C# 的历史

在过去的十多年里，C# 语言（当然也包括 .NET 框架）已经演变并成为现代软件开发的决定性部分。从 2002 年初首次发布以来，C# 语言经历了惊人的进步，并吸引了数百万开发人员加入 .NET 阵营。截至今日，C# 已经进入第四版本。

本章简要介绍了 C# 语言的历史。本章的讨论并不是为了教你这门语言，这绝对不在本书的范范围内。相反，本章的讨论假设你已经使用过这种语言。如果你是 Visual Basic 开发者，本章也能帮助你保持联系。

本章涵盖了以下主题：

- C# 语言的简史
- C# 的主要特性（在 C# 1.0 中确立的）
- C# 2.0 和 C# 3.0 特性的简要概述

在过去发布了如此多的 Visual Studio 和 .NET 框架后，现在可以很确定，每一个主要的 Visual Studio 版本都包含一个新版本的 C# 语言。Visual Studio 2010 也是如此，它引入了 C# 4.0。在第 25 章中，你将学习 C# 4.0 中新功能的细节。

### C# 的演变

今天，C# 是一种多范式编程语言。然而，它最初是一门通用的面向对象的语言。

C# 语言的开发团队由 Anders Hejberg 领导，他在 Borland 凭借 Turbo Pascal 和 Delphi 取得了巨大的成功后，于 1996 年加入了微软（并且到目前，他仍是该开发团队的领导）。在当时，微软已经在开发某种后来成为公共语言运行时 `CLR` 的东西。Hejberg 的团队还投入了大量精力消除主流编程语言中存在的共同缺陷。识别这些缺陷极大地有助于 CLR 的建立，并推动了 C# 编程语言的发展。

今天，C# 这个名字（读作 "C sharp"）在使用时，没有人质疑名称中的 "#" 到底意味着什么，因为今天的用户已经习惯了以 "sharp" 结尾（例如 J# 或 F#）。这门编程语言的名字灵感源于音乐符号，其中 "sharp"（升）表示音符的音高应该升高半音。这种灵感并非独有——就像 C++ 编程语言一样，其中 "++" 意味着“比 C 多”。名称中的 "#" 意味着“两行的 ++ —— 换句话说，即 (C++)”，暗示 C# 优于 C++。

### 设计目标

C# 的开发者在流行语言特性和缺陷方面都从 C++ 和 Java 中汲了许多灵感。最初的设计目标是创建一种简单且现代的通用编程语言。开发者还希望创建一种语言，在开发适用于部署在分布式环境中的软件组件时成为一等公民。不那么而易见的事实是，团队的目标是让 C# 适用于托管系统和嵌入式系统，无论是使用大型复杂的操作系统还是使用具有专用功能的微型操作系统。

通过从主流编程语言的缺陷中吸教训，团队专注于创建一种提供软件工程原则支持的语言，例如类型、数组边界检查、对未初始化变量尝试的检测以及自动垃圾收集。

### 简史

C# 的历史和演变与 .NET 框架密不可分。它们的起源具有相同的根，它们的共同演变仍然由推动技术走向未来趋势的力量驱动。

.NET 框架的前身被称为 Common Object Runtime `COR`。可以在地方找到它的痕迹，例如在微软公共对象运行时库 `mscorlib.dll` 的名称中。那时，COR 的类库是用一种名为 Simple Managed C 的托管代码编写的。由 Anders Hejberg 组成的团队开始开发这种新语言，并选择了 C 这个名字，代表“类 C 的面向对象”（C-like Object Oriented）。由于商标原因，微软没有使用这个重载名称，并将其重命名为 C#。.NET 在 PDC 2000 上发布，类库被移植到 C#。根据设计目标，微软决定开始向欧洲制造协会 `ECMA` 提交 C# 语言以及公共语言体系 `CLI` 规范。该提交还由惠尔-Packard `HP` 和英特尔公司共同赞助。大约 16 个月后，结果是 ECMA-334 `2001 年 12 月`，微软还向国际标准组织 `ISO` 开始标准化，C# 在 2003 年通过 ISO/IEC 23270:2003 成为 ISO 标准。2002 年，这一大跃到达了开发者社区。Visual Studio .NET（也称为 VS2002）随着 C# 1.0（以及 Visual Basic）发布。C# 1.0 编译器是 .NET SDK 的一部分，并在 2003 年已修复。

该语言的下一次成功是 C# 2.0，其最受推崇的特性是泛型。在随后的迭代中，Hejberg 从初就加入了这一特性，但还没有足够的经验在 .NET 中实现它。此新版本于 2005 年10 月随 Visual Studio 2005 发布。相关的 ECMA 和 ISO 标准也进行了更新以匹配 C# 2.0 特性。

C# 3 随 Visual Studio 2008 发布，通过引入语言集成查询 `LINQ` 和查询表达式实现了又一次飞跃。LINQ 是一个 .NET 框架组件，为 .NET 添加了数据查询能力。查询表达式表示类似于 SQL 的新数据语法形式。随着 LINQ 引入 C#，该语言发生了从命令式方法向声明式和函数编程的范式转变。与查询表达式并行，语言还包含了被广泛使用的小型（但重要的）特性。C# 编程语言的最新版本是 ISO/IEC 23270:2006 和 ECMA-334 版。

语言的最新版本是 4.0，随 Visual Studio 2010 发布。这标志着它已变成多范式语言。这个新版本引入了支持动态类型的新特性，引入了一种与动态语言交互的极佳方法。C# 现在有了可选参数，这意味着像 Visual Basic 一样简单。C# 5.0 将是什么样？目前微软没有关于团队正在工作的官方信息。但由于每两年计划发布一个新的 Visual Studio 版本，你可以确定团队正在开发令人兴奋的特性并封装到 C# 中。

### 实现

由于 C# 语言是标准化的，微软 Visual C# 并不是唯一的实现，尽管它是最常用的。还有其他实现，通常集成了 C# 语言编译器以及同样标准化的 CLI。以下是著名的 C# 和 CLI 实现的简列表：

- Mono 项目 —— 这被认为是非微软的开源 C# 最佳实现，也是带有 ECMA 规范中所需的框架库的 CLI 完全实现。Mono 长期以来由 Xamarin 领导；截至目前，它由 Novell 领导。
- DotGNU —— Free Source Foundation 属 GNU 项目的一部分，它也提供了开源 C# 编译器和带有 ECMA 规范所需框架库的 CLI。然而，此实现尚未完全完成。
- Shared Source Common Language Infrastructure —— 这是一个微软项目，许可用于教育和研究（原名为 Rotor）。根据 ECMA CLI 规范，C# 编译器和部分所需框架库的共享源代码实现。

### C# 1.0

本节简要概述了该版本包含的特性。这些讨论并不是教你 C#而是假设你具有这种语言的经验，或者至少熟悉任何 .NET 语言。

### 类型系统

C# 有一个统一的类型系统，即 .NET 框架中的公共类型系统。每个类型都有一个祖先，即 `System.Object`。类型系统将数据分为两类：

- 值类型 —— 这些是数据的纯分配，且这些实例完全没有引用标识或比较语义。
- 引用类型 —— 这些具有引用标识的概念。引用类型的每个实例都与其他任何实例本质上是不同的，即使它们内部的数据相同。

两种类型类别都可以由自定义类型扩展。值类型实例背后的值可以通过 C# 语言中隐式的装箱操作转换为对应引用类型的值。之前装箱的引用类型值可以通过拆箱操作转换为值类型实例。这需要显式转换。类型系统允许完全的类型反射和发现。

以下“Hello, World”示例展示了这一事实：

```csharp
using System;

class ExampleClass

{

    static void Main()

    {

        Console.WriteLine("Hello, world!");

    }

}
```
