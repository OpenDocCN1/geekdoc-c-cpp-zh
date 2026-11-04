
## 16.2 字符和字符串基础

字符是 C# 源代码的基本构建块。每个程序都由字符组成，这些字符按有意义的方式组合在一起时，会形成编译器解释为描述如何完成任务的指令的序列。程序也可以包含字符常量。字符常量是表示为整数值的字符，该整数值称为*字符代码*。例如，整数值 122 对应字符常量 `'z'`。整数值 10 对应换行字符 `'\n'`。字符常量根据 Unicode 字符集建立，这是一种国际字符集，包含的符号和字母比 ASCII 字符集（列于附录 J）多得多。要了解有关 Unicode 的更多信息，请参阅 unicode.org。

字符串是被当作一个单元处理的一系列字符。这些字符可以是大写字母、小写字母、数字以及各种特殊字符：+、-、*、/、$ 等。字符串是类型 `string` 的对象。正如 C# 关键字 `object` 是类 `Object` 的别名一样，`string` 是类 `String`（命名空间 `System`）的别名。我们将字符串字面量（也称为字符串常量）写成双引号中的字符序列，如下所示：

```text
"John Q. Doe"
"999 Main Street"
"Waltham, Massachusetts"
"(201) 555-1212"
```

声明可以将字符串字面量赋给字符串引用。声明

```csharp
string color = "blue";
```

初始化字符串 color，使其引用字符串字面量对象 "blue"。

> **性能提示 16.1**
>
> *如果应用中同一个字符串字面量对象出现多次，那么程序中使用该字符串字面量的每个位置都会引用它的单一副本。可以通过这种方式共享对象，因为字符串字面量对象隐式地是常量。这种共享可节省内存。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_539_0.png)

### 逐字字符串

回顾一下，字符串中的*反斜杠*字符会引入转义序列，而在字符串中放置字面反斜杠需要使用 `\\`。有时，字符串会包含多个字面反斜杠字符（这经常出现在文件名中）。为避免过多的反斜杠，可以排除转义序列并逐字解释字符串中的所有字符，使用 `@` 字符创建所谓的逐字字符串。`@` 字符后面的双引号内的反斜杠不被视为转义序列的一部分。这通常可以简化编程并使代码更易读。例如，考虑以下赋值中的字符串：

```csharp
string file = "C:\\MyFolder\\MySubFolder\\MyFile.txt";
```

使用*逐字字符串语法*，该赋值可以改为

```csharp
string file = @"C:\MyFolder\MySubFolder\MyFile.txt";
```

逐字字符串也可以跨越多行，在这种情况下，它们会保留开始 `@"` 和结束 `"` 分隔符之间的所有换行符、空格和制表符。

## 16.3 字符串构造函数

图 16.1 演示了类 `string` 的三个构造函数。

```csharp
// Fig. 16.1: StringConstructor.cs
// Demonstrating string class constructors.
using System;

class StringConstructor
{
    static void Main()
    {
        // string initialization
        char[] characterArray = {'b', 'i', 'r', 't', 'h', ' ', 'd', 'a', 'y'};
        var originalString = "Welcome to C# programming!";
        var string1 = originalString;
        var string2 = new string(characterArray);
        var string3 = new string(characterArray, 6, 3);
        var string4 = new string('C', 5);

        Console.WriteLine($"string1 = \"{string1}\"\n" +
        $"string2 = \"{string2}\"\n" +
        $"string3 = \"{string3}\"\n" +
        $"string4 = \"{string4}\"\n");
    }
}
```

```text
string1 = "Welcome to C# programming!"
string2 = "birthday"
string3 = "day"
string4 = "CCCCC"
```

**图 16.1** | 演示字符串类的构造函数。

第 10—11 行创建 char 数组 characterArray，其中包含九个字符。第 12—16 行声明字符串 originalString、string1、string2、string3 和 string4。第 12 行将字符串字面量 "Welcome to C# programming!" 赋给字符串引用 originalString。第 13 行让 string1 引用同一个字符串字面量。

第 14 行使用带字符数组参数的 string 构造函数，将一个新字符串赋给 string2。新字符串包含该数组字符的副本。

第 15 行使用接受 char 数组和两个 int 参数的 string 构造函数，将一个新字符串赋给 string3。第二个参数指定从数组中的哪个起始索引位置（偏移量）开始复制字符。第三个参数指定从数组中指定起始位置复制的字符数（计数）。新字符串包含数组中指定字符的副本。如果指定的偏移量或计数表明程序应访问字符数组边界之外的元素，则会引发 ArgumentOutOfRangeException。

> **软件工程观察 16.1**
>
> 在大多数情况下，没有必要复制现有字符串。所有字符串都是不可变的——创建后其字符内容不能更改。此外，如果有一个或多个引用指向某个字符串（就此而言，或任何引用类型对象），则该对象不能被垃圾回收器回收。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_541_0.png)

## 16.4 字符串索引器、Length 属性和 CopyTo 方法

图 16.2 展示了

- 字符串索引器（`[]`），用于获取字符串中的任意字符，
- 字符串属性 `Length`，它返回字符串的长度，以及
- 字符串方法 `CopyTo`，它将指定数量的字符从字符串复制到 char 数组中。

```csharp
// Fig. 16.2: StringMethods.cs
// Using the indexer, property Length and method CopyTo
// of class string.
using System;

class StringMethods
{
   static void Main()
   {
      var string1 = "hello there";
      var characterArray = new char[5];

      Console.WriteLine($"string1: \"{string1}\""); // output string1

      // test Length property
      Console.WriteLine($"Length of string1: {string1.Length}");

      // loop through characters in string1 and display reversed
      Console.Write("The string reversed is: ");

      for (int i = string1.Length - 1; i >= 0; --i)
      {
         Console.Write(string1[i]);
      }

      // copy characters from string1 into characterArray
      string1.CopyTo(0, characterArray, 0, characterArray.Length);
      Console.Write("\nThe character array is: ");

      foreach (var element in characterArray)
      {
         Console.Write(element);
      }

      Console.WriteLine();
   }
}
```

```text
string1: "hello there"
Length of string1: 11
The string reversed is: ereht olleh
The character array is: hello
```

**图 16.2** | 字符串索引器、Length 属性和 CopyTo 方法。

第 16 行使用字符串属性 `Length` 确定 string1 中的字符数。与数组一样，字符串始终知道自己的大小。

第 21—24 行使用字符串索引器（`[]`）按相反顺序显示 string1 的字符，该索引器将字符串视为 char 数组，并返回字符串中特定索引处的字符。与数组一样，字符串的第一个元素索引为 0。

> **常见编程错误 16.1**
>
> *尝试访问字符串边界之外的字符会导致 IndexOutOfRangeException。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_542_0.png)

第 27 行使用字符串方法 `CopyTo` 将 string1 的字符复制到字符数组（characterArray）中。传给 `CopyTo` 方法的第一个参数是该方法在字符串中开始复制字符的索引。第二个参数是将字符复制到的字符数组。第三个参数是指定该方法开始将复制的字符放入字符数组的起始位置的索引。最后一个参数是该方法将从字符串复制的字符数。第 30—33 行一次一个字符地输出 char 数组的内容。

我们在第 21—24 行使用了 `for` 语句来演示字符串的 `Length` 属性和字符串索引器，用它们反向显示字符串。该循环本可以使用 `foreach` 和 **Reverse** 扩展方法实现，如下所示

```csharp
foreach (var element in string1.Reverse())
{
    Console.Write(element);
}
```

方法 `Reverse` 是众多 LINQ 扩展方法之一，并且需要为命名空间 `System.Linq` 添加 `using` 指令。

## 16.5 比较字符串

接下来的两个示例演示*比较字符串*的各种方法。要理解一个字符串如何“大于”或“小于”另一个字符串，可以考虑将一系列姓氏按字母顺序排列的过程。读者无疑会将 "Jones" 放在 "Smith" 之前，因为在字母表中 "Jones" 的第一个字母排在 "Smith" 的第一个字母之前。字母表不仅仅是一组 26 个字母——它是一个有序字符列表，其中每个字母都出现在特定位置。例如，Z 不仅仅是一个
