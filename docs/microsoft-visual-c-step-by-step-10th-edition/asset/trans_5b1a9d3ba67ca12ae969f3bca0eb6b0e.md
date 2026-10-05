

```
Console.WriteLine(
```

> > **提示**
你可以选择提示中的上下方向键来滚动查看 `WriteLine` 的不同重载。

+   6. 输入 `);` ，语句现在应该像这样：

```
Console.WriteLine();
```

+   7. 移动光标，在 `WriteLine` 方法后的左右括号之间输入字符串 "Hello YourName"（包括引号）。

现在语句看起来像这样：

点击此处查看代码图像

```
Console.WriteLine("Hello YourName");
```

> > **提示**
养成在填充内容之前先输入成对字符的习惯，例如圆括号 `( )` 和大括号 `{ }`。。如果你等输入完内容后再输入闭合字符，很容易忘记它。

### IntelliSense 图标
当你在类名后输入句点时，IntelliSense 会显示该类的每个成员的名称。在每个成员名称的左侧有一个描述该成员类型的图标。常见的图标及其类型包括如下：

| 图标 | 含义 |
|---|---|
| ⚙ | 方法（在第 3 节中讨论） |
| 👥 | 类（在第 7 节中讨论） |
| 📦 | 结构体（在第 9 节中讨论） |
| 📋 | 枚举（在第 9 节中讨论） |
| ♀ | 扩展方法（在第 12 节“处理继承”中讨论） |
| 📖 | 接口（在第 13 节“创建接口和抽象类”中讨论） |
| 📂 | 委托（在第 17 节“介绍泛型”中讨论） |
| ⚡ | 事件（在第 17 节中讨论） |
| {} | 命名空间（在本章后续章节讨论） |

在不同的上下文中输入代码时，还会看到其他 IntelliSense 图标出现。

## 生成并运行控制台应用程序

+   1. 打开**生成 (Build)** 菜单并选择**生成解决方案 (Build Solution)**。

这将编译 C# 代码，生成一个你可以运行的程序。输出窗口出现在代码和文本编辑器窗口下方。

> > 提示
如果输出窗口没有出现，请在视图 (View) 菜单上选择输出 (Output) 以显示它。

在输出窗口中，你应该能看到类似下面的消息，指示程序正在编译的情况：

点击此处查看代码图像

```
Build started...
1------ Build started: Project: TestHello, Configuration: Debug
Any CPU
1>TestHello -> C:\Users\student\Documents\MicrosoftPressVCS\Chapter 1\TestHello\nTestHello\bin\Debug\net6.0\TestHello.dll
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped
=========
```

如果你犯了任何错误，它们将在错误列表 (Error List) 窗口报告。下面的图像显示了如果你忘记在 WriteLine 语句的文本 Hello World 之后输入引号会发生什么。注意，单个错误有时会导致多个编译器错误。

```
Program.cs - TestHello.Program - Main(string) args
1 using System;
2 using System.Collections.Generic;
3 using System.Linq;
4 using System.Text;
5 using System.Threading.Tasks;
6 
7 namespace TestHello
8 {
9 internal class Program
10 {
11 
12 static void Main(string[] args)
13 {
14 Console.WriteLine("Hello John");
15 }
16 }
17 }
```

```
Output
Show output from: Build
-- Rebuild All started: Project: TestHello, Configuration: Debug Any CPU -----
C:\TestHello\TestHello\Program.cs(13,31,13,31): error CS1010: newline in constant
C:\temp\TestHello\TestHello\Program.cs(14,6,14,6): error CS1002: expected
C:\temp\TestHello\TestHello\Program.cs(15,6,15,6): error CS1002: expected
-- Rebuild: 0 succeeded, 3 failed, 0 skipped
```

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_67_0.png)

### 提示

注意，当你输入无法编译的代码行时，Visual Studio 会其下方显示红色波浪线。要直接跳转到引起错误的行，双击错误列表窗口中的项目。

如果你仔细遵循了之前的指令，应该没有错误或警告，且程序应该可以成功生成。

> 提示
在生成之前不需要显式保存文件，因为“生成解决方案”命令会自动保存它。代码和文本编辑器窗口上方标签页中，文件名后的星号表示该文件自上次保存以来已更改。

2. 在**调试 (Debug)** 菜单上，选择**无调试启动 (Start Without Debugging)**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试 (Start Debugging)”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

（此处处此处重复重复重复，重复按任意键内容）

3. 在调试 (Debug) 菜单上，选择**无调试启动**。

打开一个命令行窗口，程序运行。显示出“Hello World!”和“Hello YourName”消息。程序现在会等待你按任意键。

```
C:\WINDOWS\system32\cmd.exe
Hello John
Press any key to continue . . . _
```

> 注意
“Press any key to continue” 提示是由 Visual Studio 生成的。你没有编写任何代码来实现这一点。如果你使用“启动调试”运行程序，程序现在会等待你按任意键。

## 使用命名空间

你目前看到的示例是一个非常程序。然而，小程序很快就会变成更大的程序。随着程序的增长，会出现两个问题：

- 理解和维护大程序比理解小程序要困难。

