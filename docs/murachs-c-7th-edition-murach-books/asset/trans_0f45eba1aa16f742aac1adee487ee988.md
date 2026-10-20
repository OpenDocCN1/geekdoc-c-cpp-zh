

## 如何在字符串中包含特殊字符

图 4-11 显示了两种可在字符串中包含特定类型特殊字符的技术。特别是，该图展示了如何包含反斜杠、引号以及换行符、制表符和回车符等控制字符。

一种可在字符串中包含这些字符的技术是使用本图所示的 *转义序列*。尽管这些转义序列是你最常使用的，但 C# 还提供了用于十六进制和 Unicode 字符的其他转义序列。

如果你要将字符串字面量分配给字符串，你可能更喜欢使用 *逐字字符串字面量* 而不是转义序列。要使用逐字字符串字面量，你在字符串的起始引号前加上 @ 符号。然后，你可以在起始和结束引号之间输入反斜杠、制表符和换行符。例如，你可以使用 Enter 键输入一个或多个换行符。然后，逐字字符串字面量将跨越两行或更多行。

尽管逐字字符串字面量对于包含反斜杠和单引号的字面量效果很好，但在需要在字面量中包含双引号时会出现复杂情况。这是因为双引号用于指示字面量的开始和结束。因此，要在逐字字符串字面量中包含双引号，你必须输入两个双引号。

到目前为止，你可能在思考何时应使用转义序列在字符串中包含特殊字符，何时应使用逐字字符串字面量。答案是每种技术都适用于某些类型的编码情况。例如，逐字字符串字面量非常适合编码文件位置。另一方面，使用转义序列在字符串中包含换行符和制表符通常更容易。因此，你需要熟悉这两种技术。然后，你可以决定哪种技术最适合特定情况。

## 常见转义序列

| Key | Description |
| --- | --- |
| \n | New line |
| \t | Tab |
| \r | Return |
| \\ | Backslash |
| \" | Quotation |

## 使用转义序列的示例

| Code | Result |
| --- | --- |
| string code = "JSPS"; decimal price = 49.50m; string result = "Code: " + code + "\n" + "Price: $" + price + "\n"; | Code: JSPS Price: $49.50 |
| string names = "Joe\tSmith\rKate\tLewis\r"; | Joe    Smith Kate   Lewis |
| string path = "c:\\c#.net\\files"; | c:\c#.net\files |
| string message = "Type \"x\" to exit"; | Type "x" to exit |

## 使用逐字字符串字面量的示例

| Code | Result |
| --- | --- |
| string names = @"Joe    Smith Kate   Lewis"; | Joe    Smith Kate   Lewis |
| string path = @"c:\c#.net\files"; | c:\c#.net\files |
| string message = @"Type ""x"" to exit"; | Type "x" to exit |

## 描述

- 在字符串中，你可以使用转义序列包含某些类型的特殊字符。
- 要编码逐字字符串字面量，你可以编码 @ 符号，后跟起始双引号、字符串和结束双引号。在字符串内部，你可以输入反斜杠、制表符、换行符和其他特殊字符而无需使用转义序列。但是，要在逐字字符串字面量中输入双引号，你必须输入两个双引号。

## 如何转换数据类型

在第 3 章中，你已了解类的使用，类为从类实例化的对象提供属性和方法。现在，你将了解结构，结构与类类似。然后，你将学习如何使用这些结构和类将数据从一种类型转换为另一种类型。

## 定义数据类型的 .NET 结构和类

图 4-12 总结了定义数据类型的结构和类，以及可用于操作这些结构和类的 C# 关键字。例如，要操作 Decimal 结构，你使用 decimal 关键字。要操作 Int32 结构，你使用 int 关键字。要操作 String 类，你使用 string 关键字。

当你将变量声明为由结构支持的数据类型之一时，该变量是值类型。这意味着变量存储其自己的数据。例如，如果你将变量声明为 decimal 类型，该变量存储十进制值。此外，如果你将该变量分配给另一个十进制变量，新变量将存储该值的单独副本。

相比之下，当你将变量声明为由类支持的数据类型之一时，会从类创建对象。然后，变量存储对对象的引用，而不是对象本身。因此，对象数据类型称为引用类型。

在本图中，.NET Framework 定义的两个引用类型是 string 和 object。因此，当你将变量声明为 string 时，该变量保存对 String 对象的引用，其中包含字符串的数据。因此，可能有两个或多个变量引用同一个 String 对象。

除了 String 类之外，.NET Framework 还提供了一个通用的 Object 类。你可以使用从该类创建的变量来保存对任何类型对象的引用。你将在第 14 章中了解更多关于操作 Object 类的信息。

## 定义值类型的常见 .NET 结构

| Structure | C# keyword | What the value type holds |
|---|---|---|
| Byte | byte | An 8-bit unsigned integer |
| Int16 | short | A 16-bit signed integer |
| Int32 | int | A 32-bit signed integer |
| Int64 | long | A 64-bit signed integer |
| Single | float | A single-precision floating-point number |
| Double | double | A double-precision floating-point number |
| Decimal | decimal | A 96-bit decimal value |
| Boolean | bool | A true or false value |
| Char | char | A single character |

## 定义引用类型的常见 .NET 类

| Class | C# keyword | What the reference type holds |
|---|---|---|
| String | string | A reference to a String object |
| Object | object | A reference to any type of object |

## 描述

- 每个内置数据类型都由 .NET Framework 中的一个结构或类支持。当你使用 C# 关键字引用数据类型时，你实际上使用的是关联结构或类的别名。
- 结构定义值类型，值类型存储其自己的数据。
- 类定义引用类型。引用类型不存储数据本身。相反，它存储数据存储的内存区域的引用。
- 本图所示的所有结构和类都位于 .NET 的 System 命名空间中。

## 注意

- .NET 还为图 4-1 中列出的其他内置数据类型提供了结构。

## 如何使用方法转换数据类型

图 4-13 介绍了两种使用方法将数据从一种类型转换为另一种类型的方法。首先，你可以使用 ToString()、Parse() 和 TryParse() 方法，这些方法可从 .NET 定义的任何数据结构中使用。其次，你可以使用 Convert 类的静态方法将值转换为 .NET 定义的任何数据结构。

ToString() 方法可让你将任何值转换为字符串。例如，在本图的第一个语句组中，ToString() 方法用于将十进制值转换为字符串值。请注意，在此示例中，ToString() 方法上未提供参数。在下一张图中，你将学习如何编码格式化结果字符串的参数。

在继续之前，你应该意识到 C# 在某些情况下会隐式调用 ToString() 方法。你在本章前面学过其中一种情况，该示例在此重复。在这种情况下，双精度值在与另一个字符串连接时会自动转换为字符串。

Parse() 方法是执行 ToString() 方法相反操作的静态方法。换句话说，它将字符串值转换为另一种数据类型。例如，在第一个语句组的第三个语句中，Decimal 结构的 Parse() 方法用于将字符串变量的值转换为十进制值。但是，如图所示，此方法仅识别标准数字字符。因此，如果你尝试转换包含非数字字符（如美元符号或括号）的字符串，将会发生异常。

避免此问题的一种方法是为 Parse() 方法编码另一个参数，指示允许的字符。你将在第 9 章中了解更多相关信息。另一种方法是使用 TryParse() 方法而不是 Parse() 方法。此方法还将字符串值转换为另一种数据类型，如第一个语句组的最后一个语句所示。请注意，在这里你不会像使用 Parse() 时那样将 TryParse() 方法的结果分配给变量。相反，你在方法的第二个参数上命名变量，并在变量名前面加上 out 关键字。你将在第 6 章中了解更多关于此关键字的知识。现在，只需意识到如果转换无法执行，TryParse() 方法会在变量中存储零值并返回 false 值而不是抛出异常。然后，你可以测试返回值以确定转换是否成功。你将在第 7 章中看到该示例。

Convert 类提供了可用于将任何数据类型的<|message|> 转换为任何其他数据类型的静态方法。这由本图中的最后一个语句组说明。这里，第一个语句使用 ToDecimal() 方法将文本框中输入的字符串转换为十进制值。第二个语句使用 ToInt32() 方法将文本框中输入的字符串转换为整数值。第三个语句使用 ToString() 方法将十进制值转换为字符串值。第四个语句使用 ToInt32() 方法将十进制值转换为整数值。

当你使用 Convert 类时，你应该意识到转换结果将根据你执行的转换类型而有所不同。如果，对于

