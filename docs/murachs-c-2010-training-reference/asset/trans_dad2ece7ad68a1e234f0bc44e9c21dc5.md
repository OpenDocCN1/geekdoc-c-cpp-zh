

# 如何声明和初始化字符串

```
string message1 = "Invalid data entry";
string message2 = "";
string message3 = null;
```

# 如何合并字符串

```
string firstName = "Bob";
string lastName = "Smith";
string name = firstName + " " + lastName; // firstName is "Bob"
// lastName is "Smith"
// name is "Bob Smith"
```

# 如何合并字符串和数字

```c
double price = 14.95;
string priceString = "Price: $" + price; // priceString is "Price: $14.95"
```

# 如何将一个字符串附加到另一个字符串

```c
string firstName = "Bob";
string lastName = "Smith";
string name = firstName + " " + lastName; // firstName is "Bob"
// lastName is "Smith"
// name is "Bob Smith"
```

# 使用 += 运算符将一个字符串附加到另一个字符串

```c
string firstName = "Bob";
string lastName = "Smith";
string name = firstName + " " + lastName; // firstName is "Bob"
// lastName is "Smith"
// name is "Bob Smith"
```

# 说明

- 字符串可以由字符集中的任何字符，包括字母、数字以及 $、*、& 和 # 等特殊字符。

- 要指定字符串的值，可以将其括在双引号中。这被称为字符串字面量。

- 要给字符串分配 `null` 值，可以使用 `null` 关键字。这意味着字符串的值是未知的。

- 要给字符串分配空字符串，可以使用一对双引号。这通常表示字符串的值是已知的，但字符串不包含任何字符。

- 要将字符串连接（或拼接）到另一个字符串或值数据类型，请使用加号 `+`。如果你将一个值数据类型连接到字符串，C# 将自动将该值转换为字符串，以便它可以作为字符串的一部分。

- 当你将一个字符串附加到另一个字符串时，是将一个字符串添加到另一个字符串的末尾。为此，可以使用赋值语句。

- `+=` 运算符是将字符串表达式附加到字符串变量的快捷方式。

![](img/3148667e42d4db35b3d08576aaa1fa01_132_0.png)

# 如何在字符串中包含特殊字符

4-9 显示了你可以使用的两种技术，可以在字符串中包含特定类型的特殊字符。特别是，这张图显示了如何包含反斜杠、引号以及换行、制表符和返回等控制字符。

你可以用于在字符串中包含这些字符的技巧是使用图中所示的转义序列。虽然这些转义序列是你最常用的，但 C# 还为十六进制和 Unicode 字符提供了其他转义序列。

如果你正在将字符串字面量赋值给字符串，你可能倾向于使用字面字面量（verbatim string literal）而不是转义序列。要使用字面字面量，在字符串的起始引号前编写一个 @ 符号。然后你可以在起始和结束引号之间输入反斜杠、制表符和换行符。例如，你可以使用 Enter 输入一个或多个换行符。这时，字面字面量将跨越两或多行。

虽然字面字面量对于包含反斜杠和单引号的字面量效果良好，但需要在字面量中包含双引号时，就会出现复杂的情况。这是因为双引号用于表示字面量的开始和结束。要在字面字面量中包含双引号，你必须输入两个双引号。

此时，你可能想知道何时在使用转义序列在字符串中包含特殊字符，以及何时使用字面字面量。答案是每种技术都适用于某些代码位置。例如，字面字面量对于代码文件路径效果良好。另一方面，使用转义序列在字符串中包含换行符和制表符更容易。因此，你将熟悉这两种技术。然后，你就可以判断在情况下哪种技术最有效。

# 常见转义序列

| 键 | 说明 |
| --- | --- |
| \n | 换行 |
| \t | 制表符 |
| \r | 返回 |
| \\ | 反斜杠 |
| \" | 双引号 |

# 示例

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

# 说明

- 字符串可以由字符集中的任何字符，包括字母、数字以及 $、*、& 和 # 等特殊字符。

- 要指定字符串的值，可以将其括在双引号中。这被称为字符串字面量。

- 要给字符串分配 `null` 值，可以使用 `null` 关键字。这意味着字符串的值是未知的。

- 要给字符串分配空字符串，可以使用一对双引号。这通常表示字符串的值是已知的，但字符串不包含任何字符。

- 要将字符串连接（或拼接）到另一个字符串或值数据类型，请使用加号 `+`。如果你将一个值数据类型连接到字符串，C# 将自动将该值转换为字符串，以便它可以作为字符串的一部分。

- 当你将一个字符串附加到另一个字符串时，是将一个字符串添加到另一个字符串的末尾。为此，可以使用赋值语句。

- `+=` 运算符是将字符串表达式附加到字符串变量的快捷方式。

![](img/3148667e42d4db35b3d08576aaa1fa01_132_0.png)

# 如何在字符串中包含特殊字符

4-9 显示了你可以使用的两种技术，可以在字符串中包含特定类型的特殊字符。特别是，这张图显示了如何包含反斜杠、引号以及换行、制表符和返回等控制字符。

你可以用于在字符串中包含这些字符的技巧是使用图中所示的转义序列。虽然这些转义序列是你最常用的，但 C# 还为十六进制和 Unicode 字符提供了其他转义序列。

如果你正在将字符串字面量赋值给字符串，你可能倾向于使用字面字面量（verbatim string literal）而不是转义序列。要使用字面字面量，在字符串的起始引号前编写一个 @ 符号。然后你可以在起始和结束引号之间输入反斜杠、制表符和换行符。例如，你可以使用 Enter 输入一个或多个换行符。这时，字面字面量将跨越两或多行。

虽然字面字面量对于包含反斜杠和单引号的字面量效果良好，但需要在字面量中包含双引号时，就会出现复杂的情况。这是因为双引号用于表示字面量的开始和结束。要在字面字面量中包含双引号，你必须输入两个双引号。

此时，你可能想知道何时在使用转义序列在字符串中包含特殊字符，以及何时使用字面字面量。答案是每种技术都适用于某些代码位置。例如，字面字面量对于代码文件路径效果良好。另一方面，使用转义序列在字符串中包含换行符和制表符更容易。因此，你将熟悉这两种技术。然后，你就可以判断在情况下哪种技术最有效。

# 常见转义序列

| 键 | 说明 |
| --- | --- |
| \n | 换行 |
| \t | 制表符 |
| \r | 返回 |
| \\ | 反斜杠 |
| \" | 双引号 |

# 示例

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

（注：重复的示例表格已根据翻译要求省略，仅保留逻辑结构）

（重复的示例表格已省略）

（重复的示例表格已省略）

（重复的示例表格已省略）

（重复的示例表格已省略）

（重复的示例表格已省略）

（重复的示例表格已省略）

| 键 | 说明 |
| --- | --- |
| string firstName = "Bob"; | |
| string lastName = "Smith"; | |
| string name = firstName + " " + lastName; | firstName is "Bob" |
| // lastName is "Smith" | |
| // name is "Bob Smith" | |

