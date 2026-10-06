

# 模块、命名空间与程序入口点

现在这个小型的 F# 程序已经编写完毕，你可能想要构建一个可执行文件。列表 1-1 是一个代码片段，你将需要使用 Visual Studio 来编写、调试和发布产品本节节介绍如何使用 Visual Studio 创建一个 F# 控制台应用程序。图 1-16 显示了如何创建 F# 控制台应用程序。

![](img/63aaf94e22830ab98ce16c5946be8ef6_81_0.png)

**图 1-16** 创建 F# 控制台应用程序

默认的 `Program.fs` 文件包含一个带有 `EntryPoint` 属性的主函数；见图1-17。实际上，F# 不需要定义入口点。对于单个项目，内容会从第一行执行到最后一行。

```
// 在 http://fsharp.net 了解更多关于 F#
// 需更多帮助请参考 'F# Tutorial' 项目。

[EntryPoint]
let main argv =
    printf "%s" argv
    0 // 返回一个整数退出代码
```

**图 1-17** F# 控制台应用程序的默认主函数

如果使用首选的 `EntryPoint` 属性，函数必须满足以下标准：

- 函数必须用 `[<EntryPoint>]` 属性装饰。
- 函数必须位于项目中的最后一个文件。
- 函数必须返回一个整数作为退出代码。
- 函数必须返回一个字符串数组 `string[]` 作为输入。

> 提示：在 F# DLL 中，模块通过静态构造函数进行初始化。这保证了初始化在任何模块值被引用之前发生。另一方面，在 F# 可执行文件中，初始化是在应用程序的入口点执行的，该入口点由 `EntryPoint` 属性定义。建议通过 `EntryPoint` 显式地为 F# 可执行文件定义入口点。

当你向控制台项目添加 F# 项目时，它可能会立即导致你的代码无法编译。新添加的项目是项目系统中的最后一个项。这是列表中的第二个要求。你可以使用右键菜单——见图 1-18——或在开发配置文件设置为 F# 时使用 `Alt+Up/Down Arrow` 键将你的项目移动到项目系统的底部。

![](img/63aaf94e22830ab98ce16c5946be8ef6_82_0.png)

**图 1-18** 上下移动项目的右键菜单

当项目有多个文件时，将代码分为不同的单元是一种良好的编码习惯。F# 提供了模块（module）或命名空间（namespace）将代码划分为小的单元。它们之间存在细微差异，我将在章后面进行讨论。

如果你删除 `Program.fs` 文件中的所有内容并粘贴列表 1-33 所示的代码（该代码没有模块定义），F# 编译器将创建一个匿名模块。它的名称是首字母大写的名称。例如，如果你的代码在 `file1.fs` 中，模块名将是 `File1`。你也可以在文件的第一行显式提供模块名称，如列表 1-88 所示。

**列表 1-88** 模块定义

```
module MyModule

printf "Hello World"
```

模块可以包含其他模块、类型定义、表达式、值或这些者的任何组合，但命名空间不能位于模块内部。嵌套模块需要缩进，并以等号 (`=`) 作为后缀。见列表 1-89。

# 列表 1-89 定义嵌套模块

```
module Print

// 通用打印函数
let x = printf("%A") x

// 定义子模块 NumberPrint
module NumberPrint =
  // 打印 int 的函数
  let printInt = printf("%d")

  // 打印 float 的函数
  let printFloat = printf("%f")

// 定义子模块 StringPrint
module StringPrint =
  // 打印 string 的函数
  let printString = printf("%s")

  // 打印 char 的函数
  let printChar = printf("%c")

// 定义新类型的子模块
module NewTypes =
  // 定义一个二维点
  type Point2D = float32*float32

// 调用打印函数
NumberPrint.printFloat 4.5
NumberPrint.printInt 2
StringPrint.printChar 'c'
StringPrint.printString "abc"
```

如果你只想持有函数和变量，从 F# 的角度来看，命名空间和模块是相同的。如果 F# 项目是要从 C# 项目打开的库，那么命名空间是更好的选择。从 C# 侧看时，模块是一个静态类。通过将模块名和函数名结合使用，你可以引用在不同模块定义的函数。如果你想引用模块内部的函数，可以使用 `open` 关键字打开该模块，或用 `AutoOpen` 属性装饰模块，这可以自动打开模块，本质上导致函数被放置在全局命名空间中。见列表 1-90。

```f
module Print
// 通用打印函数
let print x = printf("%A") x

// 自动打开 NumberPrint
[-AutoOpen]
module NumberPrint =
    // 打印 int 的函数
    let printInt = printf("%d")

    // 打印 float 的函数
    let printFloat = printf("%f")

module StringPrint =
    // 打印 string 的函数
    let printString = printf("%s")

    // 打印 char 的函数
    let printChar = printf("%c")

// 调用打印函数
printFloat 4.5
printInt 2
printChar 'c'
printString "abc"
```

> 提示：在 FSI 中，`open` 语句必须位于模块定义之后。

```
module Print
// 通用打印函数
let print x = printf("%A") x

// 自动打开 NumberPrint
[-AutoOpen]
module NumberPrint =
    // 打印 int 的函数
    let printInt = printf("%d")

    // 打印 float 的函数
    let printFloat = printf("%f")

module StringPrint =
    // 打印 string 的函数
    let printString = printf("%s")

    // 打印 char 的函数
    let printChar = printf("%c")

// 调用打印函数
printFloat 4.5
printInt 2
printChar 'c'
printString "abc"
```

> 提示：在 FSI 中，`open` 语句必须位于模块定义之后。

`RequiredAccess` 属性表示必须指定模块名。

# 列表 1-91 使用 RequiredAccess 属性

```fsharp
[<RequiredAccess>]
module MyModule =
 let f() = printf("%f")

// 引用函数
MyModule.f()
```

模块可以通过创建新模块进行扩展。命名空间中的项、类型、表达式、值通常是可用的。列表 1-92 显示了，并且通常代码更少。

> 提示：命名空间内的模块需要等号 (`=`)。

```fsharp
namespace CollectionExtensions

open System.Generic

// 扩展方法
module Array =
 n -> n
```

如前所述，如果 F# 代码需要从其他语言引用，命名空间是更好的选择。命名空间可以包含模块和类型定义。列表 1-94。

# 列表 1-94 使用命名空间

```fsharp
namespace Space

// 定义 3D 点
type Point3D = float32 * float32 * float32

// 定义命名空间内的模块
module HelloWorld =
  let msg = "%Hello"

// 下行无法编译，因为命名空间
// let a = 2
```

> 提示：FSI 不支持命名空间。

空文件在多文件项目中无法编译。如果项目包含多个文件，源代码开头必须有命名空间或模块。

![](img/63aaf94e22830ab98ce16c5946be8ef6_86_0.png)

# 使用 F# 进行面向对象编程

面向对象编程（OOP）已经取得了巨大的成功。许多现代业务系统是通过应用 OOP 概念设计和实现的。我不会讨论 OOP 的优点，作为 C# 开发者，你心里可能有很多优点。

F# 是一种多范式语言，支持 OOP。基本上你在 C# 中可以做的一切在 F# 中都可以，而且代码更少。我将遵循第一章的方法，将 C# 代码转换为 F#：列表 2-1 显示了一个 C# Point2D 类，它表示二维（2D）表面上的点。它展示了属性、静态和非静态字段、属性以及成员方法。转换不仅将进行直接翻译，还将执行一些额外工作以演示相关的 F# 概念。

列表 2-1 C# Point2D 类定义

```csharp
// 定义二维点
[Debugger("{X}, {Y}")]
public class Point2D
{
    // 定义计数器
    private static int count = 0;
    // 定义原始点
    public readonly Point2D OriginalPoint = new Point2D(0, 0);

    // 定义带有显式后台字段的 X 属性
    private double x;
    public double X
    {
        get { return this.x; }
        set { this.x = value; }
    }

    // 定义 Y 属性
    public double Y { get; set; }
}
```
