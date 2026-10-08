
```csharp
string alpha = "alpha";
string score1 = "sCoRE";
string score2 = "score";

Console.WriteLine(string.Compare(alpha, score1, false));
Console.WriteLine(string.Compare(score1, score2, false));
Console.WriteLine(string.Compare(score1, score2, true));
Console.WriteLine(string.Compare(score1, score2, 
StringComparison.CurrentCultureIgnoreCaseCase));
// Console output:
// -1
// 1
// 0
// 0
```

在最后一个示例中，`Compare(...)` 方法的第三个参数是 `StringComparison.CurrentCultureIgnoreCase` - 这通过 `Equals(...)` 方法已经很熟悉，通过我们也可以比较字符串，而无需注册大小写字母的区别。

请注意，根据字典序的 `Compare(...)` 和 `CompareTo(...)`，小写字母在字典序上在大写字母之前。该规则的正确性在 Unicode 表中非常有争议，Unicode 中大写字母在小写字母之前。例如，根据标准 Unicode，字母 "A" 的编码为 65，小于字母 "a" 的编码 `97`。

> 当你只是想考虑两个字符串的值是否相等时，请使用 `Equals(...)` 方法或运算符 `==`。`CompareTo(...)` 和 `string.Compare(...)` 方法设计用于需要字典序排列的情况。

因此，你应该考虑字典序比较并不遵循 Unicode 表中的字母排列。其他异常也由当前文化的特殊特性引起。在某些语言中（如德语），"ss" 和 "ß" 被认为是相同的。例如，通过 `==` 运算符比较 "Straße" 和 "Strasse"，它们在字典序上被认为是相等的：

## `==` 和 `!=` 运算符

在 C# 语言中，`==` 和 `!=` 运算符通过 `Equals(...)` 方法工作。我们将通过一些示例来看这些运算符：

```csharp
string str1 = "Hello";
string str2 = "Hello";

Console.WriteLine(str1 == str2);
// Console output:
// True
```

注意 `str1` 和 `str2` 之间的比较。第一个变量获取值 "Hello"。第二个变量通过字面量获取其值。此时两个变量指向不同的内存区域，但内存块的内容是相同的。以下是内存情况如下所示：

![](img/251ffe19d2b158a8f56ab0192bb465.png)

让我们来看另一个示例：

```csharp
string hel = "Hel";
string hello = "Hello";
string copy = hel + "lo";
```

```csharp
Console.WriteLine(copy == hello);
// Console output:
// True
```

注意 `hello` 和 `copy` 之间的比较。第一个变量获取值 "Hello"。第二个变量通过连接变量与字面量获取值，最终结果等于第一个变量的值。在此阶段两个变量指向相同的区域，通过 `==` 运算符进行的相等检查返回 `true`。

此时内存看起来如下：

| Stack | Heap |

| --- | --- |

| hel string@6e278a | Hel |

| hello string@2fa8fc | Hello |

| copy string@a7b46e |

## 内存优化（池化）

考虑以下示例：

```csharp
string hello = "Hello";
string same = "Hello";
```

我们创建一个值为 "Hello" 的变量。我们又创建一个变量并分配相同的字面量。在创建变量 **hello** 时，逻辑上要在堆中分配空间，写入其值并让变量指向该位置。在创建 **same** 时，也应该分配一个新位置进行记录，写入值并将引用指向内存。

但事实是，C# 编译器和 CLR 中存在一种优化，可以**节省创建重复字符串的内存**。这种优化被称为字符串池化（interning），得益于此，内存中的两个变量将指向同一个公共块。这减少了内存空间的使用并优化了某些操作，例如比较两个相同的字符串。它们在内存中的写入方式如下：

| Stack | Heap |

| --- | --- |

| hello string@a8fe24 | Hello |

| same string@a8fe24 | |

当我们使用字面量初始化 **string** 类型变量时，内存会无地检查该变量是否已存在。如果变量已存在，则分配一个新的内存块，在其中存储值并更改引用指向

# C# 计算机编程基础

新的块。.NET 中的字符串池化（string interning）之所以可行，是因为字符串在设计上是不可变的，这意味着多个字符串变量引用的内存块不会被任何人同时更改。

在用字面量初始化字符串时，会使用字符串池化。然而，如果我们想专门使用字符串池化，可以通过使用 `Intern()` 方法来实现：

```csharp
string declared = "Intern pool";
built = new StringBuilder("Intern pool").ToString();
string interned = string.Intern(built);

Console.WriteLine(object.ReferenceEquals(declared, built));
Console.WriteLine(object.ReferenceEquals(declared, interned));
// Console output:
// False
// True
```

此时的内存情况如下：

![](img/251ffe19d2b15f8a8f566ab01924bb12_467_0.png)

在示例中，我们使用了静态方法 `Object.ReferenceEquals(...)`，它比较内存中的两个对象并返回它们是否指向同一个内存块。我们使用了 `StringBuilder` 类，它用于高效地构建字符串。我们稍后会详细解释何时以及如何使用 `StringBuilder`，但现在让我们熟悉字符串的基本操作。

# 字符串处理操作

一旦熟悉了字符串的基础知识及其结构，下一步要探索的是处理这些字符串的工具。我们将回顾字符串拼接、在字符串中搜索、提取子字符串、更改字符大小、通过分隔符分割字符串以及其他帮助我们解决日常实践中各种问题的字符串操作。

# 第 13 章 字符串与文本处理

> 字符串是不可变的！任何对 string 类型变量的更改都会创建一个存储该结果的新字符串。因此，应用于字符串的操作会返回结果的引用。

为了在处理字符串时不在每次修改时都向内存中创建新对象，为此应该使用 `StringBuilder` 类。我们稍后会介绍它。

## 字符串拼接

将两个字符串合并并获得一个新的字符串的结果称为拼接。可以通过多种方式实现 `Concat(...)` 或使用运算符 `+` 和 `+=`：

使用 `Concat():` 方法的示例：

```csharp
string greet = "Hello, ";
string name = "reader";
string result = string.Concat(greet, name);
```

通过调用该方法，我们将作为参数传递的字符串变量 `name` 拼接到字符串 `greet` 上。结果字符串将是文本 "Hello, reader"。

拼接的第二种方法是通过运算符 `+` 和 `+=`。那么上面的示例可以用以下方式实现：

```csharp
string greet = "Hello, ";
string name = "reader";
string result = greet + name;
```

在两种情况下，这些变量在内存中的呈现形式如下：

| Stack | Heap |

| :--- | :--- |

| greet | |

| 0x0122F680 | Hello, |

| name | |

| 0x003456FF | reader! |

| result | |

| 0x00AD4934 | Hello, reader! |

请注意，字符串拼接不会更改现有的字符串，而是返回一个新的字符串作为结果。如果我们尝试拼接两个字符串而不将它们存储在变量中，更改将不会保存。这是一个典型的错误：

```csharp
string greet = "Hello, ";
string name = "reader";
string.Concat(greet, name);
```

在给定的示例中，两个变量被拼接了，但结果没有被保存，因此它丢失了：

如果我们想给现有变量（例如 `result` 变量）添加一个值，可以使用著名的代码：

```csharp
result = result + "How are you?";
```

为了避免对上述声明的变量进行双写，可以使用运算符 `+=`：

```csharp
result += "How are you?";
```

两种情况的结果将都是：“Hello, reader! How are you?”。我们可以将其他数据与字符串拼接。任何以文本格式呈现的数据都可以附加到字符串上。数字、字符、日期等都可以进行拼接。这里有一个示例：

```csharp
string message = "The number of the beast is: ";
int beastNum = 666;
string result = message + beastNum;
// The number of the beast is: 666
```

从上面的示例中我们可以了解到，将字符串与非字符串类型的数据拼接没有问题。让我们再看另一个字符串拼接的示例：

```csharp
public class DisplayUserInfo
{
    static void Main()
    {
        string firstName = "John";
        string lastName = "Smith";
        string fullName = firstName + " " + lastName;

        int age = 28;
        string nameAndAge = "Name: " + fullName + "\nAge: " + age;
        Console.WriteLine(nameAndAge);
    }
}
// Console output:
// Name: John Smith
// Age: 28
```

# 转换为大写和小小写字母

有时我们需要更改字符串的大小写，使其中的所有字符完全大写或完全小写。在这种情况下，有效的两种方法是 `ToLower(...)` 和 `ToUpper(...)`。第一种将所有大写字母转换为小写：

```csharp
string text = "All Kind of Letters";
Console.WriteLine(text.ToLower());
// all kind of letters
```

示例显示我们可以将文本转换为小写。第二种方法将大字母转换为大写：

```csharp
string text = "All Kind of Letters";
Console.WriteLine(text.ToUpper());
// ALL KIND OF LETTERS
```

## 在另一个字符串中搜索字符串

当我们有一个包含特定内容的字符串时，通常需要处理其值的一部分。NET平台为我们提供了两种方法在另一个字符串中搜索字符串：`IndexOf(...)` 和 `LastIndexOf(...)`。它们搜索字符串并检查作为参数传递的子字符串是否找到。这些方法的结果是一个整数。如果结果不是负值，则它是找到子字符串第一个字符的位置。记住，C# 的索引从 0 开始。

`IndexOf(...)` 和 `LastIndexOf(...)` 方法搜索文本序列的内容，但方向不同。第一种方法的搜索从字符串的开始到结束，而第二种方法——搜索是反向的。如果我们对遇到的第一个匹配项感兴趣，则使用 `IndexOf(...)`。如果我们想从字符串末尾搜索字符串（例如检测文件名或 URL 地址中的最后一个斜杠），则使用 `LastIndexOf(...)`。

当调用 `IndexOf(...)` 和 `LastIndexOf(...)` 时，可以传递第二个参数，它将指定搜索开始的位置。如果我们想搜索字符串的一部分而不是整个字符串，这非常有用。

## 搜索字符串 - 示例

让我们考虑一个使用 `IndexOf(...)` 方法的示例：

```csharp
string book = "Introduction to C# book";
int index = book.IndexOf("C#");

Console.WriteLine(index);
// index = 16
```

## 使用 IndexOf(...) 搜索 – 示例

让我们再看一个关于在文中搜索单独字符或字符串的示例：

```
string str = "C# Programming Course";
int index = str.IndexOf("C"); // index = 0
index = str.IndexOf("Course"); // index = 15
index = str.IndexOf("COURSE"); // index = 15
index = str.IndexOf("ram"); // index = 7
index = str.IndexOf("r"); // index = 7
index = str.IndexOf("r", 10); // index = 18
```

看看我们如何在内存中搜索所有字符串的：

| 栈 (Stack) | 堆 (Heap) |

|---|---|

| | 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 |

| string@821a48 | C # | P r o g r a m i n g | C o u r s e |

如果我们看第三个字符串，会注意到在文中搜索单词 "COURSE" 返回的结果为 -1，即即没有找到匹配项。虽然该单词在文中，但它是以不同的字母大小写写的。`IndexOf(...)` 和 `LastIndexOf(...)` 方法区分大写字母和小写字母。如果我们想忽略这种差异，可以将文本写入一个新的变量中，并将其完全转换为小写或完全大写，然后对其中进行搜索，而不受字母大小写的影响。

## 查找子字符串的所有出现位置 – 示例

有时，我们想要找到另一个字符串中特定子字符串的所有出现位置。仅传递一个搜索项作为参数使用这两种方法对我们来说是不行的，因为始终只会返回子字符串的第一次出现。我们可以传递第二个参数作为索引，指示搜索开始的起始位置。当然，我们需要循环遍历它，以便从搜索字符串的第一次出现移动到下一个、再下一个、等等，直到最后一个。

这里有一个如何通过给定单词和起始索引使用 `IndexOf(...)` 的示例：在给定文本查找单词 "C#" 的所有出现位置：

```
string quote = "The main intent of the \Intro C#\" + 
" book is to introduce the C# programming to newbies";
```

# 使用 C# 的计算机编程基础

```
string keyword = "C#";
int index = quote.IndexOf(keyword);

while (index != -1)
{
  Console.WriteLine("{0} found at index: {1}", keyword, index);
  index = quote.IndexOf(keyword, index + 1);
}
```

第一步是搜索单词 "C#"。如果在文中找到该单词（即返回值不为 -1），则打印它，并从找到单词的位置开始继续向右搜索。重复此操作，直到 `IndexOf(...)` 返回 -1。注意：如果省略了初始索引，搜索将始终从开始开始并返回相同的值。这将导致程序挂起。如果我们直接从索引不加1进行搜索，将反复回到已经找到的结果。因此，结果的正确搜索应该从起始位置 +1 开始。

## 提取字符串的部分

现在我们知道如何检查子字符串是否出现在文中，以及出现的位置。但我们如何提取字符串的一个部分呢？

这个问题的解决方案是 `Substring(...)` 方法。通过使用它，我们可以根据文中给定的位置和长度提取字符串的一部分（子字符串）。如果省略了长度，将从初始位置提取到字符串的末尾。

这是一个从字符串提取子字符串的示例：

```
string path = "C:\Pics\CoolPic.jpg";
string fileName = path.Substring(8, 7);
// fileName = "CoolPic"
```

我们操作变量 `path`。它包含了系统的文件路径。为了将其赋值给新变量，我们使用 `Substring(8, 7)` 并从第 8 个位置开始提取 7 个字符。调用 `Substring(startIndex, length)` 方法提取从 `startIndex` 到 `startIndex + length - 1`（包含）之间的子字符串。例如，如果我们指定 `Substring(8, 3)`，将提取索引 8 到 10（包含）之间的字符。
