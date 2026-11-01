
这些命令在几乎完全相同的方式下运行，只有一个关键区别——前者仅在调试构建中工作；后者也适用于发布构建。事实上，Debug.WriteLine() 命令甚至不会被编译到发布构建中；它只是消失了，这无疑有其优势（例如，编译后的代码会更小）。

> 注意 Debug.WriteLine() 和 Trace.WriteLine() 方法都包含在 System.Diagnostics 命名空间中。using static 指令只能与静态类一起使用，例如包含 WriteLine() 方法的 System.Console。

这些函数的工作方式与 WriteLine() 并不完全相同。它们仅使用一个字符串参数来输出消息，而不是让你使用 {x} 语法插入变量值。这意味着你必须使用替代技术将变量值嵌入字符串中——例如，+ 拼接运算符。你也可以（可选地）提供第二个字符串参数，它会为输出文本显示一个类别。这使你能够一目了然地看到在输出窗口中显示哪些输出消息，当相似的消息从应用程序的不同位置输出时，这很有用。

这些函数的一般输出如下：

```
<category>: <message>
```

例如，以下语句，其可选类别参数为 "MyFunc"，

```
Debug.WriteLine("Added 1 to i", "MyFunc");
```

会产生以下结果：

```
MyFunc: Added 1 to i
```

下一个“试一试”演示了以这种方式输出调试信息。

## 试一试 将文本写入输出窗口：Ch07Ex01\Program.cs

- 1. 创建一个名为 Ch07Ex01 的新控制台应用程序并将其保存在目录 C:\BegVCSharp\Chapter07 中。
- 2. 按如下方式修改代码：

```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static System.Console;

namespace Ch07Ex01
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] testArray = {4, 7, 4, 2, 7, 3, 7, 8, 3, 9, 1, 9};
            int[] maxValIndices;
            int maxVal = Maxima(testArray, out maxValIndices);
            WriteLine($"Maximum value {maxVal} found at element indices:");
            foreach (int index in maxValIndices)
            {
                WriteLine(index);
            }
            ReadKey();
        }

        static int Maxima(int[] integers, out int[] indices)
        {
            Debug.WriteLine("Maximum value search started.");
            indices = new int[1];
            int maxVal = integers[0];
            indices[0] = 0;
            int count = 1;
            Debug.WriteLine(string.Format(
                $"Maximum value initialized to {maxVal}, at element index 0."));
            for (int i = 1; i < integers.Length; i++)
            {
                Debug.WriteLine(string.Format(
                    $"Now looking at element at index {i}."));
                if (integers[i] > maxVal)
                {
                    maxVal = integers[i];
                    count = 1;
                    indices = new int[1];
                    indices[0] = i;
                    Debug.WriteLine(string.Format(
                        $"New maximum found. New value is {maxVal}, at element index {i}."));
                }
                else
                {
                    if (integers[i] == maxVal)
                    {
                        count++;
                        int[] oldIndices = indices;
                        indices = new int[count];
                        oldIndices.CopyTo(indices, 0);
                        indices[count - 1] = i;
                        Debug.WriteLine(string.Format(
                            $"Duplicate maximum found at element index {i}."));
                    }
                }
            }
            Trace.WriteLine(string.Format(
                $"Maximum value {maxVal} found, with {count} occurrences."));
            Debug.WriteLine("Maximum value search completed.");
            return maxVal;
        }
    }
}
```

```
indices[count - 1] = i;
Debug.WriteLine(string.Format(
    $"Duplicate maximum found at element index {i}."));
}
```

这通过将旧的 indices 数组备份到 oldIndices 中来实现，oldIndices 是此 if 代码块本地的整数数组。请注意，oldIndices 中的值使用 `<array>.CopyTo()` 函数复制到新的 indices 数组中。该函数只需采用目标数组和用于复制的第一个元素的索引，然后将所有值粘贴到目标数组中。

在整个代码中，使用 Debug.WriteLine() 和 Trace.WriteLine() 函数输出各种文本。这些函数使用 string.Format() 函数以与 WriteLine() 相同的方式将变量值嵌入字符串中。这比使用 + 拼接运算符更高效一些。

当你在调试模式下运行应用程序时，你会在循环中看到产生结果所采取步骤的完整记录。在发布模式下，你只会看到计算结果，因为发布构建中不会进行对 Debug.WriteLine() 的调用。

## 跟踪点

一种替代向输出窗口写入信息的替代方法是使用 *tracepoints*。这些是 Visual Studio 的功能，而不是 C# 的功能，但它们与使用 Debug.WriteLine() 具有相同的功能。本质上，它们使你能够在不修改代码的情况下输出调试信息。

为了演示跟踪点，你可以使用它们来替换前一个示例中的调试命令。 （请参阅本章下载代码中的 Ch07Ex01TracePoints 文件。）添加跟踪点的过程如下：

- 1. 将光标定位在想要插入跟踪点的行上。跟踪点将在执行此行代码 *before* 处理。
- 2. 右键单击代码行并选择 Breakpoint → Insert Tracepoint。右键单击放置在代码行旁边的红色圆圈并选择 Settings 菜单项。
- 3. 选中 Actions 复选框，并在 Log a message 部分的 Message 文本框中输入要输出的字符串。如果要输出变量值，请将变量名用大括号括起来。
- 4. 单击 OK。包含跟踪点的代码行左侧会出现一个红色菱形，并且该代码行本身显示为红色。

正如添加跟踪点的对话框标题和所需的菜单选择所暗示的那样，跟踪点是一种断点形式（如果需要，可以像断点一样导致应用程序执行暂停）。你稍后会在本章中看到断点，它们通常用于更高级的调试目的。

图 7-4 显示了 Ch07Ex01TracePoints 的第 32 行所需的跟踪点，其中行号适用于删除现有 Debug.WriteLine() 语句后的代码。

## 诊断输出与跟踪点对比

现在你已经看到了输出本质上相同信息的两种方法，请考虑每种方法的优缺点。首先，跟踪点没有 Trace 命令的等效项；也就是说，使用跟踪点无法在发布构建中输出信息。这是因为跟踪点不包含在你的应用程序中。跟踪点由 Visual Studio 处理，因此在编译后的应用程序版本中不存在。只有当你的应用程序在 Visual Studio 调试器中运行时，你才会看到跟踪点在起作用。

跟踪点的主要缺点也是其主要优点，即它们存储在 Visual Studio 中。这使得它们可以快速轻松地根据需要添加到你的应用程序中，但也使得它们很容易被删除。删除跟踪点只需单击指示其位置的红色菱形即可，如果你输出的是复杂的信息字符串，这可能会很烦人。

不过，跟踪点的一个好处是可以轻松添加额外的信息，例如 $FUNCTION，它会将当前函数名称添加到输出消息中。虽然使用 Debug 和 Trace 命令编写的代码也可以获得此信息，但获取起来更棘手。总结来说，使用这两种输出调试信息的方法如下：

- **Diagnostics output** — 在调试输出是你始终希望从应用程序输出的内容时使用，特别是当你想要输出的字符串很复杂，涉及多个变量或大量信息时。此外，如果你希望在发布模式下构建的应用程序执行期间输出，Trace 命令通常是唯一的选择。
- **Tracepoints** — 在调试应用程序时使用，以快速输出可能有助于你解决语义错误的重要信息。

## 中断模式下的调试

本章描述的其余调试技术在中断模式下工作。此模式可以通过多种方式进入，所有方式都会以某种方式使程序暂停。

### 进入中断模式

进入中断模式的最简单方法是当应用程序运行时单击 IDE 中的暂停按钮。此暂停按钮位于 Debug 工具栏上，你应该将其添加到 Visual Studio 默认出现的工具栏中。为此，右键单击工具栏区域并选择 Debug。图 7-6 显示了出现的 Debug 工具栏。

![](img/cf72ea860016d2d680fc085fc06f265a_171_0.png)

工具栏上的前三个按钮允许手动控制中断。在图 7-6 中，这些按钮呈灰色，因为它们不适用于当前未执行的程序。以下各节根据需要描述其余按钮。

![](img/cf72ea860016d2d680fc085fc06f265a_171_0.png)

当应用程序运行时，工具栏会更改为如图 7-7 所示的外观。
