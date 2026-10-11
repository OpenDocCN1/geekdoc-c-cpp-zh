
在这个示例中，通过使用 `using` 声明，我们可以引用 `Console` 类而无需完全限定其名称。然而，需要注意的是，截至 C# 10.0，某些系统命名空间被视为特殊情况，包括 `System` 命名空间。它们不需要显式使用 `using` 声明导入。正如原始示例代码中那样，我们可以直接省略 `using System` 声明。这在 C# 10.0 中被称为“隐式 using”、“隐式全局 using”或“隐式命名空间导入”。这是一个“可选启用”功能，我们将在稍后进一步讨论。

## 1.2. 代码阅读 - Hello World 1

`Console` 恰好是我们所说的“静态类”。它并没有真正定义一个“类型”。它仅包含一些“静态方法”和其他静态变量及常量。在这个示例中，我们使用在 `Console` 类中定义的静态方法 `WriteLine()` 向控制台打印文本（因此得名）。再次注意连接静态类名称及其静态方法名称的点语法。

在 C# 和 Java 等语言中，不能定义顶层函数，而顶层函数是 C++、Go、Python 和 JavaScript 等大多数其他编程语言的重要组成部分。作为变通方法，可以使用“静态方法”来替代顶层函数。事实上，C# 和 Java 中的静态方法可以被视为其他编程语言中的函数。它们的主要区别在于语法。

可以通过使用 `using static` 声明来简化使用静态类名称的语法。例如：

```csharp
using static System.Console;

WriteLine("Hello World!!!");
```

通过使用 `using static` 声明将名称 `System.Console` 引入源代码文件，我们现在可以引用 `Console` 的静态方法 `WriteLine()` 而无需限定其名称。

请注意，我们在 `using static` 语句中使用的是 `System.Console` 的全限定名称，而不仅仅是类名，这是 C# 语法所要求的。

这个功能官方称为“静态 using”。作者更喜欢将其称为 `using static` 声明，因为他在编程时就是这样使用它的。术语很重要，但仅在于它们有助于澄清底层概念和/或促进更轻松的沟通时。

在这本书中，我们将只使用那些有意义的术语（尽管它们可能不是“官方”术语）。归根结底，是程序在说话，而不是我们赋予程序各部分的名称。

现在，关于在 `System` 命名空间中定义的 `Console` 类的静态方法 `WriteLine()`，它接受一个 `string` 类型的参数（在此示例中），并将给定的参数打印到终端。"Hello World!!!"（带有一对双引号）是一个“字符串字面量”。它表示 `string` **类型**的一个特定（常量）值。

这就是全部了。如果你构建并运行该程序，它会向控制台打印给定的 `string`（在本例中为 Hello World!!!，不带双引号），并且由于没有其他事情要做，程序终止。

需要注意的是，C# 中的许多语句以分号 (`;`) 结尾。许多类型的语句都需要分号。（此外，“代码块”可以代替分号来结束语句。）

冒着陈述显而易见之事的危险，C# 程序中的语句末尾必须加分号。我们需要使用分号的地方不是行的末尾。（再次重申，C# 中的某些类型的语句需要（显式或隐式）“代码块”，而这类语句不以分号结尾。）

如果你是编程新手，你可能已经感到不知所措。即使是对于这样一个据称“最简单的程序”，只有一行代码，似乎也有很多事情在发生。别担心。你不需要“理解”一切，甚至不需要*任何*东西。☺ 如前所述，知识就是熟悉。随着时间推移接触更多的示例，你会逐渐对什么是“命名空间”、什么是“using”声明、什么是“静态方法”等变得更加自在。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_31_0.png)

还应该指出的是，我们在这本书中不提供这些概念的“字典定义”。你将通过示例学习它们。在适当的上下文中。

当你看到一个苹果时，你知道它是苹果。你不需要知道苹果的确切字典定义来识别它。

## 1.3. 代码阅读 - 一个新的 C# 项目

可以使用 IDE（如微软的 Visual Studio 或 JetBrains Rider）来开发 C# 程序。虽然并非严格必要，但大多数 IDE 和 `dotnet` CLI 工具都使用“项目”来管理 C# 程序及其库依赖项等。

在本课中，我们将使用 `dotnet new` 命令创建一个项目。例如：

```bash
dotnet new console
```

该命令（在空文件夹中）创建一个“控制台应用”项目。.NET 支持多种不同的语言，如 F# 和 Visual Basic，但 C# 是默认的，上述命令在未提供选项的情况下创建的是 C# 项目。

这是一个由 dotnet 版本 6.0.100 创建的示例项目文件（XML 格式）：

```text
hello-universe-0/hello-universe-0.csproj
```

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net6.0</TargetFramework>
        <RootNamespace>hello_universe_0</RootNamespace>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
```

我们在名为 `hello-universe-0` 的目录中运行了 `dotnet new` 命令，它默认使用该名称作为项目名称。运行此命令还创建了一个样板 C# 代码文件，名为 "Program.cs"：

```text
hello-universe-0/Program.cs
```

```csharp
Console.WriteLine("Hello, World!");
```

> 本示例使用 C# 10.0 和 .NET 6。早期版本，例如 C# 9.0/.NET 5，使用不同的模板，例如不使用顶层语句和隐式 System 命名空间 using。我们将在接下来的几课中简要讨论这一点。

### 1.3.1. 解释

C# 项目文件用于各种用途。正如我们稍后将看到的，C# 项目最重要的角色之一是帮助管理（第三方）库依赖项。

项目的另一个用途是在不同的 C# 源代码文件和构建输出等之间设置全局配置。例如，对于这个 "hello-universe-0" 项目，输出设置为 "Exe"，表示该项目旨在生成一个可执行程序，或者一个“应用程序”。

```xml
<OutputType>Exe</OutputType>
```

其目标设置为 "net6.0"（因为我们使用的是 *dotnet* 的 6 版本）。也就是说，我们针对的是 .NET 6 运行时。

```xml
<TargetFramework>net6.0</TargetFramework>
```

*net6.0* 是一个跨平台目标，它提供并使用所有 API 的最大公约数。对于 .NET 的任何先前版本，例如 5.0，你可以将目标框架设置为相应的版本，例如 `net5.0`。如果我们设置目标为，例如，`net6.0-windows`，那么我们还可以使用某些 Windows API（如用于 GUI 编程），但我们的程序可能无法在 Linux 或 Mac 等其他平台上运行。

如上所述，“隐式全局 using” 设置是一个*可选启用*功能。这很可能是由于向后兼容性方面的考虑。你可以按照以下方式在项目文件中启用它。

```xml
<ImplicitUsings>enable</ImplicitUsings>
```

如果你使用 *dotnet* CLI 或 Visual Studio 项目向导来搭建应用程序，此功能默认是启用的。如果你正在开始一个新项目，那么没有理由不使用这个功能。几乎每种编程语言都有类似的支持，除了 C 和 C++ 可能没有。它减少了许多冗余的样板代码。

如果你将 `ImplicitUsings` 标志设置为 `enable`，那么以下系统命名空间将被自动且“全局”导入。

`System`

`System.Collections.Generic`

`System.IO`

`System.Linq`

`System.Net.Http`

`System.Threading`

`System.Threading.Tasks`

我们稍后将在书中使用其中一些命名空间。这种隐式 using 特性 *隐式使用*（这里的双关我承认 :D）了另一个 C# 10.0 的新特性，称为“global using”（全局 using）。在这个上下文中，“global”意味着项目范围。普通的 *导入* 语句仅在给定的源代码文件内有效。在 C# 10.0 之前，如果你在某些源文件中使用了特定的命名空间，就必须在每个源文件中重复导入这些命名空间。现在，你可以在一个文件中使用 *全局导入* 语句导入它们，它们在整个项目的所有文件中都有效。我们稍后会在书中进一步讨论这一点。

生成的项目文件中还有另一件值得注意的事情是 *可空*（Nullable）标志。这启用了“可空引用类型”特性。

```
<Nullable>enable</Nullable>
```

这个特性首次引入于 C# 8 和 9，并且正在成为 C# 编程的标准方式。这也是一个选择性启用（opt-in）特性，出于向后兼容性的原因，但强烈建议你在新项目中始终启用它。（而且，如果你使用 *dotnet new* 或其他工具创建新的 C# 项目，默认情况下它是开启的。）稍后我们会更多讨论这个。

现在，生成的 *Program.cs* 文件包含一个简单的占位代码，即我们之前使用的“Hello World”单行程序。虽然你看不见（显然，如果你仔细想想 icon:grin()），它使用了 *隐式全局 using* 特性。它还使用了“顶层语句”。

如果我们使用旧版本的 dotnet CLI 或其他工具，我们最终会得到以下样板代码。

```
using System;
namespace hello_universe_0
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

注意对比。这个程序与我们刚才看到的单行程序执行完全相同的功能，而且没有更多。然而，它复杂得多了。让我们快速看一下。

程序以常规的 `using System` 声明开始，在 C# 10.0 或更高版本中可以省略。然后，有一个命名空间块：

```
namespace hello_universe_0
{
    // ...
}
```

命名空间块由一对大括号 (`{ }` ) 包围。包含在这个命名空间块内的任何内容都属于这个命名空间。不过，从 C# 10.0 开始，我们也可以为整个源文件声明命名空间。例如，

```
namespace hello_universe_0;
// ...
```

在这种情况下，在此 `namespace` 声明之后在文件中声明/定义的任何内容都属于该命名空间。这在 C# 10.0 中被称为“文件范围命名空间”（file-scoped namespace）。

请注意，命名空间名称（由 `dotnet new` 生成）基于文件夹名称，在本例中为 `hello-universe-0`，但它们略有不同。在 C# 程序中，短横线或减号 (`-`) 不能用作标识符或名称。因此它被转换为下划线符号 (`_` )。

不同的编程语言有不同的规则，但对于大多数 C 风格语言（包括 C#），有效的标识符由一个或多个字母数字字符组成。名称中不允许使用特殊符号，但下划线 `_` 是一个例外。标识符不能以数字字符/数字开头（因为数字字面量，即数字，以数字字符开头）。

另一件值得注意的事情是，在 C# 中，使用“PascalCase”（帕斯卡命名法）作为命名空间名称以及自定义类型名称等更为典型。PascalCase 命名规范，也称为大写“CamelCase”（驼峰命名法），使用一个或多个单词的连接作为名称，其中所有单词的首字母都大写。例如“PascalCase”。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_36_0.png)

另一方面，小写 camelCase 命名规范遵循与 PascalCase 相同的规则，但它使用小写字母开头。例如“camelCase”。在 C# 中，camelCase 名称通常用于变量名称等。

在这个（可选的）命名空间内，`dotnet new console` 命令创建了一个名为“Program”的简单类。

```
class Program
{
    // ...
}
```

类 `Program` 的定义也由一对大括号 (`{` 和 `}`) 包围。C# 是一种 *块作用域* 语言。

这个类 `Program` 恰好包含一个名为 `Main( )` 的单静态方法：

```
static void Main(string[] args)
{
    Console.WriteLine("Hello World!");
}
```

注意语法。它以关键字 `static` 开头，表明正在声明一个静态方法。静态方法就像其他编程语言（如 C/C++、Go、Javascript 或 Python）中的“函数”一样。它与“面向对象编程”（尽管我们使用了“class”）关系不大。

下一个关键字 `void` 表明该方法不返回任何值。然后是函数名称，本例中为 `Main`，后面跟着一对括号 (`(` 和 `)` )。在括号内，我们包含参数列表。当我们调用此方法时，需要为这些参数提供适当的值。对于这个特定方法，列表包含一个字符串数组类型的单个参数（`string[ ]`）。

参数名称对编译器来说通常不重要，但它作为文档使用，因此在创建自己的方法时，建议选取有意义的名称。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_38_0.png)

在这本书中，我们互换使用“parameters”（参数）和“arguments”（实参）这两个术语。有些人喜欢使用像这样的（细微）含义不同的术语。但我们不这样。使用这些术语的语境比使用的精确（英语）词汇及其临时含义（在编程中）更重要。另一个例子是“functions”（函数）与“methods”（方法）。有些人可能坚持它们的“精确”定义。我们不在乎。:)

`Main()` 静态方法很特殊。它是启动程序时的入口点。我们不会显式调用 `Main()` 方法。.NET 运行时，或操作系统，将使用命令行参数（如果有）调用它，我们将在下一课中讨论。参数名称按惯例为 `args`，尽管你可以将其更改为任意有效的变量名。

在这个生成的代码中，`args` 参数从未被使用（尽管意图是让程序员在占位方法体中添加真正的实现），因此我们可以暂时省略它。

```
static void Main()
{
    Console.WriteLine("Hello World!");
}
```

C# 中的 `Main()` 方法应遵循少数预定义的“方法签名”之一。`static void Main(string[] args)` 和 `static void Main()` 对于 `Main()` 方法都是有效的。我们稍后会在书中讨论其他有效签名。

如果我们运行这个生成的程序，

```
dotnet run
```

它会在控制台输出，是的，“Hello World!”。

```
Hello World!
```

## 1.4. 代码阅读 - Hello World 1 重述

在这本书的第一个示例中，我们主要使用了（相对较新的）顶层语句语法。让我们看看它们在更传统的实现中是什么样子。

> 我们将在第二部分深入讨论面向对象编程风格。

使用顶层语句的单行程序 "hello-world-1"，`System.Console.WriteLine("Hello World!!");` 或者 `Console.WriteLine("Hello World!!");`（依赖隐式 System 命名空间导入），等同于以下代码：

`hello-universe-1/Program.cs`

```
class Program {
    static void Main() => Console.WriteLine("Hello World!!");
}
```

如前所述，命名空间块是可选的，我们通常在“主程序”中省略它们。命名空间主要适用于库。这个程序包含一个名为“Main”的类，如生成的样板程序所示。

### 1.4.1. 解释

创建新项目时，我们并不总是需要使用 `dotnet new`。例如，我们可以直接从现有项目复制项目 XML 文件并用作模板。

以下是该项目的 C# 项目文件：

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

这基本上与 *dotnet* 工具生成的模板相同。

我们可以如下运行该程序：

```
dotnet run
```

输出与之前相同：

```
Hello World!!!
```

### 1.4.2. 语法

如果你是“现代 C#”的新手，那么这个程序可能看起来有点奇怪。

这个例子使用了一种较新的语法，称为“表达式体方法”。当方法体只包含一条语句（或者更准确地说，是一个表达式或一个 "return" 语句）时，我们可以省略方法体的代码块，直接用表达式来代替方法体代码块。

它使用了一种与“Lambda 表达式”相似的语法，正如我们稍后在书中会看到的那样，使用“胖箭头”符号 (`⇒`)。这段示例代码等价于以下内容：
