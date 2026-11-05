
```csharp
// Displays Array w in descending order
outputMsg = "Array w Reversed\n\n";
foreach(double wVal in w)
{
    if (wVal > 0)
        outputMsg += wVal
                   + "\n";
}
MessageBox.Show(outputMsg, caption);
}
}
}
```

正如示例 7-10 中所述，从 waterDepth 中开始于索引位置 2 的五个值被放置到数组 w 中，从索引位置 0 开始。最后两个 foreach 语句都包含一个 if 语句。数组 w 被定义为容纳 20 个条目。只有五个单元包含数据。if 语句跳过空白条目，因此它们不会被连接到 outputMsg 上。

示例 7-10 产生的输出显示在图 7-6 中。

![](img/e33ae760e23d89eac66541252ad65de8_409_0.png)

**图 7-6** 示例 7-10 和 7-12 的输出

要使用 `MessageBox` 类，您需要使用 **解决方案资源管理器** 窗口向 `System.Windows.Forms` 类添加引用。还请记住去掉后台的控制台窗口，将项目的 **输出类型** 属性设置为 **Windows 应用程序**。在 **解决方案资源管理器** 窗口中选择项目，然后按 **Alt+Enter** 快捷键会打开项目的属性对话框。

## 数组作为方法参数

您可以编写自己的方法并像对 `Array` 类的预定义方法调用那样将数组作为参数发送。在回顾示例 7-10 中的代码时，请注意用于显示输出的三个独立代码段，它们看起来都很相似。除了数组上方的不同标题外，唯一的区别是 `waterDepth` 数组只显示一次。另两次显示的是数组 `w`。为什么不写一个方法并调用三次呢？包含数组作为参数的方法标题的通用格式为：

```
modifiers returnType identifier (type [ ] arrayIdentifier...)
```

方法标题的示例显示在示例 7-11 中。

### 示例 7-11

```
void DisplayArrayContents (double [ ] anArray)
```

数组标识符和类型包含在参数标题中。不包括数组的长度或大小。需要使用方括号来指示参数是数组。

当您使用 Visual Studio 时，代码生成器会在 `Main( )` 方法标题中添加一个数组参数（`Main(string[ ] args)`）。这使得在程序首次打开时可以向程序发送参数。此时，数组标识符 `args` 可以像其他任何数组一样在程序中使用。

### 按引用传递

回想一下，数组是引用变量。数组标识符的内存位置实际上不包含值，而是包含指示数组元素位置的地址。当您将数组传递给方法时，默认情况下，您传递的是对数组元素地址的引用。此功能的重要性在于，如果方法更改一个或多个元素，则更改会作用于实际数据。因此，在被调用方法中对数组元素所做的任何更改都会改变在调用方法中创建的相同数组元素。

期望数组作为参数的方法的实际调用仅包括标识符。它不包括大小或方括号。对示例 7-11 中所示的 DisplayArrayContents( ) 方法的调用如下：

```
DisplayArrayContents (waterDepth);
```

请记住 waterDepth 是一个 double [ ] 数组。

示例 7-12 说明了如何将输出语句放在方法中并每次使用不同的参数调用三次。第一次调用发送 waterDepth 数组。最后两次调用发送 w 数组。

### 示例 7-12

```csharp
/* StaticMethods.cs Author: Doyle
 * Demonstrates use of methods from the
 * System.Array class.
 */
using System;
using System.Windows.Forms;
namespace StaticMethods
{
    class StaticMethods
    {
        public const string CAPTION = "System.Array Methods Illustrated";
        static void Main( )
        {
            double [ ] waterDepth = {45, 19, 2, 16.8,
                                    190, 0.8, 510, 6, 18};
            double [ ] w = new Double [20];

            DisplayOutput(waterDepth, "waterDepth Array\n\n");

            // Copies values from waterDepth to w
            Array.Copy(waterDepth, 2, w, 0, 5);

            // Sorts Array w in ascending order
            Array.Sort (w);
            DisplayOutput(w, "Array w Sorted\n\n");

            // Reverses the elements in Array w
            Array.Reverse(w);
            DisplayOutput(w, "Array w Reversed\n\n");
        }

        // Displays an array in a MessageBox
        public static void DisplayOutput(double [ ] anArray,
            string msg)
        {
            foreach(double wVal in anArray)
                if (wVal > 0)
                    msg += wVal
                        + "\n";
            MessageBox.Show(msg, CAPTION);
        }
    }
}
```

请注意 CAPTION 如何在 StaticMethods 类中定义为公共常量数据成员。声明出现在示例 7-12 中 Main( ) 方法之上。这样做使每个方法成员都可以访问字符串，而无需向每个方法传递 CAPTION 的值。

DisplayOutput( ) 方法中的参数标识符 anArray 用作数组参数的占位符。数组的长度不同，但这不会造成问题。方法中使用的 foreach 语句会处理数组中的每个元素。当数组 w 被发送到方法中时，有必要使用选择语句（if (wVal > 0)）；否则会显示 20 行。foreach 循环遍历数组中的每个元素。数组 w 的维度长度为 20。如果没有 if 语句，在没有其他初始化值的情况下会显示多个 0 值。

> 整数数组的构造函数使用零作为默认值。其中包括 sbyte、byte、short、ushort、int、uint、long 和 ulong；它们的默认值是 0。decimal、float 和 double 的默认构造函数值分别为 0.0M、0.0F 和 0.0D。bool 的默认值是 False。

图 7-6 显示了示例 7-12 的输出。它与示例 7-10 产生的输出完全相同。最后一个示例，即示例 7-12，更为简洁。因为数组参数自动被视为按引用传递，所以在参数或参数列表中不需要额外的关键字，如 ref 或 out。

> 请记住，当您按引用传递或按引用调用时，您传递的是标识符的地址。按值调用或按值传递会发送实际数据。当您传递单个数组元素（如整数）时，您是按值传递。当前数组元素内容的副本会被制作并发送到方法中。

考虑以下分配五个元素内存的情况：

```csharp
int [ ] temperature = new int[5];
```

以下方法可用于向 temperature 数组输入值：

```csharp
public static void InputValues(int [ ] temp)
{
    string inValue;

    for(int i = 0; i < temp.Length; i++)
    {
        Console.Write("Enter Temperature {0}: ", i + 1);
        inValue = Console.ReadLine( );
        temp[i] = int.Parse(inValue);
    }
}
```

调用输入值的方法如下：

```csharp
InputValues(temperature);
```

图 7-7 显示了输入 78、82、90、87 和 85 的结果。

![](img/e33ae760e23d89eac66541252ad65de8_413_0.png)

**图 7-7** 调用 InputValues( ) 方法后数组的内容

当调用 InputValues( ) 方法时，会发送对 temperature 的引用。在第 3 章中，您了解到当使用按值调用发送参数时，会复制参数的内容。值的副本存储在仅在该方法内可访问的新内存位置中。对值所做的更改不会影响调用模块中的变量。返回被调用方法后，参数的原始值保持不变。它包含在方法执行之前所具有的相同值。
