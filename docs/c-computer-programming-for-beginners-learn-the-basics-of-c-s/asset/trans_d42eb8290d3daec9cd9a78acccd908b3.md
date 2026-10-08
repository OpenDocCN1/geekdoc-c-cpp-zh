
整数，它们也可以是其他类型，例如 C# 中的字符串（string）。

# 字符串介绍

在 C# 中，字符串可以作为字符数组使用。尽管如此，通常的做法是使用 `string` 关键字来声明一个存储变量。你必须记住，`string` 关键字仅仅是 `System.String` 类的别名。

# 字符串对象的创建

字符串对象可以通过以下任何一种过程创建。

- * *通过将字符串字面量赋值给 `String` 变量*
- 使用 `String` 类的构造函数
- 通过获取属性或调用可以返回字符串的方法。
- 使用字符串拼接运算符 `+`
- 通过调用格式化方法，该方法可以将对象或值转换为相应的字符串表示。

下面的示例说明了字符串对象的创建。

```csharp
using System;
namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
// 来自字符串字面量和字符串拼接
string fname, lname;

fname = "John";
lname = "Smith";
string fullname = fname + lname;

Console.WriteLine("Full Name: {0}", fullname);

// 使用字符串构造函数
char[] letters = { 'H', 'e', 'T', 'o' };

string greetings = new string(letters);
Console.WriteLine("Greetings: {0}", greetings);

// 返回字符串的方法
string[] array = { "Hello", "From", "The", "Earth" };
string message = String.Join(" ", array);
Console.WriteLine("Message: {0}", message);

// 用于转换值的格式化方法
DateTime waiting = new DateTime(2016, 10, 10, 17, 58, 1);

string chat = String.Format("Message sent at {0:t} on {0:D}", waiting);

Console.WriteLine("Message: {0}", chat);

}
}
```

在编译并执行上述代码后，将产生以下结果。

Full Name: Rowan Atkinson

Greetings: Hello

Message: Hello From The Earth Message sent at 5:58 PM on Wednesday, October 10, 2016

# String 类属性

`String` 类拥有两个属性。它们描述如下。

- Chars: 获取给定字符串对象中指定位置的 `Char` 对象。
- Length: 获取给定字符串对象中字符的总数。

# String 类中存在的方法

`String` 类中提供了许多可用方法。当你处理字符串对象时，这些方法会非常有帮助。以下是一些常用方法。

```csharp
public static int Compare(string strA, string strB)
```

这将比较两个字符串对象。它将返回一个整数，表示对象在排序顺序中的相对位置。

```csharp
public static int Compare(string strA, string strB, bool ignoreCase )
```

这也会比较两个字符串对象，并返回一个表示对象在排序顺序中的相对位置的整数。尽管如此，当布尔参数为 `true` 时，它将忽略大小写。

```csharp
public static string Concat(string str0, string str1)
```

这将拼接两个字符串对象。可以增加正在拼接的字符串对象的数量。

```csharp
public bool Contains(string value)
```

它将返回一个值，表示给定字符串是否存在于字符串中。

```csharp
public static string Copy(string str)
```

这将创建一个与给定字符串具有相同值的新 `String` 对象。

```csharp
public bool EndsWith(string value)
```

这将确定给定字符串对象的末尾是否与给定字符串匹配。

```csharp
public static bool Equals(string a, string b)
```

这将确定两个 `String` 对象是否具有完全相同的值。

```csharp
public int IndexOf(char value)
```

这将返回字符在字符串中的索引。将提供字符首次出现位置的从 0 开始的索引。

```csharp
public static string Format(string format, Object arg)
```

这将替换给定字符串中的一个或多个项目。它们将被替换为给定对象的字符串表示。

```csharp
public string Insert(int startIndex, string value)
```

这将返回一个新字符串，该字符串在给定字符串的特定位置插入了给字符串。

```csharp
public static bool IsNullOrEmpty(string value)
```

这指示给定字符串是否为 `null` 或空字符串。

```csharp
public static string Join(string separator, string[] value)
```

这将使用每个元素之间的分隔符拼接数组中的所有元素。

```csharp
public static string Join(string separator, string[] value, int startIndex, int count)
```

这将使用每个元素之间的分隔符拼接字符串的元素。

```csharp
public int LastIndexOf(char value)
```

这返回当前对象内部字符的索引位置。将使用从 0 开始的索引位置，且仅提到最后一次出现。

public string Remove(int startIndex)

这将删除从当前实例的指定位置开始的所有字符。它将持续到最后一个位置。最后，将返回字符串。

`String` 类还有许多其他方法和构造函数。MSDN 库包含了完整列表。现在，让我们来看几个示例，演示如何使用上述某些方法。

下面的示例说明了如何使用上述某些方法。

（此处省略重复的示例代码翻译逻辑）
