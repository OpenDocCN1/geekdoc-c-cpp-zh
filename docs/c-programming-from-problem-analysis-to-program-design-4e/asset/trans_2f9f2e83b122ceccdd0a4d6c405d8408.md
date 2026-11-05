
### 表 8-1 ArrayList 成员（续）

| 方法或属性 | 说明 |
|---|---|
| Repeat() | 返回一个 ArrayList，其元素是指定值的副本 |
| Reverse() | 重载；反转元素的顺序 |
| Sort() | 重载；对元素或其中一部分进行排序 |
| ToArray() | 重载；将元素复制到新数组 |
| TrimToSize() | 将容量设置为实际元素数 |

> ArrayList 类类似于其他语言中的 Vector 类，因为可以使用 Add() 和 Remove() 方法将元素压入和弹出。

示例 8-14 包含一个创建 ArrayList 类对象的程序。其中添加了字符串值作为元素。任何预定义或用户定义的类型都可以用作 ArrayList 对象。

C# 还包含一个 `List<>` 类。这是一个泛型类，与 ArrayList 类非常相似。`List<>` 类也是一种动态结构，其大小可以增大和缩小。这两个类的主要区别在于，`List<>` 类要求放入结构中的对象具有相同类型。ArrayList 允许混合类型。`List<>` 的优点是，从结构中检索值时不必进行取消装箱或强制转换。对于 int、bool 和 double 等数据值类型，`List<>` 泛型类提供比 ArrayList 类更快的访问速度。你将在第 11 章学习更多关于泛型集合类的知识。

> 对于此应用程序，只需要两个 using 语句。它们就是示例 8-14 中所示的语句。

```csharp
using System;
using System.Collections;
```

### 示例 8.14

```csharp
/* ArrayListExample.cs    Author: Doyle
 * Instantiates the ArrayList class.
 * Adds and removes values. Demonstrates
 * displaying items using an index.
 */

using System;
using System.Collections;

namespace ArrayListExample;

public class ArrayListExample
{
    public static void Main( )
    {
        ArrayList anArray = new ArrayList( );

        anArray.Add("Today is the first day of the rest "
            + "of your life!");
        anArray.Add("Live it to the fullest!");
        anArray.Add("ok");
        anArray.Add("You may not get a second chance.");

        Console.WriteLine("Count of elements in array: {0}",
            anArray.Count);
        anArray.RemoveAt(2);
        Console.WriteLine("New Count (after removing ok): {0}",
            anArray.Count);
        Console.WriteLine( );
        DisplayContents(anArray);
        Console.ReadKey( );
    }

    public static void DisplayContents(ArrayList ar)
    {
        for(int i = 0; i < ar.Count; i++)
            Console.WriteLine(ar[i] );
        Console.WriteLine();
    }
}
```

该示例演示了如何向结构中添加和移除项。一次示例运行的输出如图 8-6 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_498_0.png)

图 8-6 ArrayList 示例的示例运行

**注意**

到现在，你应该已经完全清楚，方法必须包含圆括号 ( )。在 C# 中，属性成员不使用圆括号。

## String 类

你从本书开头起就一直在使用 string 数据类型。本章包含 string 数据类型，因为字符串用于存储 Unicode 字符的集合。

**注意**

Unicode 为字符分配唯一的数值。它是 .NET 语言使用的通用字符编码方案。Unicode 使开发可在全球使用的应用程序变得更容易，因为它包含大多数国际字符。

可以使用 string 或 String 实例化对象。这样做可行，因为 string 是 .NET Framework 中 System.String 类的别名。C# 中的关键字是 string，它在 Visual Studio 中显示为蓝色。本书通篇使用它来表示该类型。

你已经了解到 string 是引用类型。通常对于引用类型，相等运算符 == 和 != 比较的是对象的引用，而不是它们的值。然而，相等运算符在 string 上的工作方式与其他引用对象不同。相等运算符被定义为比较 string 类型所引用的内容或值，而不是比较它们的地址。相等运算符被定义为执行字典序比较，这意味着它使用每个字符的 Unicode 表示形式，一次一个字符地进行比较。这很像字典存储单词的方式。关系运算符（>、<、>=、<=）未针对字符串定义。有几种方法（包括表 8-2 中所示的 Compare( )）与 > 和 < 运算密切相关。比较时使用 Unicode 字符表示形式。

与某些要求将字符集合存储为 char 数组的语言不同，C# 的 string 类型允许使用 [ ] 和索引访问单个字符，但也可以将 string 类型的变量作为一组字符来处理。与数组对象一样，当访问字符串中的单个元素时，第一个字符的索引为零。不过，在 C# 中使用字符串可以两全其美。可以使用索引访问单个字符，而 string 变量又是 string 类的对象。因此，除了用于串联的 [ ] 和 + 之外，还有许多预定义的方法和属性，使 string 对象功能丰富且灵活。

string 类的对象存储不可变的字符序列。它们被认为是不可变的，因为一旦为字符串赋值，它就不能被修改。看似在修改字符串的方法实际上返回一个包含修改内容的新字符串，因此最终会得到两个不同的字符串。.NET 还包含另一个类 StringBuilder，它表示可变的字符字符串。此类的对象可以将数据追加到同一对象上。StringBuilder 类提供了许多与 string 类相同的成员。对于需要串联字符串或向字符串添加字符的应用程序，你应考虑实例化 StringBuilder 类的对象。

表 8-2 使用示例 8-15 中所示的声明，展示了 string 类的一些成员。

### 示例 8.15

```csharp
string sValue = "C# Programming";
object sObj;
string s = "C#";
```

表 8-2 的第三列展示了使用 string 类的一些方法和属性后示例产生的结果。

### 表 8-2 string 类的成员

| 方法和属性 | 说明 | 示例 |
|---|---|---|
| Clone() | 返回对此 string 实例的引用。 | sObj = sValue.Clone();<br>Console.WriteLine(sObj);<br>//Displays<br>C# Programming |
| Compare() | 重载。类方法。比较两个字符串。 | if (string.Compare(sValue, s) > 0)<br>Console.WriteLine("sValue is " + "lexicographically greater.");<br>//Displays<br>sValue is lexicographically greater. |
| Concat() | 重载。类方法。串联一个或多个字符串。 | string ns = string.Concat(sValue, s);<br>Console.WriteLine(ns);<br>//Displays<br>C# ProgrammingC# |
| Copy() | 类方法。创建与源字符串具有相同值的新字符串副本。 | s = string.Copy(sValue);<br>Console.WriteLine(s);<br>//Displays<br>C# Programming |
| EndsWith() | 确定此实例的结尾是否与指定字符串匹配。 | bool result = sValue.EndsWith("#");<br>Console.WriteLine(result);<br>//Displays<br>False |
| Equals() | 重载。确定两个字符串是否具有相同的值。 | bool result = sValue.Equals(s);<br>Console.WriteLine(result);<br>//Displays<br>False |
| Format() | 重载。类方法。将字符串中的每个格式规范替换为相应对象值的文本等效形式。 | double nu = 123.45678;<br>string nn = string.Format("{0:F2}", nu);<br>Console.WriteLine(nn);<br>//Displays<br>123.46 |
| IndexOf() | 重载。返回字符串或一个或多个字符在此实例中第一次出现的索引。 | Console.WriteLine(sValue.IndexOf("#"));<br>//Displays<br>1 |
| Insert() | 在指定索引位置插入字符串的指定实例。 | s = sValue.Insert(3, ".NET ");<br>Console.WriteLine(s);<br>//Displays<br>C# .NET Programming |
| LastIndexOf() | 重载。返回指定字符或字符串最后一次出现的索引。 | Console.WriteLine(sValue.LastIndexOf("P"));<br>//Displays<br>3 |
| Length - 属性 | 获取字符数。 | Console.WriteLine(sValue.Length);<br>//Displays<br>14 |
| PadLeft() | 重载。将字符串中的字符右对齐，并在左侧用空格或指定字符填充。 | s = sValue.PadLeft(20, '#');<br>Console.WriteLine(s);<br>//Displays<br>#######C# Programming<br>Console.WriteLine("".PadLeft(10, '-'));<br>//Displays<br>---------- |
