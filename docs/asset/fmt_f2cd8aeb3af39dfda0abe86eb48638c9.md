
表示井棋并不需要每个位置都是整数。另一种方法是为每个玩家构建一个虚拟棋盘，每个棋盘包含一个 `bool` 来指示哪些位置被选中。列表 3.18 对应于一个三维数组。

### 列表 3.18：初始化一个三维数组

```csharp
bool[,,] cells;

cells = new bool[2,3,3]{

// 玩家 1 移动               // X | |
// +------+-----
    {true, false, false},      // X | |
    {true, false, false},
    {true, false, true},
                            // X | | X
// 玩家 2 移动               // 0 |
// +------+-----
    {false, false, true},      // 0 |
    {true, false, false},
    {false, true, false}
// +------+-----
                            // |0 |
};
```

在此示例中，棋盘已初始化，并且明确标识了每个维度的大小。除了在 `new` 表达式中标识大小外，还提供了数组的字面量值。`bool[,,]` 类型的字面量值被分为两个 `bool[]` 数组，大小为 3 x 3。每个二维数组由三个大小为 3 的 `bool` 数组组成。

正如前面提到的，多维数组中的每个维度必须保持尺寸一致。然而，也可以定义交错数组（jagged array），即数组的数组。交错数组的语法与多维数组略有不同；此外，交错数组不需要尺寸一致。因此，可以如列表 3.19 所示初始化交错数组。

### 列表 3.19：初始化交错数组

```csharp
int[][] cells = {
new int[]{1, 0, 2, 0},
new int[]{1, 2, 0},
new int[]{1, 2},
new int[]{1}
};
```

交错数组不使用逗号来识别新维度。相反，它定义了一个数组的数组。在列表 3.19 中，`[]` 放在数据类型 `int[]` 之后，从而声明了一个类型为 `int[]` 的数组。

注意，交错数组的每个内部数组都需要一个数组实例（或 `null`）。在前一个示例中，你使用 `new` 来实例化交错数组的内部元素。省略实例化会导致编译错误。

## 使用数组

你使用方括号符号（称为数组访问器）访问数组中的特定项。要从数组中获取第一个项，将索引指定为零。在列表 3.20 中，`languages` 变量中的第五项（使用索引 4，因为第一个项的索引为 0）的值存储在变量 `language` 中。

### 列表 3.20：声明并访问数组

```csharp
string[] languages = new string[9]{
"C#", "COBOL", "Java",
"C++","TypeScript","Visual Basic",
"Python", "Lisp", "JavaScript"};

// 获取 languages 数组中的第五项 (TypeScript)
string language = languages[4];
```

```csharp
// 输出 "TypeScript"
Console.WriteLine(language);

// 获取从末尾开始的第三项 (Python)
language = languages[^3];

// 输出 "Python"
Console.WriteLine(language);
```

从 C# 8.0 开始，你还可以使用从索引运算符（也称为 `^` 索引符号运算符）相对于数组末尾访问项。例如，索引 `^1` 可获取数组的最后一项，而使用从索引运算符的第一个元素则是 `^9`（其中 9 是数组中的项数）。在列表 3.20 中，`^3` 将 `languages` 变量中从末尾开始的第三项（"Python"）的值赋值给 `language`。

由于 `^1` 是最后一个元素，`^0` 是无效的（它指向数组长度），而 `^2` 是倒数第二个。从索引运算符是一种无需手动计算长度即可从数组背面访问元素的方便方法。

## 数组

```csharp
new int[]{1, 2, 1}
};
```

```csharp
cells[1][0] = 1;
// ...
```

### Length

你可以获取数组的长度，如列表 3.24 所示。

### 列表 3.24：检索数组的长度

```csharp
Console.WriteLine(
  "There are {languages.Length} languages in the array.");
```

数组具有固定长度；它们的绑定方式使得在不重新创建数组的情况下无法更改长度。此外，越数组的边界（或长度）会导致运行时报告错误。当你尝试使用数组中不存在元素的索引来访问（检索或分配）数组时，就会发生这种错误。当你使用数组长度作为索引访问数组时，这种错误经常发生，如列表 3.25 所示。

### 列表 3.25：访问数组边界外抛出异常

```csharp
string[] languages = new string[9];
// 运行时错误：索引越界 - 最后一个元素
// 应该是 8
languages[4] = languages[9];
```

> 注意
`Length` 成员返回数组中项的数量，而不是最高索引。变量 `languages` 的 `Length` 成员为 9，但 `languages` 变量在运行时允许的最高索引为 8，因为这是它从开始位置计算的距离。

### 语言对比：C++—缓冲区溢出漏洞

非托管 C++ 并不总是检查你是否越过了数组边界。这不仅难以调试，而且这种错误还可能导致所谓的缓冲区溢出的潜在安全错误。相比之下，通用语言运行时（CLR）保护所有 C#（以及托管 C++）代码越越数组边界，从上消除了托管代码发生缓冲区溢出的可能性。

在 C# 8.0 中，访问 `^0` 项也会发生相同的问题：由于 `^1` 是最后一个项，因此 `^0` 是数组末之后的项——而这并不。

为了避免在访问最后一个元素时越数组边界，请使用长度检查来验证数组长度是否大于 0，并在访问数组最后一项时使用 `^1`（从 C# 8.0 开始）或 `Length - 1` 代替硬编码。使用 `Length` 作为索引时，必须减去 1 以避免越界错误（参见列表 3.26）。

### 列表 3.26：在数组索引中使用 Length - 1

```csharp
string[] languages = new string[9];
...
languages[4] = languages[languages.Length - 1];
```

（当然，如果可能根本没有数组实例，在访问数组之前首先检查是否为空。）

> 指南
- 考虑在访问数组之前检查是否为空，而不是假设存在数组实例。
- 考虑在对数组进行索引操作之前检查数组长度，而不是假设长度。
- 在 C# 8.0 或更高版本中，考虑使用从索引索引运算符 (`^`) 而不是 `Length - 1`。

`Length` 返回数组中元素的总数。因此，如果你有一个大小为 2 x 3 x 3 的多维数组 `cells[,,]`，`Length` 将返回元素的总数 18。

对于交错数组（jagged array），`Length` 返回第一个数组中的元素数量。因为交错数组是数组的数组，`Length` 仅评估外部包含数组并返回其元素计数，无论内部数组内部是什么。

### 数组 111

## 范围

C# 8.0 添加的另一个与索引相关的特性是支持数组切片——即将数组的一个切片提取到新数组中。指定范围的语法是 `..` 范围运算符，它可以可选地放置索引之间（包括从末尾开始的索引）。列表 3.27 提供了示例。

### 3.27：范围运算符的示例

```csharp
string[] languages = new string[]{
    "C#", "COBOL", "Java",
    "C++", "TypeScript", "Visual Basic",
    "Python", "Lisp", "JavaScript";
};

System.Console.WriteLine("0..3", {
    string.Join(", ", languages[0..3]) // C#, COBOL, Java
});

System.Console.WriteLine("3..0", {
    string.Join(", ", languages[3..0]) // Python, Lisp, JavaScript
});

System.Console.WriteLine("3..3", {
    string.Join(", ", languages[3..3]) // C++, TypeScript, Visual Basic
});

System.Console.WriteLine("..6", {
    string.Join(", ", languages[..6]) // C#, COBOL, Java
});

System.Console.WriteLine("6..", {
    string.Join(", ", languages[6..]) // Python, Lisp, JavaScript
});

System.Console.WriteLine("..", {
    // C#, COBOL, Java, C++, TypeScript, Visual Basic, Python, Lisp, JavaScript
    string.Join(", ", languages[..]);
});
```

关于范围运算符需要注意的重要点是，它通过指定从第一个（包含）到结束（不包含）来识别项。因此，在列表 3.27 的 `0..3` 示例中，它切片的内容包含了从第一个项到但不包括第四个项的内容。

# 第3章：数据类型进阶

返回的值为负数。（使用取反运算符 `~index` 会返回第一个大于搜索值的索引，如果存在的话。）

- `Clear()` 方法不会删除数组中的元素，也不会将长度设置为零。数组的大小是固定的，无法修改。因此，`Clear()` 方法将数组的每个元素都设置为其默认值（`null`、`0` 或 `false`）。这解释了为什么在调用 `Clear()` 后写入数组时 `Console.WriteLine()` 会创建一个空行。

![](img/b18af4770e9195628243fa73ff1469b4_152_0.png)

## 数组实例成员

与字符串一样，数组拥有实例成员，无法通过变量直接从数据类型访问。`Length` 就是实例成员的一个示例，因为对 `Length` 的访问是通过数组变量进行的，而不是类。其他重要的实例成员是 `GetLength()`、`Rank` 和 `Clone()`。

获取特定维度的长度不需要属性。为了获取特定秩数的大小，数组包含了 `GetLength()` 实例方法。调用此方法时，必须指定要返回长度的秩（参见列表 3.29）。

### 列表 3.29：获取特定维度的尺寸

```csharp
bool[][][] cells;
cells = new bool[2,3,3];
System.Console.WriteLine(cells.GetLength()); // 显示 2
System.Console.WriteLine(cells.Rank); // 显示 3
```

列表 3.29 的结果出现在输出 3.3 中。

### 输出 3.3

2

列表 3.29 显示 2，因为这是第一维中的元素数量。

也可以通过访问数组的 `Rank` 来获取整个数组的秩，例如，`cells.Rank` 将返回 3（参见列表 3.29）。

默认情况下，将一个数组变量赋值给另一个变量只会复制数组的引用，而不是数组的单个元素。要创建数组的完整副本，请使用数组的 `Clone()` 方法。`Clone()` 方法将返回数组的副本；更改此新数组的任何成员都不会影响原始数组的成员。

## 作为数组的字符串

`string` 类型的变量可以像字符数组一样访问。例如，要获取名为 `palindrome` 的字符串的第四个字符，可以调用 `palindrome[3]`。但注意，由于字符串是不可变的，无法为字符串中的特定字符赋值。因此，C# 不允许在 `palindrome` 声明为字符串的情况下情况下执行 `palindrome[3]='a'`。列表 3.30 使用数组访问器来判断命令行上的选项是否为有效选项，其中选项以连字符作为第一个字符来标识。

### 列表 3.30：查找命令行选项

```csharp
string[] args;
...
if(args[0] == '-')
{
    // 此参数是一个选项
}
```

此代码段使用了 `if` 语句，该语句将在第 4 章中介绍。此外，它还展示了一个有趣的示例，因为你使用数组访问器来获取字符串数组 `args` 中的第一个元素。紧跟第一个数组访问器之后的是第二个访问器，它获取字符串的第一个字符。因此，该代码等同于列表 3.31 所示的代码。

### 列表 3.31：查找命令行选项（简化版）

```csharp
string[] args;
...
string arg = args[0];
```

# 第3章：数据类型进阶

```csharp
if(arg[0] == '-')
{
    // 此参数是一个选项
}
```

不仅可以使用数组访问器单独获取字符串字符，还可以使用字符串的 `ToCharArray()` 方法将整个字符串作为字符数组进行获取。使用这种方法，你可以通过列表 3.32 所示的 `Reverse` 方法反转字符串。

### 列表 3.32：反转字符串

```csharp
class Palindrome
{
    static void Main()
    {
        string reverse, palindrome;
        char[] temp;
        System.Console.Write("Enter a palindrome: ");
        palindrome = System.Console.ReadLine();
        // 移除空格并转换为小写
        reverse = palindrome.Replace(" ", "");
        reverse = reverse.ToLower();
        // 转换为数组
        temp = reverse.ToCharArray();
        // 反转数组
        Array.Reverse(temp);
        // 检查反转后的字符串是否相同
        if(reverse == new string(temp))
        {
            System.Console.WriteLine($"{palindrome} is a palindrome.");
        }
        else
        {
            System.Console.WriteLine($"{palindrome} is NOT a palindrome.");
        }
    }
}
```
