

## 长度

你可以获取数组的长度，如清单 3.22 所示。

**清单 3.22：获取数组长度**

```
Console.WriteLine(
    $"There are { languages.Length } languages in the array.");
```

数组具有固定长度；它们被约束为在重新创建数组之前无法更改长度。此外，超出数组的**边界**（或长度）将导致运行时报告错误。当你试图使用一个在数组中不存在元素的索引来访问（检索或赋值）数组时，可能会发生这种情况。这种错误经常发生在你将数组长度用作数组索引时，如清单 3.23 所示。

**清单 3.23：访问数组边界之外，抛出异常**

```
string languages = new string[9];
...
// RUNTIME ERROR: index out of bounds – should
// be 8 for the last element
languages[4] = languages[9];
```

![](img/ef6a8a417630b222bfb3f3b949facff0_135_0.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_135_1.png)

使用 `Length` 代替硬编码的数组大小是一种良好的实践。例如，若要将 `Length` 用作索引，有必要减去 1 以避免越界错误（参见清单 3.24）。

**清单 3.24：在数组索引中使用 Length - 1**

```csharp
string languages = new string[9];
...
languages[4] = languages[languages.Length - 1];
```

为了避免超出数组边界，请使用长度检查来验证数组长度是否大于 0，并在访问数组中的最后一个元素时，使用 `Length - 1` 代替硬编码值（参见清单 3.24）。

`Length` 返回数组中的总元素数。因此，如果你有一个多维数组，例如尺寸为 2 × 3 × 3 的 `bool cells[ , ]`，`Length` 将返回总元素数 18。

对于锯齿数组（jagged array），`Length` 返回第一个数组中的元素数量。由于锯齿数组是数组的数组，`Length` 仅评估外部包含数组并返回其元素计数，无论内部数组中包含什么。

### 更多数组方法

数组包含用于操作数组内元素的附加方法——例如，`Sort()`、`BinarySearch()`、`Reverse()` 和 `Clear()`（参见清单 3.25）。

**清单 3.25：额外的数组方法**

```csharp
class ProgrammingLanguages
{
    static void Main()
    {
        string[] languages = new string[]{
            "C#", "COBOL", "Java",
            "C++", "Visual Basic", "Pascal",
            "Fortran", "Lisp", "J#"};

        System.Array.Sort(languages);

        string searchString = "COBOL";
        int index = System.Array.BinarySearch(
            languages, searchString);
        System.Console.WriteLine(
            "The wave of the future, "
            + $"{ searchString }, is at index { index }");

        System.Console.WriteLine();
        System.Console.WriteLine(
            $"{ \"First Element\",-20 }{t{ \"Last Element\",-20 }");
        System.Console.WriteLine(
            $"{ \"-----------\",-20 }{t{ \"-----------\",-20 }");
        System.Console.WriteLine(
            $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 "});
        System.Array.Reverse(languages);
        System.Console.WriteLine(
            $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
        // Note this does not remove all items from the array.
        // Rather, it sets each item to the type's default value.
        System.Array.Clear(languages, 0, languages.Length);
        System.Console.WriteLine(
            $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
        System.Console.WriteLine(
            $"After clearing, the array size is: { languages.Length }");
    }
}
```

清单 3.25 的结果如图 3.2 所示。

**输出 3.2**

```
The wave of the future, COBOL, is at index 2.
First Element       Last Element
----------          ----------
C#                  Visual Basic
Visual Basic         C#
After clearing, the array size is: 9
```

通过 `System.Array` 类访问这些方法。在大多数情况下，使用这些方法是不言自明的，除了两个值得注意的项目：

- 在使用 `BinarySearch( )` 方法之前，对数组进行排序很重要。如果值未按递增顺序排序，可能会返回错误的索引。如果搜索元素不存在，返回的值为负数。（使用取反运算符，`~index`，将返回任何大于搜索值的第一个索引。）
- `Clear()` 方法不会移除数组元素，也不会将长度设置为零。数组大小是固定的，无法修改。因此，`Clear()` 方法将数组中的每个元素设置为默认值（`false`、`0` 或 `null`）。这解释了为什么在调用 `Clear()` 后写出数组时，`Console.WriteLine()` 会创建一个空白行。

### 语言对比：Visual Basic——重新调整数组维度

Visual Basic 包含一个用于更改数组中项目数量的 `ReDim` 语句。虽然 C# 没有等价的特定关键字，但在 .NET 2.0 中有一个可用的方法，它会重新创建数组，然后将所有元素复制到新数组中。该方法名为 `System.Array.Resize`。

### 数组实例方法

与字符串类似，数组拥有实例成员，这些成员不是从数据类型而是直接从变量访问的。`Length` 是实例成员的一个例子，因为对 `Length` 的访问是通过数组变量进行的，而不是通过类。其他重要的实例成员包括 `GetLength()`、`Rank` 和 `Clone()`。

获取特定维度的长度不需要 `Length` 属性。若要获取特定秩的大小，数组包含一个 `GetLength()` 实例方法。调用此方法时，需要指定要返回其长度的秩（参见清单 3.26）。

**清单 3.26：获取特定维度的大小**

```csharp
bool[,] cells;
cells = new bool[2,3,3];
System.Console.WriteLine(cells.GetLength(0));   // Displays 2
```

清单 3.26 的结果如图 3.3 所示。

**输出 3.3**

2

清单 3.26 显示 2，因为这是第一个维度中的元素数量。

还可以通过访问数组的 `Rank` 成员来获取整个数组的秩。例如，`cells.Rank` 将返回 3。

默认情况下，将一个数组变量赋值给另一个数组变量仅复制数组引用，而不复制数组的各个元素。为了创建数组的全新副本，请使用数组的 `Clone()` 方法。`Clone()` 方法将返回数组的一个副本；更改此新数组的任何成员都不会影响原始数组的成员。

### 作为数组的字符串

类型为 `string` 的变量可以像字符数组一样访问。例如，要检索名为 `palindrome` 的字符串的第四个字符，你可以调用 `palindrome[3]`。然而请注意，由于字符串是不可变的，因此无法对字符串内的特定字符进行赋值。因此，C# 不允许执行 `palindrome[3]='a'`，其中 `palindrome` 被声明为字符串。清单 3.27 使用数组访问器来确定命令行参数是否是一个选项，其中选项由第一个字符处的破折号标识。

**清单 3.27：查找命令行选项**

```csharp
string[] args;
...
if(args[0][0] == '-')
{
    // This parameter is an option
}
```

该代码片段使用了 `if` 语句，这在第 4 章中有所介绍。此外，它是一个有趣的示例，因为你使用数组访问器来检索字符串数组 `args` 中的第一个元素。第一个数组访问器之后是第二个访问器，它检索字符串的第一个字符。因此，该代码等价于清单 3.28 中所示的代码。

**清单 3.28：查找命令行选项（简化版）**

```csharp
string[] args;
...
string arg = args[0];
if(arg[0] == '-')
{
    // This parameter is an option
}
```

