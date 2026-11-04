
相对顺序) 对同一底层类型的任意两个可空值。这考虑了其中任意一个值可能为 null 的情况（`HasValue` 设置为 `false`）。以下示例展示了这些方法实现的一些真值：

- `null < non-null`（例如，`Nullable.Compare<int>(null, 42) < 0`）
- `null = null`（例如，`Nullable.Compare<int>(null, null) == 0`）
- `non-null > null`（例如，`Nullable.Compare<int>(42, null) > 0`）

## The Uri Type

在高度互联的系统世界中，对端点的寻址非常常见，因此提供一个用于统一资源标识符（URI）的内置原语是合理的。为此目的提供的 Uri 类同时支持绝对 URI 和相对 URI，并有一系列属性可用于查询 URI 的各个部分。下面展示一个基本示例：

```csharp
var url = new Uri("http://bar:8080/foo/quz?answer=42");
Console.WriteLine(url.Host);                 // bar
Console.WriteLine(url.Port);                 // 8080
Console.WriteLine(url.AbsolutePath);         // /foo/quz
Console.WriteLine(url.Query);                // ?answer=42
```

在转义、主机名安全性等方面存在许多复杂性。这也是 Uri 是一个不可变类型的原因之一，因此你不能通过触及各种属性来修改其各部分。要从各部分创建新的 Uri 对象，不要使用像字符串拼接这样的方法（它有很多陷阱）；改用 UriBuilder 类：

```csharp
var builder = new UriBuilder();
builder.Scheme = Uri.UriSchemeFtp; // or use "ftp"
builder.Host = "localhost";
builder.Port = 21;                  // this is the default and will be omitted
builder.Path = "downloads";
builder.UserName = "bartde";
Console.WriteLine(builder.Uri);     // ftp://bartde@localhost/downloads
```

出于安全原因，切勿盲目信任来自用户的输入。如果处理的是 URI，情况也一样。使用 Uri 类及其功能来确保收到的输入是有效的。

## Interacting with the Environment

当今的程序并非独立存在。它们通常需要以多种方式与外部世界交互。虽然我们在第 28 章“Working with I/O”中探讨 I/O，但这里介绍的一种交互形式是：与“the environment”对话。

环境的概念已固化在操作系统中。每个程序都可以访问它，其中包含全局信息以及特定于程序调用的一些信息（如使用的命令行）。在 .NET 中，所有这些信息都通过（静态）类 Environment 提供。

与其在 MSDN 文档中罗列可读取的内容，不如我们仅限于几个示例。首先，这里有一些关于我们正在执行上的物理和虚拟（如 CLR）机器的一般信息：

```csharp
Console.WriteLine("Machine name:   " + Environment.MachineName);
Console.WriteLine("Processor #:    " + Environment.ProcessorCount);
Console.WriteLine("OS version:     " + Environment.OSVersion);
Console.WriteLine("64-bit OS:      " + Environment.Is64BitOperatingSystem);
Console.WriteLine("64-bit process: " + Environment.Is64BitProcess);
Console.WriteLine("Working set:    " + Environment.WorkingSet / 1024 + "MB");
Console.WriteLine("CLR version:    " + Environment.Version);
Console.WriteLine("System32 at:    " + Environment.SystemDirectory);
Console.WriteLine("Not a service:  " + Environment.UserInteractive);
Console.WriteLine("User info:      " + Environment.UserDomainName + "\\"
    + Environment.UserName);
Console.WriteLine("Boot time:      " + (DateTime.Now -
    TimeSpan.FromMilliseconds(
        Environment.TickCount)));
```

其中一些属性返回原始值，其他属性提供更丰富的信息。例如，OSVersion 属性实际上返回一个 OperatingSystem 实例，可以查询版本号、服务包级别等。CLR 版本属性（它只是读取 Version），返回一个 Version 类型的对象，其中包含此类数字所组成的四个部分。

### 64-BIT ODDITIES

在我机器上，查询到的 64 位标志对操作系统返回 True，但对进程返回 False。如果你一直在关注前面的章节，你会记得从 Visual Studio 2010 开始，托管代码可执行文件的默认架构已设置为 32 位。因此，进程在“Windows on Windows”（WOW）32 位仿真模式下运行。

在项目设置的 Build 属性选项卡上将标志更改为 AnyCPU 将导致进程在 64 位机器上以 64 位运行，从而使两个属性都返回 True。是否对你的程序这样做是合适的取决于各种因素。在处理互操作性时，如果对任何架构的测试没有正确执行，你可能会迅速自食其果。毕竟，这也是在 Visual Studio 最新版本中切换 32 位标志的主要原因之一。

除了特定于机器和特定于用户的信息外，我们还可以获取更接近我们进程的信息。这包括环境变量（我们的进程实际上可以影响，并且会被子进程继承）、用于启动进程的命令行等等。

## Tales About the Command Line

你可能会想，为什么 `Environment` 类还要处理提供命令行访问；这不是 `Main` 已经做的事情吗？确实如此，但在各种情况下，将参数数组传递给程序可能过于不便甚至不可能（如果你是加载到某个进程中的组件）。话虽如此，处理命令行参数时需要谨慎。获取它们的不同方式在细微之处有所不同。示例如下：

```csharp
using System;

class Cmdline
{
    static void Main(string[] args)
    {
        Console.WriteLine("CommandLine:");
        Console.WriteLine("  " + Environment.CommandLine);

        Console.WriteLine("Main:");
        foreach (var arg in args)
            Console.WriteLine("  " + arg);

        Console.WriteLine("CommandLineArgs:");
        foreach (var arg in Environment.GetCommandLineArgs())
            Console.WriteLine("  " + arg);
    }
}
```

在三种形式中，第二种在大多数情况下最有意义。第一种和第三种与第二种不同之处在于它们包含了用于启动程序的可执行文件（路径）。例如：

```text
C:\Windows> c:\temp\CmdLine.Exe "Hello, world!" 42
CommandLine:
    c:\temp\CmdLine.Exe  "Hello, world!" 42
Main:
    Hello, world!
    42
CommandLineArgs:
    c:\temp\CmdLine.Exe
    Hello, world!
    42
```

在命令行参数中包含此第一个条目可能出乎意料，这源于底层 Win32 API 的行为方式。

### WHERE DOES MY APPLICATION RUN FROM?

最近，一位朋友问了我这个问题。事实证明这并不像想象中那么容易。使用 "working directory" 显然不是好主意，因为它可能会改变，而且快捷方式也会影响它。我最初的反应之一是使用 GetCommandLineArgs 的第一个元素；然而，它不一定包含完整路径，因为用户可能只是在正确的目录中，从而可以在没有限定路径的情况下启动应用程序。

回答这个问题的正确方法是使用 Assembly 类及其 CodeBase 属性，该属性以字符串形式返回一个 URI，通常使用 file:// 方案。使用 Uri 类，可以将其映射回本地路径。剩下的疑问是使用哪个程序集。Assembly 类上的静态 GetEntryAssembly 方法正是我们需要的：

```csharp
var from = new Uri(Assembly.GetEntryAssembly().CodeBase);
Console.WriteLine(from.LocalPath);
```

同一个 Assembly 对象可用于查询应用程序的版本，这在显示命令行帮助或关于对话框时非常有用。

## Environment Variables

在应用程序之间传递设置和机器或用户特征的最简单方法之一是使用环境变量。使用 Environment 类，可以轻松读取和修改它们。虽然这些环境变量以某种方式被封装，但有时你必须直接根据变量名查询环境：

```csharp
var proc = Environment.GetEnvironmentVariable("PROCESSOR_IDENTIFIER");
```

可以指定一个目标枚举值作为附加参数，以将搜索限制为用户或机器环境，或与当前进程关联的环境块。还存在其他方法来枚举整个环境。

在某些情况下，人们希望像命令行处理器一样展开环境变量。例如，给定字符串 "%WINDIR%\notepad.exe"，你可能希望获取展开后的路径。需要注意的是，一些 I/O API 可以处理未预先展开的字符串，因此根据你的场景可能不需要此操作。尽管如此，以下是实现展开的方法：

```csharp
var notepad = Environment.ExpandEnvironmentVariables(@"%WINDIR%\notepad.exe");
```

在我机器上，这返回 C:\Windows\notepad.exe。需要注意的是，代码也可以写入环境变量。根据目标的不同，此设置会保存在进程的环境块中，或用户的注册表配置单元中，或机器配置单元中。Windows 级别的安全保护机制已到位以防止篡改机器
