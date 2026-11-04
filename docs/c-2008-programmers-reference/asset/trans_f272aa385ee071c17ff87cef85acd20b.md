
```csharp
Console.Write("Please enter a number: ");
int num = int.Parse(Console.ReadLine());
int sum = 0;
for (int i = 1; i <= num; i++)
{
    //---sum up all odd numbers---
    if (i % 2 == 1)
    {
        sum += i;
#if DEBUG
        Console.WriteLine("i={0}, sum={1}", i, sum);
#endif
    }
    Console.WriteLine(
        "Sum of all odd numbers from 1 to {0} is {1}",
        num, sum);
    Console.ReadLine();
}
```

*DEBUG 是一个开发者常用的符号，用来表示调试语句，这也是大多数书籍在示例中使用它的原因。然而，你可以使用 #define 预处理器指令定义任何你想要的符号。*

在编译之前，预处理器会评估 #if 预处理器指令，以查看是否已定义 DEBUG 符号。如果已定义，则 #if 和 #endif 预处理器指令之间包裹的语句（们）将被包含进编译。如果 DEBUG 符号未被定义，则 #if 和 #endif 预处理器之间包裹的语句 — 该语句（们） — 将从编译中省略。

要测试 TestDefine 程序，请按照以下步骤操作：

- 1. 启动 Visual Studio 2008 命令提示符（开始 ⇨ 程序 ⇨ Microsoft Visual Studio 2008 ⇨ Visual Studio 工具 ⇨ Visual Studio 2008 命令提示符）。
- 2. 切换到包含程序的路径（C:\TestDefine）。
- 3. 通过发出以下命令编译应用程序：
```
csc Program.cs.
```
- 4. 通过发出以下命令运行程序：
```
Program.exe.
```

图 3-13 显示了应用程序的输出。如你所见，调试语句打印出了中间结果。

![](img/a977a875c7c627b45d939729705a252e_137_0.png)

图 3-13

要取消定义一个符号，你可以使用 #undef 预处理器指令，如下所示：

```
#undef DEBUG
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
...
```

如果你现在重新编译程序，调试语句将被省略。

使用 #define 预处理器指令的另一种流行方式是省略符号的定义并在编译时注入它。例如，如果你从程序中删除 #define 预处理器指令，你可以使用 /define 编译器选项来定义它：

- 1. 在 Visual Studio 2008 命令提示符中，使用以下命令编译程序：
`csc Program.cs /define:DEBUG.`
- 2. 通过发出以下命令运行程序：
`Program.exe.`

输出与你在图 3-13 中看到的完全相同 — 调试语句打印出了中间结果。

如果你现在通过定义另一个符号（而不是 DEBUG）重新编译程序，你会发现调试输出不会出现（参见图 3-14）。

## 第一部分：C# 基础

（续）

```
}
Console.WriteLine(
"Sum of all odd numbers from 1 to {0} is {1}",
num, sum);

Console.ReadLine();
}
}
```

图 3-15 显示了在定义不同符号时不同的输出。顶部屏幕显示的是定义了 DEBUG 符号时的输出。中间屏幕显示的是定义了 NORMAL 符号时的输出。底部屏幕显示的是未定义任何符号时的输出。

![](img/a977a875c7c627b45d939729705a252e_139_0.png)

图 3-15

#if 预处理器指令也可以使用逻辑运算符测试多个条件。以下是一些示例：

```
#if (DEBUG || NORMAL)  //---either DEBUG or NORMAL is defined---
#if (DEBUG && NORMAL)  //---both DEBUG and NORMAL are defined---
#if (!(DEBUG && NORMAL))  //---DEBUG is not defined AND NORMAL is defined---
```

## #warning 和 #error

#warning 预处理器指令允许你从代码的特定位置生成警告。以下示例展示了如何在编译时显示警告消息的方式。

```
for (int i = 1; i <= num; i++)
{
    //---sum up all odd numbers---
    if (i % 2 == 1)
    {
        sum += i;
#if DEBUG
#warning Debugging mode is on
        Console.WriteLine("i={0}, sum={1}", i, sum);
#elif NORMAL
#warning Normal mode is on
        Console.WriteLine("sum={0}", sum);
#else
#warning Default mode is on
        Console.WriteLine(".");
#endif
    }
}
```

图 3-16 显示了使用 /define 编译器选项定义 DEBUG 符号时的输出。

![](img/a977a875c7c627b45d939729705a252e_140_0.png)

图 3-16

## 第一部分：C# 基础

#error 预处理器指令允许你生成一个错误。请考虑以下示例：

```
for (int i = 1; i <= num; i++)
{
    //--sum up all odd numbers---
    if (i % 2 == 1)
    {
        sum += i;
    }
#if DEBUG
#warning Debugging mode is on
    Console.WriteLine("i={0}, sum={1}", i, sum);
#elif NORMAL
#error This mode is obsolete.
    Console.WriteLine("sum={0}", sum);
#else
#warning Default mode is on
    Console.WriteLine("...");
#endif
}
```

这里，如果定义了 NORMAL 符号，则会显示错误消息，并且条件指令中定义的语句将被忽略。图 3-17 显示，当你定义 NORMAL 符号时，错误消息会被显示并且编译被中止。

![](img/a977a875c7c627b45d939729705a252e_141_0.png)

图 3-17

## #line

#line 预处理器指令允许你修改编译器的行号以及（可选的）错误和警告的输出文件名。

#line 预处理器指令在以下示例中被注入。突出显示的代码表示会导致调试器发出警告消息的语句：

- 1. using System;
- 2. using System.Collections.Generic;
- 3. using System.Linq;
- 4. using System.Text;
- 5.
- 6. namespace TestDefine
- 7. {
- 8.     class Program
- 9.     {
- 10.         static void Main(string[] args)

```
11.
12. #line 25
13.     int i;                 //---treated as line 25---
14.     char c;                //---treated as line 26---
15.     Console.WriteLine("Line 1");   //---treated as line 27---
16. #line hidden
17.     Console.WriteLine("Line 2");   //---treated as line 28---
18.     Console.WriteLine("Line 3");   //---treated as line 30---
19. #line default
20.     double d;              //---treated as line 20---
21.     Console.WriteLine("Line 4");   //---treated as line 21---
22. #line 45 "Program1.cs"
23.     Single s;              //---treated as line 45---
24.     Console.WriteLine("Line 5");   //---treated as line 46---
25.     Console.ReadLine();    //---treated as line 47---
26. }
27. }
28. }
```

*行号仅用于说明目的，并不是程序的一部分。*

四个突出显示的行编号为 13、14、20 和 23。当你在 Visual Studio 2008 中构建程序时，报告的行是 25、26、20 和 45（参见图 3-18）。

![](img/a977a875c7c627b45d939729705a252e_142_0.png)

图 3-18

## 第一部分：C# 基础

让我们看看示例程序中的 #line 指令：

- `#line 25` 意味着你想要修改行号，使用指定的行号（本例中为 25）而不是错误语句的实际行号。这在你需要为代码的特定部分分配固定行号以便轻松追踪时很有用。有趣的是，下一行会从 25 继续，即下一行现在是第 26 行。这可以从 `char c;` 行的警告消息中看出。
- `#line default` 意味着编译器将报告实际的行号。
- `#line 45 "Program1.cs"` 意味着你想要将行号固定在 45 并指定出错的文件名（本例中为 `Program1.cs`）。一个示例用法是，出错的语句可能是对外部 DLL 的调用，通过在此处指定 DLL 的文件名，就更清楚地表明错误可能来自该 DLL。

那么 #line hidden 语句呢？该预处理器指令指示调试器跳过从 #line hidden 预处理器指令开始的代码块。调试器将跳过该行（们），直到找到下一个 #line 预处理器指令为止。这对于跳过你不感兴趣的方法调用（例如非你编写的）很有用。

> *有趣的是，你可以用 #line 16707566 (0xFeeFee) 替换 #line hidden 预处理器指令，它仍然能正确工作。*

## #region 和 #endregion

#region 和 #endregion 预处理器指令与 Visual Studio 的代码编辑器一起使用。让我们使用以下示例进行操作：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
            //---implementations here---
        }

        private void Method1()
        {
            //---implementations here---
        }

        private void Method2()
        {
            //---implementations here---
        }
    }
}
```
