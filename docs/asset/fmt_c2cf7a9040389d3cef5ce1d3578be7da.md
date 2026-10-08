
```csharp
Console.WriteLine(reversed);

// 控制台输出：
// tide ME
}
static string ReverseText(string text)
{
    StringBuilder sb = new StringBuilder();
    for (int i = text.Length - 1; i >= 0; i--)
    {
        sb.Append(text[i]);
    }
    return sb.ToString();
}
```

# StringBuilder 类是如何工作的？

`StringBuilder`类是 C# 中字符串的实现，但与 `String`类不同。与我们熟悉的字符串不同，`StringBuilder`类对象不是不可变的，这意味着编辑操作不需要在内存中创建新对象。这减少了执行字符串拼接等操作时不必要的数据传输。

`StringBuilder`保留了一个具有特定容量的缓冲区（默认为 16 个字符）。缓冲区以字符数组的形式实现，并通过用户友接口提供给开发者——这些方法可以快速方便地添加和编辑字符串的元素。在任何时候，部分字符被使用，其余部分留存。这使得添加操作非常快。

一旦 `StringBuilder`的内部缓冲区满额，它会自动翻倍（调整内部缓冲区以增加其容量，同时保持内容不变）。调整大小是一个缓慢的操作，但很少发生，因此整体性能良好。我们将在“算法复杂度”章节中详细讨论这一点。

让我们创建一个缓冲区为 15 个字符的 `StringBuilder`类对象。向它添加字符串："Hello, C!"，得到下面的代码：

```
StringBuilder sb = new StringBuilder(15);
sb.Append("Hello, C!");
```

在创建对象并将值存储其中后，`StringBuilder`的外观如下：

![](img/251ffe19d2b15f8a8f566ab01924bb12_485_0.png)

有颜色的元素是缓冲区中填充了我们的内容部分。通常情况下，向变量添加新字符不会在内存中创建新对象，而是使用已经分配且未使用的空间。如果整个缓冲区容量被填满，则像我们之前解释的那样，缓冲区将翻倍。

## StringBuilder – 更重要的方法

`StringBuilder`类提供了一组方法，帮助我们轻松高效地编辑文本数据和构建文本。我们在示例中已经见过其中一些。最重要的有：

- `StringBuilder(int capacity)` – 带有初始容量参数的构造函数。如果我们对将执行的迭代次数和拼接次数有估算，可以使用它提前设置缓冲区大小。这样我们可以节省不必要的动态内存分配。
- `Capacity` – 返回缓冲区大小（缓冲区中已用和未使用位置的总数）。
- `Length` – 返回存储在变量中的字符串长度（缓冲区中已用位置的数量）。
- `Indexer [int index]` – 返回存储在指定位置的字符。
- `Append(...)` – 在缓冲区最后一个字符之后追加字符串、数字或其他值。
- `Clear()` – 从缓冲区移除所有字符（删除）。
- `Remove(int startIndex, int length)` – 从缓冲区根据指定的起始位置和长度移除（删除）字符串。
- `Insert(int offset, string str)` - 在指定的起始位置（偏移量）插入字符串。
- `Replace(string oldValue, string newValue)` - 将指定子字符串的所有出现处替换另一个子字符串。
- `ToString()` 将 `StringBuilder`对象的内容作为字符串对象返回。

## 文本提取所有大写字母 – 示例

下一个任务是从文本中提取所有大写字母。我们可以通过不同的方式来实现——使用数组、计数器并将找到的所有大写字母填充数组；创建一个 `string`类型的对象并将大写字母一个一个拼接上去；使用 `StringBuilder`类。

回到使用数组的方案，我们遇到了一个问题：我们不知道数组的大小是多少，因为我们完全不知道文本中有多少个大写字母。我们可以创建一个与文本一样大的数组，但这会浪费不必要的内存空间，而且我们必须维护一个计数器来记录数组何时已满。

另一个选项是使用 `string`类型的变量。由于我们将遍历整个文本并将所有大写字母拼接到变量中，可能会由于字符串拼接再次丢失效率。

## StringBuilder: 正确的解决方案

该任务的最可行解决方案是使用 `StringBuilder`。我们可以从一个空的 `StringBuilder`开始，逐字符遍历给定文本的字母，验证当前字符是否为大写，并将字符拼接到 `StringBuilder`的末尾。最后，我们可以通过调用 `ToString()`方法返回结果。以下是一个示例实现：

```csharp
public static string ExtractCapitals(string str)
{
    StringBuilder result = new StringBuilder();
    for (int i = 0; i < str.Length; i++)
    {
        char ch = str[i];
        if (char.IsUpper(ch))
        {
            result.Append(ch);
        }
    }
    return result.ToString();
}
```

调用 `Extract(...)`方法并传递指定文本作为参数时，返回值为文本中所有大写字母的字符串，即初始字符串去除了所有非大写字符后的结果。为了检查字符是否为大写，我们使用了 `char.IsUpper(...)` —— 这是来自标准 .NET 类的一个方法。你可以查看 `char`类的文档，因为它提供了其他处理字符的有用方法。

## 字符串格式化

.NET Framework 为开发者提供了格式化字符串、数字和日期的机制。我们在“控制台输入和输出”章节中已经遇到过了一些。现在我们将通过 `string`类中格式化和转换字符串的方法来扩展知识。

## ToString(...) 方法

.NET 中的有趣概念之一是，几乎每个类的对象都可以以文本形式呈现。这是通过 `ToString(...)`方法实现的，该方法存在于所有 .NET 对象中。它是类定义中隐式的——所有 .NET 数据类型直接或间接继承的基类。因此，该方法的定义出现在每个类中，我们可以用它以某种文本格式打印每个对象的内容。

当我们把不同类的对象打印到使用的类中时，`ToString(...)`方法会被自动调用。例如，在打印日期时，提交的日期通过调用 `ToString(...)`转换为文本：

```csharp
DateTime currentDate = DateTime.Now;
Console.WriteLine(currentDate);
// 输出: 01.02.2012 13:34:27 (取决于区域设置)
```

当我们将 `currentDate`作为 `WriteLine(...)`方法的参数传递时，我们并没有一个处理日期的准确语句。该方法对所有原始类型和字符串有特定的实现。对于所有对象，`WriteLine(...)`会调用它们的 `ToString(...)`方法，该方法先将它们转换为文本并显示生成的文本内容。事实上，上面的示例代码等同于：

```csharp
DateTime currentDate = DateTime.Now;
Console.WriteLine(currentDate.ToString());
```

对象类中 `ToString(...)`的默认实现返回类的全名。所有没有显式重定义 `ToString()`行为的类都使用这种实现。C# 中的大多数类都有自己的实现，以可读理解的形式表示内容。例如，将数字转换为文本使用的是当前区域的标准格式。将日期转换为文本也是使用当前区域的标准格式。

## 使用 String.Format(...)

`String.Format(...)`是一个静态方法，通过模板（格式化字符串）来格式化文本和其他数据。模板包含文本和声明的参数（占位符），并在替换参数值后获取格式化文本。你可以将其与 `WriteLine(...)`方法建立直接联系，后者也通过模板格式化字符串：

```csharp
Console.WriteLine("这是一个模板: {}", "David");
```

如何使用 `String.Format(...)`方法？考虑以下示例以明确：

```csharp
DateTime date = DateTime.Now;
string name = "David Scott";
string task = "Introduction to C# book";
string location = "his office";

string formattedText = String.Format(
"Today is {0:MM/dd/yyyy} and {1} is working on {2} in {3}",
date, name, task, location);
Console.WriteLine(formattedText);

// 输出: Today is 01/02/2012 and David Scott is working on
// Introduction to C# book in his office.
```

如示例所示，`String.Format`使用占位符（如 `{0}`, `{1}`）并接受格式化字符串（如 `dd.MM.yyyy`）。关于格式化字符串的更多信息可以在互联网和 MSDN 复合格式化 (http://msdn.microsoft.com/en-us/library/tfafckwd.aspx) 中找到。注意，输出的精确格式可能会根据默认区域设置略有不同。

## 解析数据

数据格式化的反操作是数据解析。数据解析（data parsing）意味着从特定格式的文本表示中获取给定类型的值，即从文本转换为其他数据类型，与 `ToString()`相反。例如，从

通过文本 `"10/22/2010"`，我们可以获取一个 `DateTime`类型的实例，其中包含相关数据。

在开发具有图形用户界面（GUI）的应用时，通常需要将用户输入传递给 `string`类型的变量。这种方法可以很好地处理数字、字符以及以用户偏好格式化的文本和日期。将预期输入数据以正确的方式呈现给用户取决于开发者的经验。数据会被转换为特定的数据类型，例如，数字可以转换为 `int`或 `double`变量，然后参与数学表达式进行计算。

> 在进行类型转换时，我们不应仅仅依赖信任用户。务始终检查输入数据的正确性！否则可能会出现改变正常程序逻辑的异常。

## 解析数值类型

要将字符串解析为数字，我们可以使用原始类型的 `Parse(...)`方法。以下是一个将字符串转换为整数值的示例：

```csharp
string text = "53";
int intValue = int.Parse(text);
// intValue = 53
```

我们也可以解析 `Boolean`类型的变量：

```csharp
string text = "True";
bool boolValue = bool.Parse(text);
// boolValue = true
```

当传递的参数已初始化（不是空值对象）且内容为 `"true"`时（无论字母大小写如何），返回值为 `true`。例如，任何如 `"true""True"`或 `"tTrue"`的文本都会将变量 `boolValue`设置为 `true`。如果参数内容为 `"false"`，无论大小写如何，返回值都为 `false`。此时会抛出 `FormatException`。

如果传递给 `Parse(...)`方法的值对于该类型无效（例如在解析数字时传递了 `"John!"`），将抛出异常。

## 解析日期

解析日期与解析为数值类型类似，但建议设置特定的日期格式。以下是这种操作的示例：

```csharp
string text = "11/11/2001";
DateTime parsedDate = DateTime.Parse(text);
Console.WriteLine(parsedDate);
// 11-Nov-01 00:00:00 AM
```

日期将成功解析，但控制台上打印的具体格式取决于 Windows 的当前区域设置（Culture）。在示例中，使用了美国文化（en-US）的修改版本。如果我们想显式设置一个不依赖于文化的格式，可以使用 `DateTime.ParseExact(...)`方法并为代码指定特定的格式模式：

```csharp
string text = "11/12/2001";
string format = "MM/dd/yyyy";
DateTime parsedDate = DateTime.ParseExact(
text, format, CultureInfo.InvariantCultureCulture);
Console.WriteLine("Day: {0}\nMonth: {1}\nYear: {2}",
parsedDate.Day, parsedDate.Month, parsedDate.Year);
// Day: 12
// Month: 11
// Year: 2001
```

使用显式设置的格式解析时，需要传递特定的文化以获取日期格式信息以及日期之间的分隔符。由于我们希望解析不依赖于特定文化，显式指定使用中性文化：`CultureInfo.InvariantCulture`。要使用 `CultureInfo`，我们必须在 C# 源代码开头包含 `System.Globalization`命名空间。

## 练习

- 描述 C# 中的字符串。`string`类型的特点是什么？解释 `string`类最重要的方法。
- 编写一个程序，读取字符串、将其反转并打印到控制台。例如：`"introduction"` -> `"noitcudortni"`。
- 编写一个程序，检查算术表达式中的括号放置是否正确。括号位置正确的表达式示例：`((a+b)/5-d)`。错误的表达式示例：`((a+b))`。
- 为了通过反斜杠分割文本，必须向 `Split(...)`方法传递多少个反斜杠？例如：`one\two\three`。

## C# 编程基础

注意：在 C# 中，反斜杠 `\`是转义字符。

5. 编写一个程序检测子字符串在文本中出现的次数。例如，在文本中查找字符串 `"in"`：

> We are living in a yellow submarine. We don't have anything else. Inside the submarine is very tight. So we are drinking all the day. We will move out of it in 5 days.

结果是出现 9 次。

6. 给定一段文本。编写一个程序将文本中被 `<uppercase>`和 `</uppercase>`标签包裹的所有字母转换为大写。标签不能不能嵌套。

示例：

> We are living in a <uppercase>yellow submarine</uppercase>. We don't have <uppercase>anything</uppercase> else.

结果：

> We are living in a YELLOW SUBMARINE. We don't HAVE ANYTHING else.

7. 编写一个程序，从控制台读取字符串（最多 20 个字符），并在不足时用 `*`补齐到 20 个字符。

# 第 13 章 字符串与文本处理

```
example@gmail.com
test.user@yahoo.co.com
```

20. 编写一个程序，从文本中提取所有格式为 DD.MM.YYYY 的日期，并按照加拿大的标准格式将其打印在控制台上。示例文本：

I was born at 14.06.1980. My sister was born at 3.7.1984. In 5/1999 I graduated my high school. The law says (see 7.3.12) that we are allowed to do this (section 7.4.2.9).

从示例文本中提取的日期：

```
14.06.1980
3.7
```

21. 编写一个程序，从文本中提取所有回文，例如 ABBA、"lamal"、exe。

22. 编写一个程序，从控制台读取一个字符串，并按字母顺序打印输入字符串中的字母以及每个字母在字符串中出现的次数。

23. 编写一个程序，从控制台读取一个字符串，并按字母顺序打印输入字符串中的所有单词以及每个单词在字符串中出现的次数。

24. 编写一个程序，从控制台读取一个字符串，并将其中每个连续的相同字母序列替换为单个字母（该重复的字母）。示例：`"aaaabbbbbcdedeedsaa"` -> `"abcdedsa"`。

25. 编写一个程序，读取一个由逗号分隔的单词列表，并在控制台上按字母顺序（排序后）打印它们。

26. 编写一个程序，从 HTML 文档中提取所有没有任何标签和属性值的纯文本。

示例文本：

```html
<<html>
<head><title>News</title></head>
<body><p><a href="http://softuni.org">Software University</a>aims to provide free real-world practical training for young people who want to turn into skillful software engineers.</p></body>
</html>
```

示例结果：

# C# 计算机编程基础

News
