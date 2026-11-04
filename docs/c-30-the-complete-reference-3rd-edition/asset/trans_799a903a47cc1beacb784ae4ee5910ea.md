
```csharp
// Give nums some values.
for(int i = 0; i < 3; i++)
    for(int j=0; j < 5; j++)
        nums[i,j] = (i+1)*(j+1);

// Use foreach to display and sum the values.
foreach(int x in nums) {
    Console.WriteLine("Value is: " + x);
    sum += x;
}
Console.WriteLine("Summation: " + sum);
}
```

此程序的输出如下所示：

Value is: 1
Value is: 2
Value is: 3
Value is: 4
Value is: 5
Value is: 2
Value is: 4
Value is: 6
Value is: 8
Value is: 10
Value is: 3
Value is: 6
Value is: 9
Value is: 12
Value is: 15
Summation: 90

由于 foreach 循环只能按顺序从头到尾遍历数组，你可能会认为它的用途有限。然而事实并非如此。大量算法恰好需要这种机制，其中最常见的一种就是搜索。例如，下面的程序使用 foreach 循环在数组中搜索一个值。如果找到该值则停止。

```csharp
// Search an array using foreach.

using System;

class Search {
    static void Main() {
        int[] nums = new int[10];
        int val;
        bool found = false;

        // Give nums some values.
        for(int i = 0; i < 10; i++)
            nums[i] = i;

        val = 5;

        // Use foreach to search nums for key.
        foreach(int x in nums) {
            if(x == val) {
                found = true;
                break;
            }
        }
        if(found)
            Console.WriteLine("Value found!");
    }
}
```

输出如下所示：

```
Value found!
```

在这种应用中，foreach 循环是一个极佳的选择，因为搜索数组涉及检查每个元素。其他类型的 foreach 应用包括计算平均值、查找一组数据的最小值或最大值、查找重复项等等。正如你将在本书后面看到的，foreach 在操作其他类型的集合时尤其有用。

## 字符串

从日常编程的角度来看，C# 的数据类型中最重要之一是 string。string 定义并支持字符字符串。在许多其他编程语言中，字符串是字符数组。在 C# 中并非如此。在 C# 中，字符串是对象。因此，string 是引用类型。虽然 string 是 C# 中的内置数据类型，但对 string 的讨论需要等到类和对象被介绍之后。

实际上，你从第 2 章开始就一直在使用 string 类，只是你不知道。当你创建一个字符串字面量时，你实际上是在创建一个字符串对象。例如，在语句

```
Console.WriteLine("In C#, strings are objects.");
```

中，字符串 "In C#, strings are objects." 会被 C# 自动转换为一个字符串对象。因此，string 类的使用在前面的程序中一直是“在表面之下”。在本节中，你将学习如何显式地处理它们。

## 构造字符串

构造字符串最简单的方法是使用字符串字面量。例如，这里 str 是一个字符串引用变量，被赋值为一个字符串字面量的引用：

```
string str = "C# strings are powerful.";
```

在这种情况下，str 被初始化为字符序列 "C# strings are powerful."。

你也可以从 char 数组创建一个字符串。例如：

```
char[] charray = {'t', 'e', 's', 't'};
string str = new string(charray);
```

一旦你创建了字符串对象，你就可以在几乎任何允许使用引号字符串的地方使用它。例如，你可以将字符串对象作为 WriteLine() 的参数，如以下示例所示：

```csharp
// Introduce string.
using System;
class StringDemo {
    static void Main() {
        char[] charray = {'A', ' ', 's', 't', 'r', 'i', 'n', 'g', '.'};
        string str1 = new string(charray);
        string str2 = "Another string.";
        Console.WriteLine(str1);
        Console.WriteLine(str2);
    }
}
```

程序的输出如下所示：

```
A string.
Another string.
```

## 操作字符串

string 类包含多个操作字符串的方法。表 7-1 显示了其中几个。string 类型还包括 Length 属性，其中包含字符串的长度。

要获取字符串中单个字符的值，只需使用索引即可。例如：

```
string str = "test";
Console.WriteLine(str[0]);
```

这会显示 “t”，即 “test” 的第一个字符。与数组一样，字符串索引从零开始。然而，有一点很重要，即你不能使用索引为字符串中的字符赋新值。索引只能用于获取字符。

| 方法 | 描述 |
|---|---|
| static string Copy(string str) | 返回 str 的副本。 |
| int CompareTo(string str) | 如果调用的字符串小于 str，则返回小于零；如果大于 str，则返回大于零；如果字符串相等，则返回零。 |
| int IndexOf(string str) | 在调用的字符串中搜索由 str 指定的子字符串。返回首次匹配的索引，若失败则返回 -1。 |
| int LastIndexOf(string str) | 在调用的字符串中搜索由 str 指定的子字符串。返回最后一次匹配的索引，若失败则返回 -1。 |
| string ToLower() | 返回调用字符串的小写版本。 |
| string ToUpper() | 返回调用字符串的大写版本。 |

表 7-1 一些常见的字符串处理方法

要测试两个字符串是否相等，可以使用 == 运算符。通常，当 == 运算符应用于对象引用时，它会判断两个引用是否指向同一对象。对于 string 类型的对象则不同。当 == 应用于两个字符串引用时，会比较字符串本身的内容是否相等。对于 != 运算符也是如此：比较字符串对象时，会比较字符串的内容。对于其他类型的字符串比较，你需要使用 CompareTo() 方法。

下面是一个演示多个字符串操作的程序：

```
// Some string operations.

using System;

class StrOps {
  static void Main() {
    string str1 =
      "When it comes to .NET programming, C# is #1.";
    string str2 = string.Copy(str1);
    string str3 = "C# strings are powerful.";
    string strUp, strLow;
    int result, idx;

    Console.WriteLine("str1: " + str1);

    Console.WriteLine("Length of str1: " +
      str1.Length);

    // Create upper- and lowercase versions of str1.
    strLow = str1.ToLower();
    strUp = str1.ToUpper();
    Console.WriteLine("Lowercase version of str1:\n  " +
      strLow);
    Console.WriteLine("Uppercase version of str1:\n  " +
      strUp);

    Console.WriteLine();

    // Display str1, one char at a time.
    Console.WriteLine("Display str1, one char at a time.");
    for(int i=0; i < str1.Length; i++)
      Console.Write(str1[i]);
    Console.WriteLine("\n");

    // Compare strings.
    if(str1 == str2)
      Console.WriteLine("str1 == str2");
    else
      Console.WriteLine("str1 != str2");

    if(str1 == str3)
      Console.WriteLine("str1 == str3");
    else
      Console.WriteLine("str1 != str3");
```

## 字符串数组

像其他任何数据类型一样，字符串也可以组合成数组。例如：

```
// Demonstrate string arrays.
using System;

class StringArrays {
    static void Main() {
        string[] str = { "This", "is", "a", "test." };
        Console.WriteLine("Original array: ");
        for(int i=0; i < str.Length; i++)
            Console.Write(str[i] + " ");
        Console.WriteLine("\n");
        // Change a string.
        str[1] = "was";
        str[3] = "test, too!";
        Console.WriteLine("Modified array: ");
        for(int i=0; i < str.Length; i++)
            Console.Write(str[i] + " ");
    }
}
```

此程序的输出如下：

```
Original array:
This is a test.

Modified array:
This was a test, too!
```

这里有一个更有趣的例子。下面的程序使用单词显示整数值。例如，值 19 将显示为 "one nine"。

```
// Display the digits of an integer using words.
using System;

class ConvertDigitsToWords {
    static void Main() {
        int num;
        int nextdigit;
        int numdigits;
        int[] n = new int[20];

        string[] digits = { "zero", "one", "two",
            "three", "four", "five",
            "six", "seven", "eight",
            "nine" };

        num = 1908;
