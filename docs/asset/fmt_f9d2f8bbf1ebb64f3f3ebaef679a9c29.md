
```csharp
string companyName = "Mike Murach and Associates";
int index1 = companyName.IndexOf(" ") // 4
int index2 = companyName.IndexOf("'") // 4
int index3 = companyName.IndexOf("Inc") // -1
int index4 = companyName.LastIndexOf(" ") // 15
```

### 使用 Remove, Insert 和 Replace 方法的代码

### 使用 Substring, ToUpper 和 ToLower 方法的代码

```csharp
string firstName = "anne";
string firstLetter = firstName.Substring(0, 1).ToUpper();
string otherLetters = firstName.Substring(1).ToLower();
firstName = firstLetter + otherLetters; // Anne
```

### 将一个字符串复制到另一个字符串的代码

```csharp
string s1 = "abc";
string s2 = s1; // 这将 s1 中存储的值复制到 s2
s2 = "def"; // 这不会改变 s1 中存储的值
```

图 9-6 用于处理字符串的代码示例

### 更多处理字符串的代码示例

9-7 介绍了一些额外的字符串处理例程。前四个用于解析字符串中的数据。第五个向字符串中添加字符。第六个将字符串中的某些字符替换为其他字符。如果你能理解这些例程中的代码，就应该能够在需要时编写自己的例程。

第一个例程展示了如何从包含全名的字符串中解析出名字。在这里，全名被赋值给 `fullName` 变量，这样你就可以根据该名称视觉化后续的语句。但在实际操作中，名称将由用户输入或从文件中读取，因此你不知道它是什么。

首先，该例程使用 `Trim` 方法移除用户可能不小心输入的字符串开头结尾的空格。接下来，使用 `IndexOf` 方法获取字符串中第一个空格的位置，该位置应该位于名和中间名或姓之间。然而，如果该方法没有在字符串中找到空格，它将返回 -1。在这种情况下，`if-else` 语句将整个字符串赋值给 `firstName` 变量。否则，它使用 `Substring` 方法将 `firstName` 变量设置为从字符串第一个字符开始且长度等于第一个空格位置的字符串。

为了移除字符串开头和结尾的空格，该例程还使用了 `Trim` 方法。然后，它使用 `StartsWith` 和 `EndsWith` 方法确定字符串中的第一个或最后一个字符是否为管道符（|）。如果是， `Remove` 方法将从字符串中移除该字符。

接下来的三条语句使用 `StartsWith` 和 `EndsWith` 方法（注：此处原文逻辑似乎有误，按原文翻译）...（此处根据原文逻辑翻译：接下来的三条语句使用 `StartsWith` 和 `EndsWith` 方法来确定字符串中的第一个或最后一个字符是否是管道符。如果是，`Remove` 方法将从字符串中移除该字符。）

*注：由于提供的原文文本部分存在逻辑重复或错位，以下翻译已严格遵循原文文本结构。*

接下来的三条语句使用 `StartsWith` 和 `EndsWith` 方法...第四个例程使用 `Split` 方法来简化字符串，所示。第三第三和第四个例程使用`Split` 方法可以简化你的代码，特别是当字符串包含多个元素时。第五和六个例程展示了如何向电话号码添加线字符以及将日期中的为字符替换为斜杠。为了添加连字符，你只需使用 `Insert` 方法在适当的位置插入字符。

### 从字符串中解析名字

```csharp
string fullName = "Edward C Kop";    // Edward C Kop
fullName = fullName.Trim();              // "Edward C Kop"
int firstSpace = fullName.IndexOf(" ");     // 6
string firstName = "";                   // 
if (firstSpace == -1)
    firstName = fullName;
else
    firstName = fullName.Substring(0, firstSpace); // Edward
```

# 检查字符串是否包含小数值的方法

public bool IsDecimal(TextBox textBox, string name)

```csharp
{
    string s = textBox.Text;
    int decimalCount = 0;
    bool validDecimal = true;
    foreach (char c in s)
    {
        if (!(
            c == '0' || c == '1' || c == '2' || // 数字字符
            c == '3' || c == '4' || c == '5' ||
            c == '6' || c == '7' || c == '8' ||
            c == '9' || c == '-' || c == '%' || c == ',' || // 格式字符
            c == '_'
        ))
        {
            validDecimal = false;
            break;
        }
        if (c == '.')
        {
            decimalCount++;
        }
    }
    if (validDecimal && decimalCount <= 1)
    {
        return true;
    }
    else
    {
        MessageBox.Show(name + " must be a decimal value.",
        "Entry Error");
        textBox.Focus();
        return false;
    }
}
```

# 从数字字符串中剔除格式字符的方法

public string Strip(string s)

```csharp
{
    foreach (char c in s)
    {
        if (c == '$' || c == '%' || c == ',' || c == ' ')
        {
            int i = s.IndexOf(c);
            s = s.Remove(i, 1);
        }
    }
    return s;
}
```

# 调用上述方法的代码

```csharp
decimal monthlyInvestment = 0;
if (IsDecimal(txtMonthlyInvestment, "Monthly Investment"))
{
    monthlyInvestment = Convert.ToDecimal(
    Strip(txtMonthlyInvestment.Text));
}
```

图 9-8 验证用户输入的两种方法

# 如何使用 StringBuilder 类

当你使用 `String` 类来创建字符串时，该字符串具有固定的长度和值。也就是说，`String` 类创建的字符串是不可变的。那么，当你给 `String` 变量分配一个新值时，旧的 `String` 对象会被删除，并被一个包含新值的新 `String` 对象所取代。

不过处理字符串的另一种方法是使用 `StringBuilder` 类。这样，你可以创建可变的 `StringBuilder` 对象，从而可以在对象中添加、删除或替换字符。这使得编写某些类型的字符串处理程序变得更加简单，而且这些程序的执行效率更高。因此，对于需要在字符串中追加、插入、删除或替换字符的字符串处理，你应该使用 `StringBuilder` 类，特别是当你处理占用大量系统资源的长字符串时。

在 9-9 中，你可以看到从 `StringBuilder` 类创建的字符串的一些常用属性和方法。如你所见，你可以使用索引来引用 `StringBuilder` 对象中的字符，并可以使用 `Length` 属性来获取字符串中的字符数量，就像对待 `String` 对象一样。你也可以对 `StringBuilder` 对象使用 `Insert`、`Remove` 和 `Replace` 方法。然而，这些方法不是返回新字符串，而是修改现有的字符串。

当你使用 `StringBuilder` 类时，需要包含一个包含它的 `System` 命名空间的引用语句。你可以在类的开头编写此语句，连同默认添加到类中的 `using` 语句一起。这样，你就可以在不带命名空间名称的情况下引用 `StringBuilder` 类了。

当你创建一个 `StringBuilder` 对象时，可以编写一个或两个参数来分配初始值、初始容量或两者兼有。第二个示例中的语句说明了这种工作原理。在这里，第一个语句不包含任何参数，因此创建的 `StringBuilder` 对象具有 16 个字符的默认容量和空字符串初始值。第二个语句创建了一个初始容量为 10 的 `StringBuilder` 对象。第三和第四条语句类似，但它们为对象指定了初始值。

图中的最后一个示例显示了如何使用 `StringBuilder` 类的五种方法。在这里，第一个语句创建了一个初始容量为 10 的 `StringBuilder` 对象，第二个语句向对象追加了一个 10 字符的数字。第三和第四条语句在字符串中插入句点以格式化数字。第五条语句删除了区号和随后的点。第六条语句将剩余的句点替换为连字符。最后一条语句将存储在 `StringBuilder` 对象中的字符转换为字符串。

此示例还显示了 `StringBuilder` 对象在需要时如何自动增加容量。在这里，`StringBuilder` 对象在创建时容量为 10，该容量在插入第一个点之前一直保持为 11。然后，为了能够存储这 11 个字符，`StringBuilder` 对象自动将其容量翻倍到 20。

# 第 9 章 如何处理日期和字符串

# 创建 StringBuilder 对象的语法

`StringBuilderNameName = new StringBuilder([value], [capacity]);`

# StringBuilder 类的常用属性和方法

| 索引器 | 描述 |

| --- | --- |

| `[index]` | 获取指定位置的字符。 |

| 属性 | 描述 |

| `Length` | 获取字符串中字符的数量。 |

| `Capacity` | 获取或设置字符串可以容地的字符数。 |

| 方法 | 描述 |

| `Append(string)` | 将指定的字符串添加到字符串的末尾。 |

| `Insert(index, string)` | 在字符串的指定索引处插入指定的字符串。 |

| `Remove(startIndex, count)` | 从字符串中删除指定的字符。 |

| `Replace(oldString, newString)` | 将旧字符串的所有出现处替换为新字符串。 |

| `ToString()` | 将 `StringBuilder` 对象转换为字符串。 |

# 包含以下内容的语句

[content]using System.Text;[/content]

创建并初始化的语句

```csharp
StringBuilder phoneNumber1 = new StringBuilder();
StringBuilder phoneNumber2 = new StringBuilder(10);
StringBuilder phoneNumber3 = new StringBuilder("555");
phoneNumber4 = new StringBuilder("555", 10);
```

# 创建并插入的代码

```csharp
StringBuilder phoneNumber = new StringBuilder(10);
phoneNumber.Append("1234567890");
phoneNumber.Insert(3, ".");
phoneNumber.Insert(7, ".");
phoneNumber.Remove(0, 3);
phoneNumber.Replace(".", "-");
string result = phoneNumber.ToString();
```

# 

- 与字符串对象不同，`StringBuilder` 对象是可变的，这意味着它们可以被更改。
- `StringBuilder` 的容量是分配的内存量。
- 要引用 `StringBuilder` 类，必须包含 `System.Text` 命名空间。
- `StringBuilder` 的默认容量为 16 个字符。

图 9-9 如何使用 `StringBuilder` 类

# 如何格式化数字、日期和时间

在第 4 章中，你学习了如何对数字应用标准格式。在本在本章前面的部分，你学习了如何对日期和时间应用标准格式。然而，你也可以对数字、日期和时间应用自定义格式。

## 第 9 章 如何处理日期和字符串

## String 类的 Format 方法的语法

```
Format(string, value1[, value2]...)
```

## 字符串参数中格式规范的语法

`{N, M} [:formatString]}`

说明

| N | 描述 |

|---|---|

| N | 表示要进行格式化的值的整数。 |

| M | 表示格式化值宽度的整数。如果 M 为负数，则该值将左对齐。如果 M 为正数，则将右对齐。 |

| formatString | 格式代码的字符串。 |

## 格式字符串的语法

`positiveformat[;negativeformat;zeroform]]`

## 标准数值格式代码

| 代码 | 描述 |

|---|---|

| C 或 c | 以指定的小位数将数字格式化为货币格式。 |

| D ord | 以指定的位数将整数格式化。 |

| E 或 e | 以指定的小位数将数字以科学计数法（指数形式）格式化。 |

| F 或 f | 以指定的小位数将数字格式化为小数。 |

| G org | 根据哪种方式更紧凑，将数字格式化为小数或科学计数法。 |

| N orn | 使用千位分隔符和指定的小位数将数字格式化。 |

| P 或 p | 以指定的小位数将数字格式化为百分比。 |

## 自定义数值格式代码

| 符号 | 描述 | 描述 |

|---|---|---|

| 0 | 零占位符 | 千位分隔符 |

| # | 数字占位符 | 百分比占位符 |

| | 小数点 | 分隔符 |

## 格式化单个数字的语句

```
string balance = String.Format("{0:c}", 1234.56); // $1,234.56
string balance2 = String.Format("{0:##,0.00} ($0:#,0.00)", -1234.56); // ($1,234.56)
string balance3 = String.Format("{0:##,0.00} ($0:#,0.00);Zero", 0); // Zero
string quantity = String.Format("{0:d3}", 43); // 043
string payment = String.Format("{0:f2}", 432.8175); // 432.82
```

## 格式化两个数字的语句

```
string totalDue = String.Format("Invoice total: {0:c}; Amount due: {1:c}", 354.75, 20); // Invoice total: $354.75; Amount due: $20.00.
```

![](img/3148667e42d4db35b3d08576aaa1fa01_292_0.png)

## C# 语言基础

负数的格式也是类似的。然而，这种格式包含了括号，这意味着负数在显示时会带有括号，如结果所示。请注意，括号实际上并不是格式代码。它们仅仅是包含在输出字符串中的字面量值。美元符号也是如此。

第三条语句与第二个语句相似，但它包含一个针对零值的额外格式。在这种情况下，零值将显示为字面量 "Zero"，正如你在该语句的结果中所看到的那样。

最后两条语句展示了如何使用整数和小数的标准格式代码。在第一条语句中，整数被格式化为三位数，因为在格式代码后面包含了数字 3。在第二条语句中，小数被格式化为两位小数。如你所见，如果数字包含的小数位比指定的多，则数字会被四舍五入。

图底部的示例显示了如何使用 `Format` 方法来格式化两个数字。在这里，字符串参数除了包含每个待格式化值的格式规范外，还包含了文本。在这种情况下，第一个值根据第一个格式规范进行格式化，第二个值根据第二个格式规范格式化。

## 如何格式化日期和时间

你也可以使用 `String` 类的 `Format` 方法来格式化日期和时间。该方法的工作原理与数值格式相同，但你对图 9-11 所示的 `DateTime` 值使用标准和自定义格式代码。图中的示例展示了它是如何运作的。如果你理解如何使用此方法格式化数字，那么在使用它格式化日期和时间时应该不会遇到问题。

## 标准 DateTime 格式代码

| 代码 | 代码 | 描述 |

|---|---|---|

| d | f | 长日期，短时间 |

| D | F | 长日期，长时间 |

| t | g | 短日期，短时间 |

| T | G | 短日期，长时间 |

## 自定义 DateTime 格式代码

| 代码 | 代码 | 描述 |

|---|---|---|

| d | h | 不带前导零的 |
