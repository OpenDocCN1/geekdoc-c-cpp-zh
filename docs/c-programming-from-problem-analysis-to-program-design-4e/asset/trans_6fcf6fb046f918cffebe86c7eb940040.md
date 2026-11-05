

### 示例 7.8

```csharp
int total = 0;
double avg;
foreach(int val in score)
{
    total += val;
}
Console.WriteLine("Total: " + total);
avg = (double)total / scoreCnt;
Console.WriteLine("Average: " + avg.ToString("F0"));
```

标识符 val 是迭代变量。在每次循环迭代中，它代表一个不同的数组元素。请记住，foreach 表达式中使用的类型应与数组类型匹配。因为 score 数组包含 int 元素，所以 val 被声明为该类型。在循环的第一次迭代期间，val 引用 score[0]。如果 foreach 循环体中的某个语句试图更改迭代变量，或将迭代变量作为 ref 或 out 参数传递，则会发生编译时错误。示例 7-9 在单独的行上显示 red、blue 和 green。

### 示例 7.9

```csharp
string[] color = {"red", "green", "blue"};
foreach(string val in color)
    Console.WriteLine(val);
```

## Array 类

通过使用索引值访问元素，C# 可以像其他语言一样方便地处理数组。但你得到的不仅仅是索引访问。任何类型的所有数组都从 Array 类继承特征，该类包含许多预定义的方法和属性。表 7-1 列出了 System.Array 类中的一些预定义方法。第三列给出了每个方法的使用示例。您可以使用 Visual Studio 中的联机帮助功能来探索这些方法，尤其是那些重载的方法。表 7-1 中的大部分信息都来自该文档。当您探索 Array 类方法时，您会发现许多未在表 7-1 中列出的其他成员。Array 类是所有面向公共语言运行时的语言的基础数组类。其属性和方法跨语言可用，这为每种 .NET 语言提供了强大的功能，而且只需极少的编程即可实现。例如，只需调用 Array 类成员方法之一即可对整个数据集合进行排序。

### 表 7-1 System.Array 方法（续）

| 方法 | 描述 | 示例 |
|---|---|---|
| GetValue(int index) | 重载。获取当前数组中指定元素的值。 | double[ ] waterDepth = {2.4, 3.5, 6.8};<br>Console.WriteLine<br>&nbsp;&nbsp;&nbsp;&nbsp;(waterDepth.GetValue(2));<br>//Displays<br>6.8 |
| IndexOf(System.Array array, object value) | 类方法。重载。返回指定值在一维数组或数组的某一部分中第一次出现的索引。 | double[ ] waterDepth = {2.4, 3.5, 6.8};<br>int i = Array.IndexOf(waterDepth, 3.5);<br>Console.WriteLine (i);<br>//Returns -1 when the value is not<br>//found in the array<br>//Displays<br>1 |
| LastIndexOf(System.Array array, object value) | 类方法。重载。返回指定值在一维数组或数组的某一部分中最后一次出现的索引。 | double[ ] waterDepth = {2.4, 3.5, 2.4};<br>int i = Array.LastIndexOf<br>&nbsp;&nbsp;&nbsp;&nbsp;(waterDepth, 2.4);<br>Console.WriteLine ( i );<br>//Displays<br>2 |
| Reverse(System.Array array) | 类方法。重载。反转一维数组或数组的某一部分中元素的顺序。 | double[ ] waterDepth = {2.4, 3.5, 6.8};<br>Array.Reverse (waterDepth);<br>foreach (double wVal in waterDepth)<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.Write (wVal + "\t");<br>//Displays<br>6.8&nbsp;&nbsp;3.5&nbsp;&nbsp;2.4 |
| SetValue(object value, int indexLocation) | 重载。将当前数组中的指定元素设置为指定值。 | double[ ] waterDepth = {2.4, 3.5, 6.8};<br>waterDepth.SetValue (55, 0);<br>foreach (double wVal in waterDepth)<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.Write (wVal + "\t");<br>//Displays<br>55&nbsp;&nbsp;3.5&nbsp;&nbsp;6.8 |
| Sort(System.Array array) | 类方法。重载。对一维数组对象中的元素进行排序。 | double[ ] waterDepth = {12.4, 3.5, 6.8};<br>Array.Sort (waterDepth);<br>foreach (double wVal in waterDepth)<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.Write (wVal + "\t");<br>//Displays<br>3.5&nbsp;&nbsp;6.8&nbsp;&nbsp;12.4 |

表 7-1 第二列中列出的一些描述指明“类方法”。您已经使用过 Math 类中的类方法。要调用类方法，请在方法名前面加上类名。查看第三列中的示例时，请注意这些类方法调用要求将 Array 列在方法名之前。

示例 7-10 演示了 Sort( )、Reverse( ) 和 Copy( ) 方法的使用。在 foreach 循环结构中，值被连接到一个字符串上。在循环外部，通过一次 MessageBox.Show( ) 方法调用来显示该字符串。

### 示例 7.10

```csharp
/* UsePredefinedMethods.cs   Author: Doyle
 * Demonstrates use of methods from the System.Array class.
 */

using System;
using System.Windows.Forms;

namespace UsePredefinedMethods
{
    class UsePredefinedMethods
    {
        static void Main( )
        {
            double [ ] waterDepth = {45, 19, 2, 16.8,
                190, 0.8, 510, 6, 18 };
            string outputMsg = "";
            string caption = "System.Array Methods Illustrated";
            double [ ] w = new double [20];

            // Displays contents of Array waterDepth
            outputMsg += "waterDepth Array\n\n";
            foreach(double wVal in waterDepth)
                outputMsg += wVal + "\n";
            MessageBox.Show(outputMsg, caption);

            // Copies 5 values from waterDepth, beginning at
            // index location 2. Place values in Array w,
            // starting at index location 0.
            Array.Copy(waterDepth, 2, w, 0, 5);

            // Sorts Array w in ascending order
            Array.Sort(w);

            // Displays Array w sorted
            outputMsg = "Array w Sorted\n\n";
            foreach(double wVal in w)
            {
                if (wVal > 0)
                    outputMsg += wVal + "\n";
            }
            MessageBox.Show(outputMsg, caption);

            // Reverses the elements in Array w
            Array.Reverse(w);

            // Displays Array w in descending order
            outputMsg = "Array w Reversed\n\n";
            foreach(double wVal in w)
            {
                if (wVal > 0)
                    outputMsg += wVal + "\n";
            }
            MessageBox.Show(outputMsg, caption);
        }
    }
}
```

如示例 7-10 所示，waterDepth 中从索引位置 2 开始的 5 个值被放入数组 w，起始索引位置为 0。最后两个 foreach 语句都包含一个 if 语句。数组 w 的大小被设置为容纳 20 个元素，但只有 5 个元素包含数据。if 语句跳过空白元素，以免它们被连接到 outputMsg 上。

示例 7-10 产生的输出如图 7-6 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_439_0.png)

### 图 7-6 示例 7-10 和示例 7-12 的输出

> 注意
> 要使用 MessageBox 类，您需要使用解决方案资源管理器窗口添加对 System.Windows.Forms 类的引用。另外，请记住去掉后台的控制台窗口，请将项目的“输出类型”属性设置为“Windows 应用程序”。在解决方案资源管理器窗口中选择项目，然后按 Alt+Enter 快捷键打开项目的属性对话框。

## 数组作为方法参数

您可以编写自己的方法并将数组作为参数发送，这与您调用 Array 类的预定义方法时非常相似。在查看示例 7-10 中的代码时，请注意使用了三个独立的代码段来显示输出，它们看起来都很相似。除了数组上方显示的标题不同之外，唯一的区别是 waterDepth 数组只显示一次，而另外两次显示的是数组 w。为什么不编写一个方法并调用它三次呢？包含数组作为参数的方法头的通用格式是：

```csharp
modifiers returnType identifier (type [ ] arrayIdentifier...)
```

示例 7-11 展示了方法头的一个示例。

### 示例 7.11

```csharp
void DisplayArrayContents (double [ ] anArray)
```

数组标识符和类型包含在参数头中。数组的长度或大小不包含在内。需要方括号来表示该参数是一个数组。

> 注意
> 当您使用 Visual Studio 时，代码生成器会向 Main( ) 方法头添加一个数组参数（Main(string[ ] args)）。这使得应用程序启动时可以将参数发送到程序中。发生这种情况时，数组标识符 args 可以像任何其他数组一样在程序中使用。由于没有值被发送到 Main( )，因此可以删除 (string[ ] args) 参数。

## 按引用传递

回顾一下，数组是引用变量。数组标识符的内存位置实际上并不包含值，而是包含一个指示数组中元素位置的地址。当您将数组传递给方法时，默认情况下，您传递的是对数组元素地址的引用。此特性的重要性在于：如果方法更改了一个或多个元素，则更改会反映在实际数据上。因此，在被调用的方法中对数组元素所做的任何更改，都会更改在调用方法中创建的相同数组元素。

