
| 方法 | 描述 |
|---|---|
| Append | 将指定对象的字符串表示形式追加到此实例的末尾。 |
| AppendFormat | 将包含零个或多个格式说明符的格式化字符串追加到此实例。每个格式规范都被对应的对象参数的字符串表示形式替换。 |
| AppendLine | 将默认的行终止符，或指定字符串的副本和默认的行终止符，追加到此实例的末尾。 |
| CopyTo | 将此实例中指定段的字符复制到目标 Char 数组的指定段。 |
| Insert | 在此实例的指定字符位置插入指定对象的字符串表示形式。 |
| Remove | 从此实例中移除指定的字符范围。 |
| Replace | 用另一个指定的字符或字符串替换此实例中指定字符或字符串的所有出现。 |
| ToString | 将 StringBuilder 的值转换为 String。 |

## 正则表达式

处理字符串时，您经常需要对其进行检查，以查看它们是否匹配某些模式。例如，如果您的应用程序要求用户输入电子邮件地址，以便稍后向他们发送确认邮件，那么至少验证用户是否输入了格式正确的电子邮件地址是很重要的。为了进行检查，您可以使用本章前面学到的技术，通过手动查找电子邮件地址中的特定模式。然而，这是一项繁琐且枯燥的任务。

更好的方法是使用正则表达式——一种用于描述和操作文本的语言。使用正则表达式，您可以定义文本的模式并将其与字符串匹配。在 .NET Framework 中，System.Text.RegularExpressions 命名空间包含用于操作正则表达式的 RegEx 类。

## 搜索匹配项

要使用 RegEx 类，首先需要导入 System.Text.RegularExpressions 命名空间：

```
using System.Text.RegularExpressions;
```

## 第一部分：C# 基础

以下语句展示了如何创建 Regex 类的实例，指定要搜索的模式，并将其与字符串匹配：

```
string s = "This is a string";
Regex r = new Regex("string");
if (r.IsMatch(s))
{
    Console.WriteLine("Matches.");
}
```

在此示例中，Regex 类接受一个字符串构造函数，即您要搜索的模式。在此情况下，您正在搜索单词“string”，并将其与 s 字符串变量进行匹配。IsMatch() 方法如果存在匹配项则返回 True（即字符串 s 包含单词“string”）。

要查找变量中文本“string”的确切位置，您可以使用 Regex 类的 Match() 方法。它返回一个 Match 对象，您可以使用其 Index 属性获取与搜索模式匹配的文本的位置：

```
string s = "This is a string";
Regex r = new Regex("string");
if (r.IsMatch(s))
{
    Console.WriteLine("Matches.");
}
```

```
Match m = r.Match(s);
if (m.Success)
{
    Console.WriteLine("Match found at " + m.Index);
    //---Match found at 10---
}
```

如果字符串中有多个匹配项怎么办？在这种情况下，您可以使用 Regex 类的 Matches() 方法。此方法返回一个 MatchCollection 对象，您可以迭代遍历它以获取每个单独匹配项的索引位置：

```
string s = "This is a string and a long string indeed";
Regex r = new Regex("string");
```

```
MatchCollection mc = r.Matches(s);
foreach (Match m1 in mc)
{
    Console.WriteLine("Match found at " + m1.Index);
    //---Match found at 10---
    //---Match found at 28---
}
```

### 更复杂的模式匹配

您可以使用 *正则表达式运算符* 指定更复杂的搜索。例如，要知道字符串是否包含单词 "Mr" 或 "Mrs"，您可以使用运算符 |，如下所示：

```
string gender = "Mr Wei-Meng Lee";
Regex r = new Regex("Mr|Mrs");
if (r.IsMatch(gender))
{
    Console.WriteLine("Matches.");
}
```

下表描述了在搜索模式中常用的正则表达式运算符。

| 操作符 | 描述 |
| --- | --- |
| . | 匹配任意一个字符 |
| [ ] | 匹配方括号之间列出的任意一个字符 |
| [^ ] | 匹配方括号之间未列出的任意一个字符 |
| ? | 如果存在则匹配任意字符一次 |
| * | 如果存在则多次匹配已声明的元素 |
| + | 匹配已声明的元素一次或多次 |
| {n} | 精确匹配已声明的元素 n 次 |
| {n,} | 至少匹配已声明的元素 n 次 |
| {n,N} | 至少匹配已声明的元素 n 次，但不超过 N 次 |
| ^ | 匹配行开头 |
| $ | 匹配行结尾 |
| \< | 匹配单词开头 |
| \> | 匹配单词结尾 |
| \b | 匹配单词开头或结尾 |
| \B | 匹配单词中间 |
| \d | 数字（0-9）的简写 |
| \w | 单词字符（字母和数字）的简写 |
| \s | 空白字符的简写 |

## 第一部分：C# 基础

另一个常见的搜索模式是验证包含日期的字符串。例如，如果字符串包含格式为 "yyyy/mm/dd" 的日期，您将按如下方式指定搜索模式："[19|20]\d\d[- /.]{0[1-9]|1[012]}[- /.]{0[1-9]|1[012]}"。此模式将匹配从 1900-01-01 到 2099-12-31 的日期。

```
string date = "2007/03/10";
Regex r = new Regex(@"[19|20]\d\d[- /.]{0[1-9]|1[012]}[- /.]{0[1-9]|1[012]}");
if (r.IsMatch(date))
{
    Console.WriteLine("Matches.");
}
```

您可以使用以下日期分隔符与上面指定的模式一起使用：

```
string date = "2007/03/10";
string date = "2007-03-10";
string date = "2007 03 10";
string date = "2007.03.10";
```

一些常用的搜索模式在下表中描述。

| 模式 | 描述 |
|---|---|
| [0-9] | 数字 |
| [A-Fa-f0-9] | 十六进制数字 |
| [A-Za-z0-9] | 字母数字字符 |
| [A-Za-z] | 字母字符 |
| [a-z] | 小写字母 |
| [A-Z] | 大写字母 |
| [ \t] | 空格和制表符 |
| [\x00-\x1F\x7F] | 控制字符 |
| [\x21-\x7E] | 可见字符 |
| [\x20-\x7E] | 可见字符和空格 |
| [!"#$%&'()*+,-./:;<=>?@\[\]_`{|}~] | 标点字符 |
| [ \t\r\n\v\f] | 空白字符 |
| \w+([.-+]?\w+)*@\w+([.-]\w+)*\.\w+([.-]\w+)* | 电子邮件地址 |
| http(s)?://([\w-]+\.)+([\w-]+)(/[\w- ./?%&=]*)? | 互联网 URL |
| \(\(\d{3}\)\s?\)?\|\d{3}-\)?\d{3}-\d{3} | 美国电话号码 |
| \d{3}-\d{2}-\d{4} | 美国社会安全号码 |
| \d{5}(-\d{4})? | 美国邮政编码 |

要验证电子邮件地址是否格式正确，您可以使用以下语句与指定的正则表达式一起使用：

```
string email = "weimenglee@learn2develop.net";
Regex r = new Regex(@"^[\w\.-]+@[\w-]+\.[\w-]{2,4}$");
if (r.IsMatch(email))
    Console.WriteLine("Email address is correct.");
else
    Console.WriteLine("Email address is incorrect.");
```

您可以使用许多不同的正则表达式来验证电子邮件地址。然而，没有完美的正则表达式可以验证所有电子邮件地址。有关使用正则表达式验证电子邮件地址的更多信息，请查看以下网站：http://regular-expressions.info/email.html 和 http://fightingforalostcause.net/misc/2006/compare-email-regex.php。

## 摘要

字符串操作是常见的操作，因此了解它们的工作原理以及处理它们的各种方法和类非常重要。本章提供了大量关于 C# 中字符串表示以及使用正则表达式对字符串进行匹配的信息。

## 泛型

.NET Framework（从 2.0 版本开始）中的新功能之一是对 Microsoft Intermediate Language（MSIL）中泛型的支持。泛型使用类型参数，允许您设计类和方法，将一个或多个类型的指定推迟到客户端代码声明和实例化该类或方法时。泛型使开发人员能够在设计时不绑定到特定固定数据类型的情况下定义类型安全的数据结构。

泛型是 IL 的特性，而非仅限于 C#，因此 C# 和 VB.NET 等语言可以利用它们。

本章讨论泛型的基础知识以及如何使用它们来提高应用程序的效率和类型安全性。具体来说，您将学习：
- 使用泛型的优点
- 如何在泛型类型中指定约束
- 泛型接口、结构体、方法、运算符和委托
- .NET Framework 类库中支持泛型的各种类

## 理解泛型

让我们看一个例子来了解泛型的工作原理。假设您需要实现自己的自定义栈类。栈是一种后进先出（LIFO）数据结构，使您能够将项目推入栈并从栈中弹出项目。一个可能的实现是：

```
public class MyStack
{
    private int[] _elements;
    private int _pointer;

    public MyStack(int size)
    {
        _elements = new int[size];
```
