
# 70 StringBuilder：更高效地处理字符串

当你对字符串进行大量修改时，请使用辅助类 `StringBuilder` 以避免此类开销。请确保在文件顶部添加此行：

```
using System.Text; // 编译器在此查找 StringBuilder。
```

与 `StringBuilder` 的操作不同，你对 `StringBuilder` 进行的操作会直接更改底层字符串。这里有一个示例：

```
StringBuilder builder = new StringBuilder("012");
builder.Append("34");
builder.Append("56");
string result = builder.ToString(); // result = 0123456
```

如所示，创建一个用现有字符串初始化的 `StringBuilder` 实例。创建一个没有初始值的空 `StringBuilder`：

```
StringBuilder builder = new StringBuilder(); // 默认为 16 个字符
```

你也可以按照预期的容量创建 `StringBuilder`，这可以减少频繁增加器容量的开销：

```
StringBuilder builder = new StringBuilder(256); // 256 个字符。
```

使用 `Append()` 方法在当前内容的末尾添加文本。完成修改后，使用 `ToString()` 获取 `StringBuilder` 内部的字符串。这里是底层循环的 `StringBuilder` 版本，其中获取最终拼接字符串的部分已**加粗**：

```
StringBuilder sb = new StringBuilder(20000); // 分配大量内存
for (int i = 0; i < 1000; i++) {
    sb.Append(listOf[i]); // 与之前相同的名称列表
}
string result = sb.ToString(); // 获取结果。
```

`StringBuilder` 拥有许多其他字符串方法，包括 `Insert()`、`Remove()` 和 `Replace()`。不过，它缺少字符串的许多方法，如 `Substring()`、`CopyTo()` 和 `IndexOf()`。

假设你想将字符串的第一个字母转换为大写，就像前面的章节“将字符串转换为大写或小写”一样。使用 `StringBuilder` 会比我提供的代码整洁得多。

```csharp
StringBuilder sb = new StringBuilder("jones");
sb[0] = char.ToUpper(sb[0]);
string fixedString = sb.ToString();
```

这会将小写字符串 "jones" 放入 `StringBuilder`，直接访问 `StringBuilder` 字符串中的第一个字符，使用 `char.ToUpper()` 方法将该字符转换为大写。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_95_0.png)

并将大写后的字符重新赋值给 `sb[0]`。最后，它从 `StringBuilder` 中提取出改进后的字符串 "Jones"。

本章前面的 `BuildASentence` 示例可以从使用 `StringBuilder` 中获益。我经常使用 `StringBuilder`。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_96_0.png)

本书网站上的 `StringCaseChanging` 和 `VariousStringTechniques` 示例展示了 `StringBuilder` 的实际用法。

第二卷引入了名为扩展方法的 C# 特性。该示例为 `String` 类添加了几个实用的方法。在该微型书的后面，我们描述了如何在字符串、`char` 数组和 `byte` 数组之间转换。你可能需要频繁执行这些操作（在网站的 `StringCaseChanging` 示例中所示）。

# 第 4 章：熟练的运算符

本章内容

- 进行一些算术运算
- 执行一些逻辑算术
- 使用复合逻辑运算符使问题复杂

数学家创建变量并以各种方式对其进行操作，相加、相乘以及——这是一个难题——甚至对它们进行积分。本微型书的第 2 章描述了声明变量后如何使用它们来完成任务。然而，它对于如何使用变量来完成任务描述较少。本章介绍了你可以在变量上执行的操作以完成工作。操作需要运算符，如 `+`、`-`、`=`、`<` 和 `&`。本章包含了算术、逻辑和其他类型的运算符。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_98_0.png)

编写编写任务程序是好的。如果你的程序什么都不做，你永远无法成为一名 C# 程序员——除非你当然是一名顾问。

## 执行算术运算

算术运算符集分为几组：算术运算符、赋值运算符以及一组编程特有的特殊运算符。在消化这些之后，你还需要消化另一组逻辑运算符。祝胃口好！

## 简单运算符

你可能在小学就学会了如何使用大多数简单运算符。表 4-1 列出了它们。注意：计算机使用星号 (`*`) 而不是乘号 (`×`) 来进行乘法。

| 表 4-1 | 简单运算符 |
| --- | --- |
| 运算符 | 它的含义 |
| - (一元) | 取负 |
| * | 乘 |
| / | 除 |
| + | 加 |
| - (二元) | 减 |
| % | 取模（模） |

表中的大多数运算符都是二元运算符，因为它们作用于两个值：一个在运算符的左侧，一个在右侧。例外是一元负号。不过，它和其他运算符一样直观，如下例所示：

```csharp
int n1 = 5;
int n2 = -n1; // n2 现在值为 -5。
```

`-n` 的值是 `n` 的值的负数。

取模运算符你可能不像其他运算符那样熟悉。取模类似于除法后的余数。因此，`5 % 3` 是 `(5 / 3 = 1, 余数 2)`，`25 % 3` 是 `(25 / 3 = 8, 余数 1)`。读作“five modulo three”或“five mod third”。偶数模 2 结果为 0：`6 % 2 = 0 (6/2 = 3, 余数 0)`。

除取模以外的算术运算符适用于所有数值类型。取模运算符未定义用于浮点数，因为浮点值除法后没有余数。

## 运算顺序

某些表达式的值可能并不清晰。例如：

```csharp
int n = 5 * 3 + 2;
```

程序员是“先乘 5 次再加 2”（得到 17），还是……逻辑逻辑从左到右执行。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_99_0.png)

某些表达式的值可能并不清晰。例如：

```csharp
int n = 5 * 3 + 2;
```

程序员是“先乘 5 次再加 2”（得到 17），还是……逻辑从左到右执行。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_99_0.png)

*注：此处原文文本存在大量重复和 OCR 错误，已根据逻辑清理。*

## 运算顺序

某些表达式的值可能并不清晰。例如：

```csharp
int n = 5 * 3 + 2;
```

*注：此处提供的文本在 111aa4233d5cab0d6ddd1d82e8 处存在损坏。*

某些表达式的值可能并不清晰。例如：

```csharp
int n = 5 * 3 + 2;
```

*注：此处剩余文本存在严重乱码。*

## 递增运算符

在所有可能执行的加法操作中，给变量加 1 是最常见的：

```csharp
n = n + 1; // n 增加 1。
```

C# 使用一组二元运算符扩展了简单运算符。例如，`n += 1;` 等同于 `n = n + 1`。

赋值运算符存在于每个二元运算符：`+=`、`-=`、`*=`、`/=`、`&=`、`|=`。

甚至 C# 提供了更短的版本：

```csharp
n++; // n 增加 1。
```
