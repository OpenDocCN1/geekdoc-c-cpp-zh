
## 第13章：字符串连接

### 第13.1节：+ 运算符

```csharp
string s1 = "string1";
string s2 = "string2";

string s3 = s1 + s2; // "string1string2"
```

### 第13.2节：使用 System.Text.StringBuilder 连接字符串

使用 `StringBuilder` 连接字符串与使用 + 进行简单的字符串连接相比可以提供性能优势。这是因为内存分配方式的不同。Strings are reallocated with each concatenation, StringBuilder allocate memory in blocks only reallocating when the current block is exhausted. This can make a huge difference when doing a lot of small concatenations.

```csharp
StringBuilder sb = new StringBuilder();
for (int i = 1; i <= 5; i++)
{
    sb.Append(i);
    sb.Append(" ");
}
Console.WriteLine(sb.ToString()); // "1 2 3 4 5 "
```

对 `Append()` 的调用可以串联，因为它返回对 `StringBuilder` 的引用：

```csharp
StringBuilder sb = new StringBuilder();
sb.Append("some string ")
  .Append("another string");
```

### 第13.3节：使用 String.Join 连接字符串数组元素

`String.Join` 方法可用于连接字符串数组中的多个元素。

```csharp
string[] value = {"apple", "orange", "grape", "pear"};
string separator = ", ";

string result = String.Join(separator, value, 1, 2);
Console.WriteLine(result);
```

> 生成以下输出："orange, grape"

此示例使用 `String.Join(String, String[], Int32, Int32)` 重载，它在分隔符和值之上指定起始索引和计数。

如果您不想使用 startIndex 和 count 重载，可以连接所有给定的字符串。像这样：

```csharp
string[] value = {"apple", "orange", "grape", "pear"};
string separator = ", ";
string result = String.Join(separator, value);
Console.WriteLine(result);
```

将产生：

> apple, orange, grape, pear

### 第13.4节：使用 $ 连接两个字符串

$ 提供了一种简便且简洁的方法来连接多个字符串。

```csharp
var str1 = "text1";
var str2 = " ";
var str3 = "text3";
string result2 = $"{str1}{str2}{str3}"; //"text1 text3"
```

## 第14章：字符串操作

### 第14.1节：在字符串中替换字符串

使用 System.String.Replace 方法，您可以将字符串的一部分替换为另一个字符串。

```csharp
string s = "Hello World";
s = s.Replace("World", "Universe"); // s = "Hello Universe"
```

搜索字符串的所有出现位置都会被替换：

```csharp
string s = "Hello World";
s = s.Replace("l", "L"); // s = "Hello WorlD"
```

String.Replace 还可通过指定空字符串作为替换值来删除字符串的一部分：

```csharp
string s = "Hello World";
s = s.Replace("ell", String.Empty); // s = "Ho World"
```

### 第14.2节：在字符串中查找字符串

使用 System.String.Contains 可以判断特定字符串是否存在于字符串中。该方法返回布尔值，如果字符串存在则为 true，否则为 false。

```csharp
string s = "Hello World";
bool stringExists = s.Contains("ello"); //stringExists =true as the string contains the substring
```

使用 System.String.IndexOf 方法，可以定位子字符串在现有字符串中的起始位置。

请注意返回的位置是基于零的，如果未找到子字符串，则返回 -1。

```csharp
string s = "Hello World";
int location = s.IndexOf("ello"); // location = 1
```

要从字符串末尾查找第一个位置，请使用 System.String.LastIndexOf 方法：

```csharp
string s = "Hello World";
int location = s.LastIndexOf("l"); // location = 9
```

### 第14.3节：从字符串中删除（修剪）空白

System.String.Trim 方法可用于从字符串中删除所有前导和尾随空白字符：

```csharp
string s = "      String with spaces at both ends      ";
s = s.Trim(); // s = "String with spaces at both ends"
```

此外：

- 仅从字符串开头删除空白，请使用：System.String.TrimStart
- 仅从字符串末尾删除空白，请使用：System.String.TrimEnd

### 子字符串以提取字符串的一部分。

System.String.Substring 方法可用于提取字符串的一部分。

```csharp
string s = "A portion of word that is retained";
s = s.Substring(26); //s="retained"
s1 = s.Substring(0,5); //s="A por"
```

### 第14.4节：使用分隔符拆分字符串

使用 System.String.Split 方法返回一个字符串数组，其中包含基于指定分隔符拆分的原始字符串的子字符串：

```csharp
string sentence = "One Two Three Four";
string[] stringArray = sentence.Split(' ');

foreach (string word in stringArray)
{
    Console.WriteLine(word);
}
```

输出：

- One
- Two
- Three
- Four

### 第14.5节：将字符串数组连接成单个字符串

System.String.Join 方法允许使用指定的分隔符在每个元素之间连接字符串数组中的所有元素：

```csharp
string[] words = {"One", "Two", "Three", "Four"};
string singleString = String.Join(",", words); // singleString = "One,Two,Three,Four"
```

### 第14.6节：字符串连接

字符串连接可以通过使用 System.String.Concat 方法或（更简单）使用 + 运算符来完成：

```csharp
string first = "Hello ";
string second = "World";

string concat = first + second; // concat = "Hello World"
concat = String.Concat(first, second); // concat = "Hello World"
```

### 第14.7节：更改字符串中字符的大小写

System.String 类支持多种方法，可在字符串中在大写和小写字符之间转换。

- System.String.ToLowerInvariant 用于返回转换为小写的 String 对象。
- System.String.ToUpperInvariant 用于返回转换为大写的 String 对象。

**注意：** 使用这些方法的 *invariant* 版本的原因是为了防止产生意外的特定于文化的字母。这在 [此处详细说明](#)。

示例：

```csharp
string s = "My String";
s = s.ToLowerInvariant(); // "my string"
s = s.ToUpperInvariant(); // "MY STRING"
```

请注意，您可以通过相应地使用 [String.ToLower(CultureInfo)](#) 和 [String.ToUpper(CultureInfo)](#) 方法在转换大小写时指定特定的 **Culture**。

## 第15章：字符串插值

### 第15.1节：在字符串中格式化日期

```csharp
var date = new DateTime(2015, 11, 11);
var str = $"It's {date:MMMM d, yyyy}, make a wish!";
System.Console.WriteLine(str);
```

您还可以使用 DateTime.ToString 方法来格式化 DateTime 对象。这将产生与上面代码相同的输出。

```csharp
var date = new DateTime(2015, 11, 11);
var str = date.ToString("MMMM d, yyyy");
str = "It's " + str + ", make a wish!";
Console.WriteLine(str);
```

### 输出：

It's November 11, 2015, make a wish!

在 .NET Fiddle 上实时演示

使用 DateTime.ToString 的实时演示

> 注意：MM 代表月份，mm 代表分钟。使用时务必非常小心，因为错误可能会引入难以发现的 bug。

### 第15.2节：填充输出

字符串可以格式化为接受填充参数，该参数将指定插入字符串将使用的字符位置数：

```
${value, padding}
```

生命、宇宙以及一切的答案是 42。

在 .NET Fiddle 上实时演示

### 右填充

右填充使用负填充值，会在当前值的末尾添加空格。

```csharp
var number = 42;
var str = $"The answer to life, the universe and everything is {number, -5}.";
//str is "The answer to life, the universe and everything is 42   .";
//                                      ^^^^^
System.Console.WriteLine(str);
```

### 输出：

The answer to life, the universe and everything is 42   .

在 .NET Fiddle 上实时演示

### 使用格式说明符填充

您也可以将现有的格式说明符与填充结合使用。

```csharp
var number = 42;
var str = $"The answer to life, the universe and everything is {number, 5:f1}";
//str is "The answer to life, the universe and everything is 42.1 ";
//                                      ^^^^^
```

在 .NET Fiddle 上实时演示

### 第15.3节：表达式

完整的表达式也可以在插值字符串中使用。

```csharp
var StrWithMathExpression = $"1 + 2 = {1 + 2}"; // -> "1 + 2 = 3"

string world = "world";
var StrWithFunctionCall = $"Hello, {world.ToUpper()}!"; // -> "Hello, WORLD!"
```

在 .NET Fiddle 上实时演示

### 第15.4节：在字符串中格式化数字

您可以使用冒号和标准数字格式语法来控制数字的格式。

```csharp
var decimalValue = 120.5;

var asCurrency = $"It costs {decimalValue:C}";
// String value is "It costs $120.50" (depending on your local currency settings)

var withThreeDecimalPlaces = $"Exactly {decimalValue:F3}";
// String value is "Exactly 120.500"

var integerValue = 57;
```
