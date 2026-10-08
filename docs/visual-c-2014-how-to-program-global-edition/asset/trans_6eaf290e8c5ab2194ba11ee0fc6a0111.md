

## 16.9 杂项字符串方法

string1 = "cheers!"
string2 = "GOOD BYE "
string3 = " spaces "
将 string1 中的 "e"替换为 "E": "chEEers!"
string1.ToUpper() = "CHEERS!"
string2.ToLower() = "good bye"
string3 在 trim 后 = "spaces"
string1 = "cheers!"

图 16.8 展示字符串方法 Replace，ToLower，ToUpper 和 Trim。（2 部分中的第 2 部分。）

第 20 行使用[s] 方法返回一个新字符串，将 string1 中所有出现的字符 'e' 替换为 'E'。Replace 接受两个参数——要查找的字符（char）和另一个用于替换第一个参数所有出现位置的字符。原始字符串保持不变。如果没有出现第一个参数，该方法将返回原始字符串。该方法的较旧版本允许你提供两个字符串作为参数。

ToUpper 方法生成一个新字符串（第 24 行），将任何小写字母替换为其对应的大写字母（使用当前区域的规则）。该方法返回一个包含转换后字符串的新字符串；原始字符串保持不变。如果没有需要转换的字符，则返回原始字符串。

第 25 行使用 ToLower 方法返回一个新字符串，其中 string2 中的任何大写字母都被替换为其对应的小写字母（使用当前区域的规则）。原始字符串保持不变。与 ToUpper 类似，如果没有需要转换成小写的字符，方法ToLower 方法将返回原始字符串。

## 第 16 章 字符串与字符：深入观察

第 29 行使用 string Trim 来移除字符串开头和结尾的所有空白字符。在不改动原始字符串的情况下，该方法返回一个新字符串，该字符串包含原字符串，但省略了开头和结尾的空白字符。此方法对于获取用户输入（例如，通过 TextBox）特别有用。Trim 方法的另一个版本接受字符数组，并返回字符串的副本，该副本不以参数中的任何字符作为开头或结尾。

## 16.10 StringBuilder 类

该类提供了许多处理字符串的功能。然而，字符串的内容永远无法改变。看似在拼接字符串的操作实际上是在创建新字符串——++ 运算符创建一个新字符串并将其引用赋值给 ++ 运算符左侧的变量。

接下来的章节将讨论 StringBuilder 类（命名空间 System.Text）的特性，即可变字符串。每个 StringBuilder 都可以存储由其容量（capacity）指定的字符数量。扩展 StringBuilder 的容量会导致容量扩大以容纳额外的字符。正如我们所看到的，StringBuilder 类的成员（如方法 Append 和 AppendFormat）可以用于拼接，就像 string 类的 + 和 += 运算符一样——但不会创建任何新对象。StringBuilder 在处理大量字符串操作时特别有用，因为它比创建不可变字符串要高效得多。

> 性能提示 16.2
> string 类的对象是不可变的（即常量字符串），而 StringBuilder 类的对象是可变的。它可以执行某些涉及字符串的优化（例如在多个引用之间共享一个字符串），因为它知道这些对象不会改变。

## StringBuilder 构造函数

StringBuilder 类提供了六个重载构造函数。StringBuilder 类（第 10 行，16.9）演示了这些重载构造函数中的三个。第 10 行使用无参数的 StringBuilder 构造函数创建一个不包含任何字符且具有特定实现实现的默认初始容量的 StringBuilder。第 11 行使用接受 int 参数的 StringBuilder 构造函数来创建一个不包含任何字符且初始容量为 int 参数中指定的值（即 10）的 StringBuilder。第 12 行使用接受字符串参数的 StringBuilder 构造函数来创建一个可能与字符串大小不同的 StringBuilder。第 14–16 行隐式地使用 StringBuilder 方法 ToString 来获取 StringBuilder 内容的字符串表示。

```cs
// 图 16.9: StringBuilderConstructor.cs
// 展示 StringBuilder 类的构造函数。
using System;
using System.Text;
```

图 16.9 | 展示 StringBuilder 类的构造函数。（2 部分中的第 1 部分）。

## 16.11 StringBuilder 类

```csharp
5
6 class StringBuilderConstructor
7 {
8   static void Main()
9   {
10    var buffer1 = new StringBuilder();
11    var buffer2 = new StringBuilder(10);
12    var buffer3 = new StringBuilder("hello");
13
14    Console.WriteLine($"buffer1 = {buffer1}");
15    Console.WriteLine($"buffer2 = {buffer2}");
16    Console.WriteLine($"buffer3 = {buffer3}");
17
18 }
```

buffer1 = ""
buffer2 = ""
buffer3 = "hello"

图 16.9 | 展示 StringBuilder 类的构造函数。（2 部分中的第 2 部分。）

## 16.11 Length 和 Capacity 属性，EnsureCapacity 方法和 StringBuilder 类的索引器

StringBuilder 类提供了 Length 和 Capacity 属性，分别返回 StringBuilder 中当前的字符数量以及 StringBuilder 在不分配更多内存的情况下可以存储的字符数量。这些属性也可以用于增加或减少 StringBuilder 的长度或容量。EnsureCapacity 方法允许你减少 StringBuilder 容量增加的次数。该方法确保 StringBuilder 的容量至少为指定的值。图 16.10 展示了这些方法和属性。

```cs
// 图 16.10: StringBuilderFeatures.cs
// StringBuilder 尺寸操作。
using System;
using System.Text;
class StringBuilderFeatures
{
  static void Main()
  {
    var buffer = new StringBuilder("Hello, world!");
    // 使用 Length 和 Capacity
    Console.WriteLine(buffer.Length);
    Console.WriteLine(buffer.Capacity);
    // EnsureCapacity
    buffer.EnsureCapacity(75);
  }
}
```

图 16.10 | 容量操作。（2 部分中的第 1 部分。）

## 第 16 章 字符串与字符：深入观察

```csharp
var buffer = new StringBuilder("Hello, ");
// 使用 Length 和 Capacity
Console.WriteLine(buffer.Length);
Console.WriteLine(buffer.Capacity);
// EnsureCapacity
buffer.EnsureCapacity(75);
```

图 16.10 | 容量操作。（2 部分中的第 2 部分。）

程序包含一个 StringBuilder，第 10 行使用接受字符串参数的构造函数将其初始化为 "Hello, "。第 11 行使用 Length 属性设置长度。第 12 行使用 EnsureCapacity 确保 75。第 25-28 行可以使用以下 foreach 替换：

```csharp
for (int i = 0; i < buffer.Length; i++)
{
    Console.Write(buffer[i]);
}
```

## 16.12 StringBuilder 类

## 16.12 StringBuilder 类的 Append 和 AppendFormat 方法

StringBuilder 类提供了重载方法，允许各种类型的值添加到 StringBuilder 的末尾。框架库为每个简单类型以及字符数组、字符串和对象的版本提供了支持（记住 ToString 方法会产生任何对象的字符串表示）。每个方法接受一个参数，将其转换为字符串并附加到 StringBuilder。图 16.11 使用多个 Append 方法（第 22–40 行）附加第 10–18 行变量的字符串表示。

```cs
// 图 16.11: StringBuilderAppend.cs
// 展示 StringBuilder 方法。
using System;
using System.Text;
class StringBuilderAppend
{
    static void Main()
    {
        object objectValue = "hello";
        var stringValue = "good bye";
        char[] charArray = {'a', 'b', 'c', 'd', 'e', 'f'};
        var booleanValue = true;
        var charValue = 'Z';
        var integerValue = 7;
        var longValue = 1000000; // L 表示长型字面量
        var floatValue = 2.5F; // F 表示浮点型字面量
        var doubleValue = 33.333;
        var buffer = new StringBuilder();

        // 使用 Append 方法将值添加到 buffer
        buffer.append(objectValue);
        buffer.append(" ");
        buffer.append(stringValue);
        buffer.append(" ");
        buffer.append(charArray);
        buffer.append(" ");
        buffer.append(characterArray, 0, 3);
        buffer.append(" ");
        buffer.append(booleanValue);
        buffer.append(" ");
        buffer.append(charValue);
        buffer.append(" ");
        buffer.append(integerValue);
        buffer.append(" ");
        buffer.append(longValue);
        buffer.append(" ");
        buffer.append(floatValue);
        buffer.append(" ");
        buffer.append(doubleValue);
    }
}
```

图 16.11 | 展示 StringBuilder 方法。（2 部分中的第 1 部分）。

