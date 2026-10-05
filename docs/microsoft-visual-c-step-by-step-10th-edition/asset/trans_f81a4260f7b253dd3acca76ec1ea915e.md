
7. 打开“文件”（File）菜单并选择“新建”（New）以创建一个新的空白文件。

8. 在文件中添加以下文本：

点击此处查看代码图片

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exec</OutputType>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
</Project>
```

这是一个 C# 项目文件的示例。.NET CLI 工具将使用此文件将你的代码编译为可执行应用程序。该文件的内容指定了要创建的可执行文件类型（EXE 文件）以及用于构建和运行应用程序时使用的 .NET 运行时版本（.NET 6.0）。在本书随后的章节中，你会看到你可以创建其他类型的可执行文件，例如动态链接库 (DLL)，它们可以被许多应用程序共享。

9. 打开“文件”（File）菜单，选择“另存为”（Save As），并将文件命名为 `Hello.csproj`，保存到你“文档”（Documents）文件夹下的 `Microsoft Press\VCSBS\Chapter1\HelloWorld` 文件夹中。

> 注意
> C# 项目文件应具有 .csproj 后缀。

10. 关闭记事本，返回命令提示符窗口，运行以下命令进入 HelloWorld 文件夹：

```
cd HelloWorld
```

11. 运行 `dir` 命令并验证文件夹是否包含 `HelloWorld.csproj` 和 `Program.cs` 两个文件。

# 管理员：命令提示符

```
C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld>dir
Volume in drive C is Windows
Volume Serial Number is DABB-41AS

Directory of C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld
05/05/2021  04:05 PM    <DIR>
05/05/2021  04:05 PM    <DIR>
05/05/2021  04:02 PM                167 Hello.csproj
                                        41 Program.cs
05/05/2021  03:52 PM                208 2 File(s)
Dir(s)         82,347,448 bytes free

C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld>_
```

12. 使用以下命令构建并运行应用程序：

```
dotnet run
```

在 .NET CLI 工具下载并安装一个或两个额外库以及开发证书期间，你会看到几条消息。最后，你应该看到 `Hello World!` 字样。这是你程序的输出。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_49_0.png)

13. 重复 `dotnet run` 命令。这一次，.NET CLI 工具不需要下载任何库或证书，因为它们已经安装过了。相反，你应该只会看到 `Hello World!` 消息。

Hello World! 应用程序编写起来快速简单，但你必须添加项目文件，以便 .NET CLI 工具理解如何构建和运行程序。这种方法对于简单的应用程序是行的，但更复杂的系统可能需要大量的配置以及相应的复杂的项目文件。例如，一个应用程序可能需要几个不同的库，项目文件必须指定这些库的名称以及 .NET CLI 工具应该从哪里下载它们。幸运的是，.NET CLI 可以自动化处理许多复杂性，或者至少停止手动管理。

在接下来的练习中，你将创建另一个版本的 Hello World!，但这次你将让 .NET CLI 工具为你生成项目文件。

# 使用 .NET CLI 工具构建和运行 C# 项目

- 1. 在命令提示符窗口中，返回“文档”文件夹下的 `Microsoft Press\VCSBS\Chapter 1HelloWorld` 文件夹。

点击此处查看代码图片

```
cd C:\Users\YourName\Documents\Microsoft Press\VCSBS\Chapter 1
```

- 2. 创建一个名为 `HelloWorld` 的新文件夹。

```
mkdir HelloWorld
```

- 3. 进入 HelloWorld 文件夹。

```
cd HelloWorld
```

- 4. 运行以下命令创建一个新的控制台应用程序。`console` 是 .NET CLI 用于生成应用程序的模板名称。

```
dotnet new console
```

当 .NET CLI 为新的控制台应用程序创建 C# 项目文件时，你会看到几条消息。

```
C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld2>dotnet new console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld2\HelloWorld2.csproj
HelloWorld2.csproj
Determining projects to restore...
Restored: C:\Users\student\Documents\Microsoft Press\VCSBS\Chapter 1\HelloWorld2\HelloWorld2.csproj (in 0 ms).
restore succeeded.
```

# 注意

.NET CLI 还提供了其他几种模板用于创建其他类型的应用程序，例如 ASP.NET Web 应用程序或 Windows Forms 图形应用程序。

- 5. 输入 **dir** 显示 HelloWorld2 文件夹的内容。

你会看到一个名为 `HelloWorld2.csproj` 的项目文件、一个名为 `Program.cs` 的 C# 代码文件以及一个名为 `obj` 的文件夹。`obj` 文件夹包含 .NET CLI 用于编译和运行应用程序的配置文件和其他数据。

- 6. 启动记事本。然后打开“文件”（File）菜单，选择“打开”（Open），并打开 **HelloWorld2** 文件夹中的 **HelloWorld2.csproj** 文件。你可能需要将文件类型下拉列表框设置为 **所有文件**（All Files）才能看到 HelloWorld2 文件夹中的文件。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_52_0.png)

7. HelloWorld2.csproj 文件的内容应该如下：

点击此处查看代码图片

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
```

```
</Project>
```

此项目文件与你在上一个练习中手动创建的相同。

8. 打开 `Program.cs` 文件。它应该包含以下代码：

点击此处查看代码图片

```
using System;

namespace HelloWorld
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

这个程序文件比你之前创建的复杂一点，但的功能完全相同。`Program.cs` 定义了一个名为 `Program` 的类，其中包含一个方法。在 C# 中，每个方法都定义在类或结构内部。`Main` 方法指定了程序的入口。该方法应定义在 `Program` 类中作为静态方法，否则 .NET 框架可能无法将其识别为起点。你将在第 3 章“编写方法”中学习更多相关知识。

此时，你可能在想：“我们在上一个练习中并没有创建 `Program` 类或 `Main` 方法”。在最新版本的 C# 中，如果你像第一个练习所示有一个简单的应用程序，C# 编译器会创建自己的 `Main` 方法（你可以将其理解为编译器生成的）。然而，.NET 提供的控制台模板总是创建一个 `Program` 类和 `Main` 方法。此外，其他类型的应用程序使用不同的方式标记程序的入口。这些类型应用程序模板会生成相应的启动代码。对于 `using` 语句和命名空间定义，你将在本章稍后的部分中学习这些内容。

9. 不要更改任何内容；关闭记事本并返回命令提示符。
10. 编译并运行应用程序。这是你在上一个练习中使用的命令。

```
dotnet run
```

屏幕上应该显示 `Hello World!` 消息。

