
图 1.2：创建新项目的对话框

## 配置你的新项目

`Console App (.NET Core)`

![](img/b18af4770e9195628243fa73ff1469b4_45_1.png)

图 1.3：新项目对话框

# 第 1 章：引入 C#

5. 一旦项目创建，你就应该看到一个 `Program.cs` 文件，如图 1.4 所示。

![](img/b18af4770e9195628243fa73ff1469b4_46_0.png)

图 1.4：显示 `Program.cs` 文件的对话框

- 6. 使用调试->不调试启动菜单运行生成的程序。这将显示命令行窗口并带有输出 1.2 所示文本，但第一行将仅显示“Hello World!”

7. 修改 `Program.cs` 以匹配代码清单 1.1。

8. 重新运行程序以查看输出 1.2 所示的输出。

```
> Hello. My name is Inigo Montoya.More output
按任意键关闭此窗口 . .
```

使用 IDE 的一个重要特性是它支持调试。要尝试一下，请在 Visual Studio 或 Visual Studio Code 中遵循以下额外步骤：

- 1. 打开 `Program.cs` 后，

- 2. 打开 `Program.cs` 后，

- 3. 打开 `Program.cs` 后，

## 语言对比：Java——文件名必须为类名

在 Java 中，文件名必须遵循类名。在 C# 中，经常遵循这一约定，但并非强制。在 C# 中，可以在一个文件中包含两个类，甚至一个类可以跨越多个文件。

虽然不是一定需要，但通常会包含一个配置文件作为 C# 项目源代码的一部分。项目内容会根据应用程序类型和 .NET 框架的不同而异。然而，它至少识别了包含哪些文件、要构建什么类型的应用程序（控制台、Web、移动、测试项目等）、支持哪个 .NET 框架，以及调试或启动应用程序所需的潜在设置，以及代码可能依赖的其他依赖（称为库）。例如，在本节创建的简单 .NET Core 应用程序项目文件位于代码清单 1.2。

代码清单 1.2：示例 .NET Core 控制台项目文件

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>
</Project>
```

由 `dotnet build` 创建的编译输出是一个程序集 `HelloWorld.dll`。扩展名代表动态链接

- 1. 注意，如果你使用 Microsoft .NET Framework 创建控制台程序，编译代码被放在 `HelloWorld.exe` 文件，只要计算机安装了 Microsoft .NET Framework，就可以直接执行它。

库（DLL），在 .NET Core 中，即使是像这样的控制台程序，所有程序都具有 .dll 扩展名。默认情况下，.NET Core 应用程序的编译输出放置在子目录（`./bin/debug/netcoreapp3/`）中。使用 Debug 目录是因为默认配置是调试。此配置使输出针对调试进行了优化，而不是优化性能。编译输出不会独立运行。相反，它需要 CLI 来托管代码。对于 .NET Core 应用程序，这需要使用 `dotnet.exe` 进程（Linux 和 Mac 上为 `dotnet`）作为应用程序的宿主。这就是为什么使用 `dotnet run` 命令执行程序。尽管如此，有一种方法可以生成一个包含必要运行时文件的独立可执行文件，但这需要安装 dotnet 运行时——请参阅“高级主题：发布独立执行文件”。

## 高级主题

## 发布独立执行文件

可以输出一个可以独立于 `dotnet` 命令运行的独立可执行文件。要实现这一点，请运行 `dotnet publish` 命令并带有 `--runtime (-r)` 参数，该参数指定了输出兼容的目标平台（操作系统）。例如，在大多数 Linux 平台上，你可以在与 `CSPROJ` 文件相同的目录中使用 `linux-x64`：

```
dotnet publish --runtime linux-x64
```

执行此命令将创建一个目录（`./bin/Debug/netcoreapp3.1/linux-x64/publish/`），该目录包含了无需先安装运行时即可运行 `HelloWorld` 控制台程序的所有文件。要执行 `HelloWorld` 程序，如果当前目录不是发布目录，请指定路径：

```
.bin/Debug/netcoreapp3.1/linux-x64/publish/HelloWorld
```

（在 Windows 上，可执行文件名为将包含 .exe 扩展名，但在运行程序时不需要指定它。）

请注意，生成的可执行文件将只能在 `linux-x64` 平台上运行。你需要为你目标的每个平台执行 `dotnet publish` 命令。其他平台的常见运行时标识符包括 `win-x64` 和 `osx-x64`（完整列表请参阅 http://itl.tc/ridcatalog）。

也可以将独立可执行文件发布到单个文件中（而不是通常所需的约 200 个文件）。对于单个可执行文件，在命令末尾附加 `/p:PublishSingleFile=true`：

```
dotnet publish --runtime linux-x64 -p:PublishSingleFile=true
```

关于 `-p` 参数的更多信息出现在第 10 章。

## 核心 C# 源代码

与本书相关的源代码包含一个 `EssentialCSharp.sln`，它将所有章节的代码组合在一起。可以使用 Visual Studio 或 dotnet CLI 对源代码进行构建、运行和测试。

也许简单的方法是将源代码粘贴到本节早些创建的 `HelloWorld` 程序中，然后执行源代码。或者，源代码包含了每个章节的项目文件以及一个菜单，在执行程序时可以从该菜单选择要运行的列表项（listing），如接下来的两个章节所示。

## 使用 Dotnet CLI

要使用 dotnet CLI 构建并执行代码，请打开命令提示符，并将当前目录设置为与 `EssentialCSharp.sln` 文件相同的目录。从那里使用 `dotnet build` 命令编译所有项目。

要运行特定项目的源代码，导航到包含项目文件的目录并运行 `dotnet run` 命令。或者，从任何目录，使用 `dotnet run -p <project>` 命令，其中项目文件是你尝试执行的文件的路径（例如，`dotnet run -p .\src\Chapter01\Chapter01.csproj`）。执行后，程序将提示要执行哪个列表项，然后继续执行该项。

许多列表项在 `Chapter?? Tests` 目录中有相应的单元测试，其中 `[?]` 表示章节号。要执行测试，请从要执行的测试所在的项目目录运行 `dotnet test`（或从 `EssentialCSharp.sln` 文件所在运行相同的命令来执行所有测试）。

- 本书提供的源代码（以及一些与 C# 早期版本相关的章节）可以在 //IntelliText.com/EssentialCSharp 下载。你也可以直接从 GitHub 下载代码：https://github.com/IntelliText/EssentialCSharp。

## C# 语法基础

### 使用 Visual Studio
打开解决方案文件后，使用“Build->Build Solution”（生成->生成解决方案）菜单用 Visual Studio 编译代码。在执行源代码之前，你需要通过将关联项目设置为“启动项目”来选择要执行哪个项目。例如，要执行第 1 章中的示例，你会右键点击 `Chapter01` 项目并选择“Set as StartUp Project”（设为启动项目）。如果没有选择正确的项目，在执行时指定列表项编号将导致出现带有消息“Error, could not run the Listing...”的异常。

一旦你选择了正确的项目，就可以从“Debug->Start Without Debugging”（调试->不调试启动）菜单运行项目。或者，如果你想调试项目，可以使用“Debug->Start Debugging”（调试->开始调试）。运行后，程序将提示你想要执行的列表项（例如 18.33）。如前文所述，你只能输入设为启动的项目中的列表项。

许多列表项都有相应的单元测试。要执行测试，打开测试项目并导航到要执行的列表项对应的对应位置。从那里，右键点击测试方法并选择“Run Tests”（Ctrl+R, T）或“Debug”（Ctrl+R, T）。

## C# 语法基础
为了启用编译器，某些词具有特殊状态。这些被称为关键字的词提供了意义。在 C# 中考虑这些关键字。由于这些规则，编译器会发出错误。在 `HelloWorld` 程序中，关键字是组织的示例。编译器使用关键字来解释结构。

## C# 关键字

| 1.1 | | |
| :--- | :--- | :--- |
| abstract | enum | stackalloc |
| alias | event | string |
| as | explicit | struct |
| async | finally | switch |
| await | false | object |
| base | fixed | order |
| break | group | try |
| bool | get | this |
| byte | in | uint |
| char | goto | unsafe |
| class | global | volatile |
| const | internal | virtual |
| continue | int | void |
| catch | long | ref |
| default | remove | var |
| delegate | into | where |
| descending | is | when |
| do | join | set |
| double | let | while |
| else | lock | short |
| dynamic | lock | sizeof |
| decimal | namespace | yield |
| event | new | typeof |
| extern | null | keyword (n) |

## C# 语法基础

在 C# 1.0 之后，引入了新的关键字。然而，后续版本的某些构造使用了上下文关键字，它们仅在指定位置具有意义。在这些位置之外，上下文关键字没有意义。

## 标识符

与其他语言一样，C# 包含标识符来识别构造。在列表 1.1 中，`HelloWorld` 和 `Main` 是标识符的示例。标识符随后会被分配给构造，因此开发者分配的名称是有意义的，而不是任意的。

选择简洁且指示性名称的能力是优秀程序员的重要特征，因为这意味着结果更容易被理解和重用。清晰度和一致性非常重要，以至于框架设计指南（http://bitly/dotnetguidelines）建议不要在标识符中使用缩写。

标识符有两种大小写格式。Pascal 命名法（称为 PascalCase），.NET 框架创建者如是称为

9. 存在一些罕见且不幸的不兼容之处，例如：
* C# 2.0 使用 语句实现 `IDisposable`，而不是简单地使用 `Dispose()` 方法。
* 某些罕见的泛型表达式在版本之间存在差异。例如，C# 1.0 中的 `F(G<A,B>(B>7))`，但在 C# 2.0 中，它意味着调用泛型 `G<A,B>` 并传入参数 7，然后将结果传递给 F。

# 第 1 章：引入 C#

在 Pascal 编程语言中，流行的做法是将标识符名称中每个单词的首字母大写；示例包括 `ComponentModel`、`Configuration` 和 `HttpFileCollection`。正如 `HttpFileCollection` 在 HTTP 中所示的，当使用超过两个字母的缩写词时，仅首字母大写。第二种格式是驼峰命名法（下称为 camelCase），遵循相同的约定，不同之处第一个字母是小写的；示例包括 `firstName`、`iStream` 和 `DreadPirateRoberts`。

### 指南
- 在命名标识符时，**优先**考虑清晰性而非简洁。
- **不要**在标识符名称中使用缩写或收缩形式。
- 除非被广泛接受，否则**不要**使用任何缩写，如果使用，请保持一致性。

请注意，虽然下划线是合法的，但标识符名称中通常没有下划线、连字符或其他非字母数字字符。此外，C# 不遵循其前身的匈牙利命名法（即在名称前加上数据类型的缩写）。这种约定避免了在数据类型更改时必要的重命名，也避免了在使用匈牙利命名法时未调整数据类型前缀所导致的不一致。

在少数情况下，某些标识符（如 `Main`）在 C# 语言中具有特殊含义。

### 指南
- 对于两个字母的缩写词，两个字母都要大写，驼峰命名标识符的首单词除外。
- 对于三个或更多字母的缩写词，仅大写第一个字母，驼峰命名标识符的首单词除外。
- **不要**大写驼峰命名标识符开头缩写中的任何字符。
- **不要**使用匈牙利命名法（即不要在变量名中编码其类型）。

## 高级主题

### 关键字
虽然很少见，但如果关键字包含 @ 作为前缀，则可以作为标识符。例如，你可以将本地变量命名为 `@return`。同样（尽管它不符合 C# 标准的大小写规范），可以将方法命名为 `@throw`，并在后面跟上括号：`@throw()`。

Microsoft 的实现中还有四个未文档的关键字：`__arglist`、`__makeref`、`__reftype` 和 `__refvalue`。这些关键字仅在罕见的互操作场景中需要，在所有实际用途中你可以忽略它们。请注意，这四个特殊关键字以两个下划线开头。C# 的设计者保留在未来版本中将任何以两个下划线开头的标识符变为关键字的权利；为了安全，请避免自己创建此类标识符。

# 类型定义

C# 中的可执行代码出现在类型定义中，最常见的类型定义以 `class` 关键字开始。类定义是代码中通常以 `class` 标识符 `{ ... }` 开始的部分，如列表 1.3 所示。

列表 1.3：基本类声明

```
class HelloWorld
{
    ...
}
```

用于该类型的名称（在本例中为 `HelloWorld`）可以变化，根据约定，它必须是 PascalCase。因此，对于此示例，其他可能的名称有 `HelloInigoMontoya`、`Hello` 或简单的 `Program`。（当类包含下文描述的 `Main()` 方法时，使用 `Program` 是一个值得遵循的良好约定）

# 指南
- 使用名词或名词短语来命名类。
- 所有类名均使用 PascalCase 驼峰命名法。

通常，程序包含多个类型，每个类型都包含方法。

# 第 1 章：引入 C#

## Main 方法

## 初学者主题

## 什么是方法？
在实践中，C# 中的方法是由方法声明（例如 `static void Main()`）引入的命名代码块，并（通常）后跟大括号内的零或多个语句。用于执行计算和/或操作。像面语言中的段落一样，方法提供了一种结构化和组织代码的方法，使其具可读性。更重要的是方法可以重复使用并从多个地方调用，从而避免了重复代码的需求。方法声明引入了方法，并定义了方法名称以及在方法之间传递的数据。在列表 1.4 中，`Main()` 后接 `{ ... }` 是一个 C# 方法的示例。C# 开始执行的位置是方法，它以 `static Main()` 开始。当你在控制台输入 `dotnet run` 时，程序启动，解析 `Main` 的位置并执行列表 1.4 所示的第一条语句。

列表 1.4：拆分 HelloWorld

```
class HelloWorld
{
    static void Main() { /* 方法声明 */
    {
        System.Console.WriteLine("Hello, My name is Inigo");
    }
}
```

虽然 `Main` 方法

## 高级主题

## 方法的声明
`Main` 方法声明是一个执行操作的代码块。在 C# 中，方法通过返回类型、名称和可选的参数列表定义。列表 1.5 显示了带参数的方法。

列表 1.5：带参数和返回类型的方法

```c
static int Main(string[] args)
{
    // ...
}
```

C# 开始执行的位置是方法，它以 `static void Main()` 开始。当你在控制台输入 `dotnet run` 时，程序启动，解析 `Main` 的位置并执行列表 1.4 所示的第一条语句。虽然 `Main` 方法声明可以发生变化，但 C# 始终使用大括号作为方法体。

## 高级主题

## 无分号的语句
C# 中的许多编程元素以分号结束。一个不包含分号的示例是 `switch` 语句。因为 `switch` 语句始终包含大括号，所以 C# 不需要在该语句后的分号。事实上，代码块本身也被视为语句（它们由语句组成），并且不需要使用分号来结束。同样，在某些情况下（例如使用声明时），分号作为后缀出现，但它并不是语句。

## 语句和语句分隔符

`Main` 方法包含单个语句 `System.Console.WriteLine()`，它用于向控制台写入行文本。C# 通常使用分号来表示语句的结束。声明变量、控制程序流和调用方法都是语句的典型用途。

创建换行符并不分隔语句，你可以将多个语句放在同一行，C# 编译器将把该行解释为多条指令。例如，列表 1.6 在单行内包含两个语句，组合在一起可以显示 Up 和两个独立的行。

列表 1.6：单行多条语句

```
System.Console.WriteLine("Up");System.Console.WriteLine("Down");
```
