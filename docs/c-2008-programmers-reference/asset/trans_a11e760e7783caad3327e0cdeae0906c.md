

## 第 I 部分：C# 基础

> > 默认情况下，当你使用 \n 插入新行时，光标会自动返回到该行的开头。然而，某些旧式应用程序仍然要求你在字符串中插入换行符和回车符。

![](img/a977a875c7c627b45d939729705a252e_269_0.png)

下表总结了你在本节中见过的不同转义序列：

| 序列 | 用途 |
| --- | --- |
| \n | 换行 |
| \r | 回车 |
| \r\n | 回车、换行 |
| \" | 双引号 |
| \\ | 反斜杠字符 |
| \t | 制表符 |

在 C# 中，字符串也可以采用 @ 引号形式。前面你已经看到，要在字符串中包含特殊字符（例如双引号、反斜杠等），需要使用反斜杠字符来关闭其特殊含义：

```csharp
string path="C:\\Windows";
```

实际上你可以使用 @ 字符，并将其作为字符串的前缀，像这样：

```csharp
string path=@"C:\Windows";
```

使用 @ 字符可使字符串更易读。基本上，编译器会逐字处理以 @ 字符为前缀的字符串——也就是说，它只是接受字符串（引号内）的所有字符。为了更好地理解这一点，请考虑以下示例，其中包含 XML 片段的字符串被分成多行（每行以回车结尾）：

```csharp
string XML = @"
    <Books>
        <title>C# 3.0 Programmers' Reference</title>
    </Books>";
Console.WriteLine(XML);
```

图 8-7 显示了输出。`WriteLine()` 方法会逐字打印该行。

![](img/a977a875c7c627b45d939729705a252e_270_0.png)

图 8-7

为了说明在双引号字符串中使用 @ 字符的情况，以下代码：

```
string quotation =
    "\"I don't necessarily agree with everything I say.\" Marshall McLuhan";
Console.WriteLine(quotation);
```

可以改写为：

```
string quotation =
    @"""I don't necessarily agree with everything I say."" Marshall McLuhan";
Console.WriteLine(quotation);
```

### Unicode 转义码

C# 支持使用转义码表示 Unicode 字符。四位转义码格式为：`\udddd`。例如，以下语句打印出 £ 符号：

```csharp
string symbol = "\u00A3";
Console.WriteLine(symbol);
```

有关 Unicode 的更多信息，请访问 http://unicode.org/Public/UNIDATA/NamesList.txt。

## 字符串操作

通常，将值存储在字符串变量中后，你需要对它们执行各种操作，例如比较两个字符串的值、在现有字符串中插入和删除字符串、连接多个字符串等。.NET Framework 中的 `String` 类提供了大量用于操作字符串的方法，其中一些重要方法将在以下各节中说明。

*你可以在 www.msdn.com 上了解所有 String 类方法。*

## 第 8 章：字符串和正则表达式

可以使用 `String.Compare()` 静态方法比较两个字符串：

```
Console.WriteLine(string.Compare(str1, str2));    // 1; str1 is greater than str2
Console.WriteLine(string.Compare(str2, str1));    // -1; str2 is less than str1
Console.WriteLine(string.Compare(str1, str2, true)); // 0; str1 equals str2
```

小写字符“m”排在大写“M”之前，因此 str1 被认为大于 str2。第三条语句在不考虑大小写（即不区分大小写）的情况下比较两个字符串；正是第三个参数表明比较应忽略所涉及字符串的大小写。

`String.Compare()` 静态方法已重载；除了刚才展示的两个重载方法（前两条语句和第三条语句）之外，下表中还描述了其他重载方法。

| 方法 | 描述 |
|---|---|
| `Compare(String, String)` | 比较两个指定的 String 对象。 |
| `Compare(String, String, Boolean)` | 比较两个指定的 String 对象，忽略或考虑其大小写。 |
| `Compare(String, String, StringComparison)` | 比较两个指定的 String 对象。还指定比较使用当前区域性还是固定区域性、遵循或考虑大小写，以及使用单词排序规则还是序号排序规则。 |
| `Compare(String, String, Boolean, CultureInfo)` | 比较两个指定的 String 对象，忽略或考虑其大小写，并使用区域性特定信息进行比较。 |
| `Compare(String, Int32, String, Int32, Int32)` | 比较两个指定 String 对象的子字符串。 |
| `Compare(String, Int32, String, Int32, Int32, Boolean)` | 比较两个指定 String 对象的子字符串，忽略或考虑其大小写。 |
| `Compare(String, Int32, String, Int32, Int32, StringComparison)` | 比较两个指定 String 对象的子字符串。 |
| `Compare(String, Int32, String, Int32, Int32, Boolean, CultureInfo)` | 比较两个指定 String 对象的子字符串，忽略或考虑其大小写，并使用区域性特定信息进行比较。 |

或者，你可以使用 `CompareTo()` 实例方法，像这样：

```
Console.WriteLine(str1.CompareTo(str2)); // 1; str1 is greater than str2
Console.WriteLine(str2.CompareTo(str1)); // -1; str2 is less than str1
```

注意，由 `CompareTo()` 实例方法进行的比较始终区分大小写。

## 创建和连接字符串

.NET Framework 中的 `String` 类提供了许多方法，使你能够创建或连接字符串。

连接两个字符串最直接的方法是使用“+”运算符，像这样：

```
    string str1 = "Hello ";
    string str2 = "world!";
    string str3 = str1 + str2;
    Console.WriteLine(str3); //---Hello world!---
```

`String.Format()` 静态方法接收多个对象的输入并创建一个新字符串。请考虑以下示例：

```
    string Name = "Wei-Meng Lee";
    int age = 18;
    string str1 = string.Format("My name is {0} and I am {1} years old",
                            Name, age);

    //---str1 is now "My name is Wei-Meng Lee and I am 18 years old"---
    Console.WriteLine(str1);
```

注意，你提供了 `string` 和 `int` 类型的两个变量，`Format()` 方法会自动将它们组合起来返回一个新字符串。

前面的示例可以使用 `String.Concat()` 静态方法改写，像这样：

```
    string str1 = string.Concat("My name is ", Name, " and I am ", age ,
                            " years old");
    //---str1 is now "My name is Wei-Meng Lee and I am 18 years old"---
    Console.WriteLine(str1);
```

> > **字符串是不可变的**
> >
> > 在 .NET 中，所有字符串对象都是*不可变的*。这意味着一旦字符串变量被初始化，它的值就不能更改。而当你修改字符串的值时，会创建该字符串的新副本，并丢弃旧副本。因此，所有处理字符串的方法都会返回修改后字符串的副本——原始字符串保持不变。
> >
> > 例如，`Insert()` 实例方法将字符串插入当前字符串并返回修改后的字符串：
> >
> >     str1 = str1.Insert(10, "modified ");
> >
> > 在此语句中，必须将返回的结果赋给原始字符串，以确保新字符串被修改。

要查找某个单词出现的位置，请使用 IndexOf() 和 LastIndexOf() 实例方法。IndexOf() 返回字符串中特定单词第一次出现的位置，而 LastIndexOf() 返回该单词最后一次出现的位置。下面是一个示例：

```
string str1 = "This is a long long long string...";
Console.WriteLine(str1.IndexOf("long")); //---10---
Console.WriteLine(str1.LastIndexOf("long")); //---20---
```

要查找某个单词的所有出现位置，可以使用 IndexOf() 方法编写一个简单的循环，像这样：

```
int position = -1;
string str1 = "This is a long long long string...";
do
{
    position = str1.IndexOf("long", ++position);
    if (position > 0)
        Console.WriteLine(position);
} while (position > 0);
```

这会打印出以下内容：

10
15
20

要搜索特定字符的出现位置，请使用 IndexOfAny() 实例方法。以下语句在 str1 字符串中搜索 char 数组中指定的 a、b、c、d 或 e 中的任意字符：

```
char[] anyof = "abcde".ToCharArray();
Console.WriteLine(str1.IndexOfAny(anyof)); //---8---
```

要从字符串中获取子字符串，请使用 Substring() 实例方法，如下例所示：

```
string str1 = "This is a long string...";
string str2;
Console.WriteLine(str1.Substring(10)); //---long string...---
Console.WriteLine(str1.Substring(10, 4)); //---long---
```

要判断字符串是否以特定字符串开头，请使用 StartsWith() 实例方法。同样，要判断字符串是否以特定字符串结尾，请使用 EndsWith() 实例方法。以下语句说明了这一点：

```
Console.WriteLine(str1.StartsWith("This")); //---True---
Console.WriteLine(str1.EndsWith("...")); //---True---
```

