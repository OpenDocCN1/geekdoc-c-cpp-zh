

## 如何使用日期和字符串

在第 4 章中，您已经学习了处理字符串的一些基本技能。在本章中，您将学习更多关于处理字符串的内容，并学习如何处理日期。由于您将在开发的许多应用程序中使用日期和字符串，因此您需要确保掌握本章介绍的技能。

- 如何使用日期和时间 ... 270
- 如何创建 DateTime 值 ... 270
- 如何获取当前日期和时间 ... 272
- 如何格式化 DateTime 值 ... 272
- 如何获取日期和时间的信息 ... 274
- 如何对日期和时间执行操作 ... 276
- 如何使用字符串 ... 278
- String 类的属性和方法 ... 278
- 处理字符串的代码示例 ... 280
- 更多处理字符串的代码示例 ... 282
- 如何使用 Parse() 和 TryParse() 方法验证数字输入 ... 284
- 如何使用可空引用类型 ... 286
- 如何使用 StringBuilder 类 ... 288
- 如何格式化数字、日期和时间 ... 290
- 如何格式化数字 ... 290
- 如何格式化日期和时间 ... 292
- 如何使用内插字符串 ... 294
- 总结 ... 296

### 如何使用日期和时间

在 C# 中处理日期和时间时，您需要使用 DateTime 结构。您将看到，该结构提供了各种属性和方法，用于获取日期和时间信息、格式化 DateTime 值以及对日期和时间执行操作。

#### 如何创建 DateTime 值

图 9-1 展示了创建 DateTime 值的三种方式。第一种，您可以使用 new 关键字从 DateTime 结构创建 DateTime 值。这与您创建其他内置值类型的方式不同。这是因为 C# 并未像为其他值类型提供关键字那样，为该结构提供专门的关键字。

使用 new 关键字创建 DateTime 值时，必须始终指定年、月和日。此外，您还可以选择指定小时、分钟、秒和毫秒。如果不指定时间，则时间会被设置为 12:00 AM。图 9-1 中的第一条语句说明了这一点。

您还可以使用 DateTime 结构的静态 Parse() 或 TryParse() 方法创建 DateTime 值。使用这些方法之一时，您需要将日期和时间指定为字符串，如图 9-1 中的第三、第四和第五条语句所示。这里，第三条语句仅指定了日期。因此，DateTime 值的时间部分被设置为 12:00 AM。第四条语句同时指定了日期和时间。第五条语句说明，您可以从包含日期/时间字符串的属性或变量创建 DateTime 值。在本例中，从文本框的 Text 属性创建了 DateTime 值。

最后一条语句展示了如何使用 TryParse() 方法执行与第五条语句相同的处理。请记住，使用此方法时，您需要使用 out 关键字和类型（本例中为 DateTime）来声明存储日期的变量。然后，如果字符串无法转换为 DateTime 值，此方法将返回 false 值。相反，如果 Parse() 方法无法转换该字符串，则会抛出 FormatException。

使用 Parse() 或 TryParse() 方法创建 DateTime 值时，指定的日期和时间必须是有效格式。图 9-1 列出了一些最常见的格式。在本章稍后，您将了解更多关于可接受的日期和时间格式。

尽管图 9-1 中的语句指示了所创建的 DateTime 值，但您应该意识到，这些并不是实际存储在变量中的值。相反，它们显示了将 DateTime 值转换为字符串时发生的情况。日期和时间实际上存储为自 0001 年 1 月 1 日 12:00:00 AM 以来经过的计时周期数（100 纳秒单位）。这使得对日期和时间执行算术运算变得容易，正如您将在本章稍后看到的那样。

#### 创建 DateTime 值的语法

```csharp
DateTime variableName = new DateTime(year, month, day
    [, hour, minute, second[, millisecond]]);
```

#### 如何使用 Parse() 方法创建 DateTime 值

```csharp
DateTime variableName = DateTime.Parse(string);
```

#### 如何使用 TryParse() 方法创建 DateTime 值

```csharp
DateTime.TryParse(string, out DateTime variableName);
```

#### 创建 DateTime 值的语句

```csharp
DateTime startDate = new DateTime(2020, 01, 30);      // 1/30/2020 12:00 AM
DateTime startDateAndTime =
    new DateTime(2020, 1, 30, 14, 15, 0);      // 1/30/2020 2:15 PM

DateTime startDate = DateTime.Parse("01/30/20");      // 1/30/2020 12:00 AM
DateTime startDateAndTime
    = DateTime.Parse("Jan 30, 2020 2:15 PM");      // 1/30/2020 2:15 PM
DateTime invoiceDate = DateTime.Parse(txtInvoiceDate.Text);

DateTime.TryParse(txtInvoiceDate.Text, out DateTime invoiceDate);
```

#### 有效的日期格式

- 01/30/2020
- 1/30/20
- 01-01-2020
- 1-1-20
- 2020-01-01
- Jan 30 2020
- January 30, 2020

#### 有效的时间格式

- 2:15 PM
- 14:15
- 02:15:30 AM

#### 说明

- 您可以使用 .NET 的 DateTime 结构来创建并处理日期和时间。
- 要创建 DateTime 值，您可以使用 new 关键字，然后指定要用于创建日期的日期和时间值。
- 您还可以使用 DateTime 结构的静态 Parse() 或 TryParse() 方法从字符串创建 DateTime 值。
- 如果在创建 DateTime 值时省略了时间说明，则时间会被设置为 12:00 AM。当使用 Parse() 或 TryParse() 方法创建 DateTime 值时，您还可以省略日期说明。此时，日期会被设置为当前日期。
- 日期存储为 64 位有符号整数，表示自 0001 年 1 月 1 日 12:00 AM 以来经过的计时周期数（100 纳秒单位）。

#### 如何获取当前日期和时间

图 9-2 展示了 DateTime 结构可用来获取当前日期和时间的两个静态属性。如果使用 Now 属性，则返回日期和时间。如果使用 Today 属性，则仅返回日期，时间则被设置为 12:00:00 AM。图 9-2 中的前两条语句说明了其工作原理。

#### 如何格式化 DateTime 值

要格式化日期和时间，您可以使用图 9-2 中显示的 DateTime 结构的四个方法。但请注意，这些格式可能与您系统上使用的格式略有不同。具体格式取决于您计算机的区域设置。如果这些方法无法提供您需要的格式，您可以使用本章稍后将要学习的格式化技巧，按照您想要的方式格式化日期和时间。

#### 用于获取当前日期和时间的 DateTime 属性

| 属性 | 描述 |
| --- | --- |
| Now | 返回当前日期和时间。 |
| Today | 返回当前日期。 |

#### 获取当前日期和时间的语句

```csharp
DateTime currentDateTime = DateTime.Now;      // 1/30/2020 4:24:59 AM
DateTime currentDate = DateTime.Today;          // 1/30/2020 12:00:00 AM
```

#### 用于格式化日期或时间的 DateTime 方法

| 方法 | 描述 |
| --- | --- |
| ToLongDateString() | 将 DateTime 值转换为包含星期名称、月份名称、月中的日期和年份的字符串。 |
| ToShortDateString() | 将 DateTime 值转换为包含月、日和年数字的字符串。 |
| ToLongTimeString() | 将 DateTime 值转换为包含小时、分钟和秒的字符串。 |
| ToShortTimeString() | 将 DateTime 值转换为包含小时和分钟的字符串。 |

#### 格式化日期和时间的语句

```csharp
string longDate =
    currentDateTime.ToLongDateString();      // Thursday, January 30, 2020
string shortDate =
    currentDateTime.ToShortDateString();     // 1/30/2020
string longTime =
    currentDateTime.ToLongTimeString();      // 4:24:59 AM
string shortTime =
    currentDateTime.ToShortTimeString();     // 4:24 AM
```

#### 说明

- Now 和 Today 属性是 DateTime 结构的静态属性。
- 用于日期或时间的格式取决于您计算机的区域设置。

