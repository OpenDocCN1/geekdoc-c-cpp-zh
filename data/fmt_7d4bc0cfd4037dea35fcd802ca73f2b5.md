
| Static (静态) | 静态方法是一个类方法，这意味着它属于类而不是属于从该类创建的单个对象。将 `Main` 声明为静态的以便 .NET 框架运行时在应用程序启动时执行它是至关重要的。 |
| --- | --- |
| Void | 声明的方法不返回任何值。 |

# 编译（生成）控制台应用程序

你可以按键盘上的 `Shift + B` 来生成应用程序，如果存在错误，它们将列在错误列表中，可以通过开发环境底部的标签页访问。你可以通过按 `F5` 轻松地运行应用程序。

| 描述 | 文件 | 行 | 列 |
| --- | --- | --- | --- |
| 1 名称 '...' 在上下文中文中不存在 | `Program.cs` | 13 | 15 |
| 2 隐式类型局部变量必须初始化 | `Program.cs` | 14 | 17 |
| 3 缺少分号 | `Program.cs` | 14 | 18 |

![](img/00a5dd1bec9fd78e4d7f7685508abf5_43_0.png)

# C# 初学者入门

## 如何创建控制台应用程序

1. 打开 Visual Studio。
2. 在菜单中选择 **文件-新建项目**（`File-New Project`）。
3. 在左侧树形中选择 **C#**。
4. 在模板列表中选择 **控制台应用程序**（`Console Application`）。
5. 在 **名称** 字段中为项目命名。
6. 确保 **解决方案目录** 已勾选。
7. 点击 **确定** 按钮，让 Visual Studio 设置带有必要文件、文件夹和引用的项目。

## C# 初学者教程

请注意，你可以在代码中添加注释，这些注释在构建应用程序时会被忽略。方法是在代码行开头使用双斜杠（`//`），或者如果是较长的注释，可以使用斜杠星号将其包围（`/* 这是一个注释 */`）。

```csharp
// 添加换行符
Console.WriteLine();
// 向控制台写入一行文本，但不带换行符
Console.Write("A line of text");
// 使用 \n 命令在新行行写入文本
Console.WriteLine("\Another line of text");
// 使用 \t 分两列写入文本
Console.Write("\t{tagName}");
/* 通过将名称插入字符串中来格式化字符串。你可以通过添加更多花括号、增加索引数字并添加逗号分隔的列表值来插入多个字符串。 */
Console.WriteLine("Welcome {0}!", "Jonas");
// 创建固定长度列
Console.WriteLine("{0,2}{1,4}yo", "Jonas", 45);
```

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_45_0.png)

### 从控制台窗口读取用户输入

当从控制台读取用户输入时，你可能想存储该值以便以后使用。存储值的简单方法是使用 `var` 关键字后跟变量名，通过该变量你可以访问存储的值（你将在后续章节中学习更多关于的知识）。

```csharp
// 提示用户输入名称
Console.Write("Enter your name: ");
// 将名称存储在变量中以后使用
var name = Console.ReadLine();
// 如果用户输入了 Jonas，则向控制台写入：Welcome Jonas!
Console.WriteLine("Welcome {0}!", name);
```

### 在调试时保持控制台窗口打开

你可以调用 `ReadKey` 方法在输出最后一行内容后保持控制台窗口打开。方法中的 `true` 值可以防止字符被输出到控制台。

```csharp
Console.WriteLine("\nPress any key to exit");
Console.ReadKey(true);
```

### 练习：创建你的第一个控制台应用程序

在本次练习中，你将创建一个新的控制台应用程序，该程序将提示用户输入名称“Enter your name: ”，并将输入的名称存储在名为 `Name` 的变量中。然后，你将使用变量中的值写入文本“Welcome the entered name!”，其中输入的名称代表存储在 `name` 变量中的实际名称，例如，如果他们输入 Jonas，则显示 Welcome Jonas!。名称应与文本在同一行输入。

然后，你将在文本“Enter your age: ”的开头添加一个换行符（`\n`），并让用户在文本同一行输入他们的年龄，文本后不添加换行符。用户输入的年龄应存储在名为 `age` 的变量中。

使用制表符（`\t`）将文本向右推，然后输出一个标题“Name Age”，并在两个单词之间加上一个制表符。随后在标题下方另起一行显示名称和年龄。

接下来，你将使用 `{0, 20}` 语法使用固定长度列，其中 `0` 是代表变量值插入位置的索引，`20` 是列中的固定字符数。使用固定长度列显示存储在变量中的名称和年龄。

最后，你将提示用户按任意键退出应用程序，并在文本之后使用 `ReadKey` 方法等待用户按下键盘键。

## C# 初学者教程

```text
C:\Users\Jonas\Documents\Visual Studio 2017\Projects\MVCS Exam Solution\ConsoleTest.exe
Enter your name: Jonas
Welcome Jonas!

Enter your age: 45

Name    Age
Jonas   45

Fixed length column output
Jonas   45yo

Press any key to exit
```

## 创建解决方案

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_47_0.png)

1. 打开 Visual Studio
2. 点击“新建项目”链接或在主菜单中选择“文件-新建项目”。

## C# 初学者教程

1. 在“新建项目”对话框左侧树形视图中点击 **Visual C#**。
2. 在对话框中间的模板列表中选择 **Console Application**。
3. 在 **Name** 文本字段中将项目命名为 **My First Application**。
4. 点击 **OK** 按钮。
5. 在 `Program.cs` 文件中找到 `Main` 方法，你将在其中编写程序代码。

```csharp
static void Main(string[] args)
{
    //在此处编写你的代码
}
```

### 保持控制台窗口打开

待办事项列表第一件事是确保在输出和用户输入完成后控制台窗口保持打开。如果不保持窗口打开，在 Visual Studio 中运行时，它将在执行最后一行代码后立即关闭。

控制台窗口的输出应该如下所示：

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_48_0.png)

1. 将光标置于 `Main` 方法中上方大括号的右侧，在大括号之间创建一个新行，并按下键盘上的 **Enter** 键。
2. 使用 `WriteLine` 方法写入“Press any key to exit”消息。在字符串开头使用 `\n` 命令添加换行符以移动文本。
3. 使用 `ReadKey(true)` 防止字符被输出到控制台。
4. 按 `F5` 运行应用程序。目前的代码如下：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("\nPress any key to exit");
    Console.ReadKey(true);
}
```

## C# 初学者教程

1. 在上一个练习中添加的 Welcome 消息下方添加新行。
2. 使用 `Write` 方法写入消息 **Enter your age:** 而不在文本后添加换行符。在字符串开头使用 `\n` 命令添加换行符。

`Console.Write("\nEnter your age:");`

3. 使用 `var` 关键字将用户输入的年龄存储在名为 `age` 的变量中。使用 `ReadLine` 方法读取值。

`var age = Console.ReadLine();`

5. 使用包含两个制表符的格式化字符串写入存储在变量中的名称和年龄，实现这一点，必须添加索引为 0 和 1 的花括号，然后以逗号分隔的列表列出变量。

`Console.WriteLine("\t{0}\t{1}", name, age);`

## 命名空间 (Namespace) 和使用 (using)

命名空间是将属于一起且具有共同点的类进行物理分组的一种。要访问命名空间中的类，你可以在想要访问这些类的 `.cs` 文件顶部添加 `using` 语句，或者在使用这些类时在代码中提供完整的命名空间和类名。后一种使用命名空间的方法不是推荐的方法，因为它会引入大量的额外代码，导致代码杂乱且难以阅读。

假设你想计算一个数字平方根，为了实现这一点，你可以使用预定义的 .NET Framework `Math` 类中名为 `Sqrt` 的数学方法。下面是实现该功能的两种方法，命名空间路径比示例中的要长得多。你还可以注意到，在创建项目时，你的 `Program` 类被自动放置在一个命名空间中。

直接在代码中使用命名空间来实现计算。请注意，你每次调用 `Sqrt` 方法时都必须使用完整的命名空间路径。在每行上写命名空间路径看起来可能没什么额外的代码，但请记住，这是 .NET Framework 库中最短的命名空间路径之一，通常它们有几层深。

```csharp
namespace MyConsoleApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            var result1 = System.Math.Sqrt(5);
            var result2 = System.Math.Sqrt(10);
            var result3 = System.Math.Sqrt(15);
        }
    }
}
```

使用 `using` 语句声明命名空间然后调用该方法。注意，你只需要声明一次命名空间路径，就可以根据需要直接在 `Math` 类上多次调用 `Sqrt` 方法。

```csharp
using System;

namespace MyConsoleApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            var result1 = Math.Sqrt(5);
            var result2 = Math.Sqrt(10);
            var result3 = Math.Sqrt(15);
        }
    }
}
```

## 区域 (Regions)

区域是一种逻辑上分组代码的方式，不会影响程序执行流，它仅用于使代码更易读且易于遵循。区域是一个可折叠的代码段，它会隐藏代码并在位置显示描述性文本。当代码需要修改或查看时，可以展开该区域。你可以通过点击左侧边距中的加/减号来折叠和展开区域。

要创建一个区域，你需要在要包含在区域内的第一行上方添加 `#region` 关键字并后跟描述，并在要属于该区域的最后一行代码之后添加 `#endregion` 关键字。

如果你想在上一个示例的数学计算周围添加一个区域，代码看起来如下：

```csharp
static void Main(string[] args)
{
    #region Math Calculations
    var result1 = System.Math.Sqrt(5);
    var result2 = System.Math.Sqrt(10);
    var result3 = System.Math.Sqrt(15);
    #endregion
}
```

折叠时，代码将只显示标题 `Math Calculations`。

## C# 初学者教程

```csharp
static void Main(string[] args)
{
    // Math Calculations
}
```

在编写程序时，我的类或结构体中通常会有以下几个主要的区域，你将在接下来的章节中学习结构体和类，在这里，我只是想向你展示我经常使用区域创建的逻辑部分。如果区域描述中有你未知的术语，只需在脑中记住它们，并在阅读接下来的章节时留意即可。如果你觉得需要刷新关于区域的知识，可以随时返回此节。在某些应用程序中，我不需要所有的区域，而在某些情况下，我需要更细致地创建子区域。

```csharp
public class MyClass
{
    #region Delegates and Events
    #endregion
    #region Constants
    #endregion
    #region Fields/Variables
    #endregion
    #region Properties
    #endregion
    #region Constructors
    #endregion
    #region Methods
    #endregion
    #region Control Events
    #endregion
}
```

### 练习：在应用程序中添加区域

打开你在上一个练习中创建的应用程序，用获取和显示名称的代码包裹在一个区域内，并描述为 `Fetch user name`。接下来，在获取和显示用户年龄的代码周围放置一个区域，并将其描述为 `Fetch user's age`。在保持控制台窗口打开的代码周围放置第三个区域，并给它描述为 `Exit code`。

## C# 初学者教程

一旦区域就绪，通过点击代码窗口左边距的加/减号折叠和展开它们来对其进行测试。

运行应用程序以确保区域不会影响程序执行流，并且仍然像以前一样工作。

1. 在 Visual Studio 中打开 `My First Application` 项目。
2. 在第一个 `Write` 方法调用上方添加 `#region` 命令，并将其描述为 `Fetch user name`。

```csharp
#region Fetch user name
Console.Write("Enter your name: ");
```

3. 在写入欢迎消息的 `WriteLine` 方法下方添加 `#endregion` 命令。

```csharp
Console.WriteLine("Welcome {0}!", name);
#endregion
```

4. 在询问用户年龄的 `Write` 方法调用上方添加 `#region` 命令，并将其描述为 `Fetch user's age`。

```csharp
#region Fetch user's age
Console.Write("\nEnter your age: ");
```

5. 在向控制台窗口写入名称和年龄的 `WriteLine` 方法下方添加 `#endregion` 命令。

```csharp
Console.WriteLine("\t{0}\t{1}", name, age);
#endregion
```

6. 在要求用户按任意键退出的 `Write` 方法调用上方添加 `#region` 命令，并将其描述为 `Exit code`。

```csharp
#region Exit code
Console.Write("\nPress key to exit");
```

7. 在 `ReadKey` 方法下方添加 `#endregion` 命令。

```csharp
Console.ReadKey(true);
#endregion
```

8. 现在区域已就绪，通过点击代码窗口左边距中的减号来折叠它们。
9. 点击边距中的加号再次打开它们。

## C# 初学者教程

10. 现在通过右键点击代码窗口并选择 `Ctrl+M,O` 来折叠所有大纲。这将折叠活动代码窗口中的所有区域。
11. 点击边距中的加号展开 `Main` 方法。这应该显示被折叠的区域描述。
12. 通过右键点击代码窗口并选择 `Ctrl+M,L` 展开所有区域。
13. 按键盘上的 `F5` 或工具栏上的播放按钮运行应用程序。确保应用程序像添加区域之前一样正常工作。
14. 关闭应用程序。

## 初识 Windows Forms

你刚刚熟悉了用途有限的控制台应用程序。现在你将查看功能更强大的 Windows Forms 项目，你可以用它创建完整的 Windows 桌面系统。这种项目类型具有图形界面 (GUI)，用户可以通过它与你添加的控件进行交互。你可以添加许多类型的预定义控件，从按钮、文本字段到树视图控件和菜单。

## 创建解决方案

| |
| --- |
| ![57_0.png]() |

1. 打开 Studio
2. 点击 **New Project** 链接或在主菜单中选择 **File-New**。
3. 点击对话框左侧树视图中的 **Visual C#**。
4. 在项目模板列表中选择 **Windows Forms Application**。
5. 在 **Name** 文本框中将项目命名为 `My First Forms Application`。
6. 点击 **OK** 按钮。

## 项目内容

如所示，项目内容与控制台应用程序不同。首先，显示的是灰色表单而不是代码窗口，这是故意的，因为你必须在表单上添加控件才能对其进行任何有用操作，即使只是一个按钮。表单是用户交互的应用程序界面。为了给用户提供良好的体验，你应该将控件对齐在直线上，而不是

# C# 入门

不要将它们以混乱的方式散布在表面，你还想使用标签（labels）来描述控件的用途。如果用户需要在文本框中输入名称，那么你应该根据你决定的布局，在控件的上方或左侧添加标签。你可以从下一节介绍的工具箱（Toolbox）中添加控件。
