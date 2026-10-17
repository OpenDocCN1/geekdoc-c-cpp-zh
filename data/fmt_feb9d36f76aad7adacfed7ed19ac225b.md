
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
ItemName.Length > 0, Employee.Role: "Admin" => true,

#pragma warning disable IDE0170 // 属性模式可以简化

// 属性模式

ItemName: { Length > 0 }, Employee: { Role: "Manager" },

ExpenseDate: DateTime date

#pragma warning restore IDE0170 // 属性模式可以

when date >= DateTime.Now.AddDays(-30) => true,

{ ItemName.Length > 0, Employee.Name.Length > 0,

CostAmount: < 1000, ExpenseDate: DateTime date

when date >= DateTime.Now.AddDays(-30) => true,

{ } => false, // 此非空检查可以消除。

=> false

};
```

关于所有属性匹配需要注意的第一个重要点是，它们只有在输入操作数不为 `null` 时才会匹配。这就是为什么例如，一个空属性匹配的匹配表达式 `{ }` 只要输入操作数不为 `null` 就会匹配。（在列表 7.30 中，`{ }` 匹配表达式是冗的，因为 `switch` 结尾的默认匹配表达式会捕获 `null` 以及所有穿透下来的剩余非空操作数）。虽然它可以作为非空检查，但直接指定 `null`（C# 9.0）更佳，因为其语法更清晰。

在列表 7.30 中，`switch` 表达式中的第一个匹配表达式以 `ItemName.Length > 0` 开始，要求 `ItemName.Length` 大于 0。该表达式隐含了 `ItemName` 也不为 `null`。事实上，初始的空检查是隐式的，编译器不允许在属性表达式中使用空条件（`ItemName?.Length`）。

在列表 7.30 中，第一个匹配表达式还要求 `Employee.Role` 被设置为 `"Admin"`。如果这两个匹配表达式匹配成功，`switch` 将返回 `true`，表示 `ExpenseItem` 是有效的。完整的匹配

# 第 7 章：继承

表达式使用了扩展的点符号表示法来访问子属性（`Length` 和 `Role`）。

列表 7.30 的第二个匹配表达式 `{ ItemName: { Length: >0 }, Employee: {Role: "Manager"}, ExpenseDate: DateTime date }` 也是一个属性匹配表达式（而不是扩展属性表达式），但语法略有不同。属性匹配表达式是在 C# 7.0 中引入的并且仍然受支持，尽管会有警告），因为扩展语法在所有情况下都更简单且更受青睐。

这个第二个匹配表达式包含了对 `ExpenseDate` 的属性匹配，并并在其中声明了一个变量 `date`。虽然 `date` 仍作为 `switch` 过滤的一部分使用，但它出现在 `when` 子句中而不是匹配表达式中。

## when 子句

对于所有形式的常量和关系匹配表达式，必须使用常量。然而，鉴于比较操作数通常在编译时不可用，这可能会具有限制性。为了避免这种限制，C# 7.0 引入了 `when` 子句，你可以在其中添加任何条件表达式（返回布尔值的表达式）。

列表 7.30 中的代码声明了一个 `DateTime` 变量，用以检查 `ExpenseItem.ExpenseDate` 不早于 30 天。然而，由于年龄取决于当前的日期和时间，该值不是常量，我们无法使用匹配表达式。相反，代码在匹配表达式之后使用了 `when` 子句，将 `date` 值与 `DateTime.Now.AddDays(-30)` 进行比较。该子句为（可选的）更复杂的条件提供了一个捕获位置，而不受仅使用常量的限制。

`when` 子句的添加是 C# 7.0 允许匹配表达式的核心原因。

## 无关类型的模式匹配

模式匹配的一项有趣功能是，它使得从无关类型中提取数据变得可能。列表 7.31 提供了一个示例。

```csharp
// 列表 7.31：switch 中的模式匹配
public static string? CompositeDateFormat(object input, string formatString) =>
    input switch
    {
        DateTime { Year: int year, Month: int month, Day: int day } => (year, month, day),
        DateTimeOffset { Year: int year, Month: int month, Day: int day } => (year, month, day),
        DateOnly { Year: int year, Month: int month, Day: int day } => (year, month, day),
        string dateText when DateTime.TryParse(dateText, out var date) => (date.Year, date.Month, date.Day),
        _ => null
    } is (int year, int month, int day) ? string.Format(formatString, year, month, day) : null;
```

## 递归模式匹配 (C# 7.0)

```csharp
// 列表 7.32：使用 is 运算符的递归模式匹配
Person inigo = new("Inigo", "Montoya");
var buttercup = (FirstName: "Princess", LastName: "Buttercup");
(Person inigo, (string FirstName, string LastName) buttercup) couple = (inigo, buttercup);
if (couple is
    // 元组：从 Person 的解构造函数中检索
    ( // 位置：选择左侧或元组
        { // FirstName 的属性
            Length: int inigoFirstNameLength
        }))
{
    // ...
}
```

# 模式匹配 435

```cs
// 丢弃元组的姓名部分
,
{
  // Princess Buttercup 元组的属性
  FirstName: string buttercupFirstName
  Console.WriteLine("$ { inigoFirstNameLength }, { buttercupFirstName }}");
}
else {
  // ...
}
// ...
```

在此示例中，`couple` 的类型如下：

`(Person, (string FirstName, string LastName))`

因此，第一次匹配发生在外部元组 `(inigo, buttercup)` 上。接下来，对 `inigo` 使用位置模式匹配，利用了 `Person` 解构器。这选择了一个 `(FirstName, LastName)` 元组，并使用属性模式匹配提取 `inigo.FirstName` 值的 `Length`。位置匹配中的 `LastName` 部分通过下划线丢弃。最后，使用属性模式匹配选择 `buttercup.FirstName`。

虽然模式匹配是选择数据的强大手段，但它并非没有注意事项：请留意列表 7.32 中的注释，理解这段代码可能具有挑战性。如果没有注释，会更加困难：

```cs
if(couple is ( { Length: int inigoFirstNameLength }, _ ), { FirstName: string buttercupFirstName }}) { ...}
```

尽管如此，模式匹配真正证明有用的地方是在 `switch` 语句和表达式中。

## 列表模式 (C# 11.0)

C# 11 的一个重要新特性是引入了列表模式。这些模式允许对数组等项目项列表进行模式匹配。因此，你可以对列表内的元素使用任何类型的模式匹配。7.33 演示了如何解析 `Main` 方法的 `args` 参数。

列表 7.33：`switch` 表达式中的模式匹配

```cs
public static void Main(string[] args)
{
    // 为了简单起见，假设所有选项
    // 都是小写的。
    // 第一个参数是选项，通过
    // '/','-' 或 '--' 前缀识别。
    switch (args)
    {
        case "--" or ['/' or '-', 'h' or '?']:
            // Display.help, /h, -h, ?, -?
            DisplayHelp();
            break;
        case ['/' or '-', char option], ..]:
            // 选项以 '/' 开头并有 0 或多个参数。
            if(EvaluateOption("${option}", args[1..]))
            {
                DisplayHelp();
            }
            break;
        case ['-', ..] option, ..:
            // 选项以 "--" 开头并有 0 或多个参数。
            if(EvaluateOption(option[2..], args[1..]))
            {
                DisplayHelp();
            }
            break;
        // 以下情况与 default 重复
        // 但仅为了演示目的而提供。
        case []:
            // 无命令行参数
    }
    default:
        DisplayHelp();
}
```

# 模式匹配

```cs
break;
}
private static bool EvaluateOption(string option, string[] args) =>
    (option, args) switch
{
    ("cat" or "c", [string fileName]) =>
        CatalogFile(fileName),
    ("copy", [string sourceFile, string targetFile]) =>
        CopyFile(sourceFile, targetFile),
    _ => false
};
```

```cs
private static bool CopyFile(object sourceFile, string targetFile)
{
    Console.WriteLine($"'{sourceFile}' '{targetFile}'...");
    return true;
}
```

列表 7.33 中的第一个情况查找文本 `"-help"` 作为 `args` 数组的第一个也是唯一的元素。如果没有匹配，列表表达式的剩余部分将在以 `/` 或 `-` 开头且后跟 `?` 或 `h` 的第一个元素上进行匹配。列表模式的后半部分查找恰好两个字符（因为字符串是字符数组），这由表达式中的逗号（`.`）识别，该逗号将前缀与单字符表达式隔开：

```cs
['/' or '-', 'h' or '?']
```

接下来的两个情况也评估 `args` 的第一个元素，确定第一个字符是否为 `/` 或 `-`；在第三种情况下，确定 `args` 的第一个元素是否以 `--` 开头。在这两种情况下，如果匹配，`args[]` 将赋值给 `option` 变量。遗憾的是，没有办法将列表的剩余元素捕获到变量中。列表匹配总是查找精确数量的元素。因此，当调用 `EvaluateOptions()` 时，我们使用范围 `[1..]` 来传递剩余元素。（参见 https://essentialsharp.com/arrays 获取示例）。

第四种情况使用 `[]` 来识别具有零元素的列表。在这个示例中，它是多余的，因为 `default` 情况也捕获了剩余参数。在列表 7.33 的 `EvaluateOptions` 方法中，我们使用元组来首先评估命令。对于 `"cat"` 匹配表达式，它查找一个项目；而对于 `"copy"` 匹配表达式，它查找恰好两个项目。在两种情况下，它都将数组捕获到变量中。模式匹配非常强大，由于它可以处理字符串，它使得简单的场景无需使用正则表达式。

## 在可以使用多态时避免模式匹配

虽然模式匹配功能很重要，但在使用模式匹配之前，你应该考虑与多态相关的问题。多态支持在不需要修改的情况下扩展数据类型。例如，将 `Name` 等成员放在基类 `PdaItem` 中，然后处理派自 `PdaItem` 的值，比使用模式匹配处理新引入的类型更好。无论如何，多态总是可能的，当不可能时，模式匹配（特别是类似于属性匹配的）提供了良好的替代方案。

多态失效的一种场景是对象层次结构不匹配你的目标——例如你正在处理属于无关系统的类。此外，假设需要多态的代码无法修改。在 7.33 中处理日期就是这样一个例子。第二种场景是你正在添加的功能不属于这些类的抽象。例如，不同类型的车辆在收费公路上支付的通行费不同，但通行费并不是车辆的核心功能。

### 高级主题

## 使用 `as` 运算符

除了运算符之外，C# 还有 `as` 运算符。最初，`as` 运算符比 `is` 运算符具有优势：它不仅检查操作数是否为特定类型，还尝试转换为特定的数据类型，如果源类型不是目标类型（在继承链内），则分配 `null`。此外，它比强制转换更有优势，因为它不会抛出异常。列表 7.34 演示了 `as` 运算符的使用。

列表 7.34：使用 `as` 运算符进行数据转换

```cs
public class PdaItem {
    protected Guid ObjectKey { get; }
    // ...
}
public class Contact : PdaItem {
    // ...
    public Contact(string name) => Name = name;
    static public Contact Load(PdaItem pdaItem) {
        #pragma warning disable IDE0019 // 使用模式匹配
        Contact? contact = pdaItem as Contact;
        #pragma warning restore IDE0019 // 使用模式匹配
        if (contact != null) {
            System.Diagnostics.Trace.WriteLine($"ObjectKey: {contact.ObjectKey}");
            return (Contact)pdaItem;
        }
    else {
        throw new ArgumentException("Item is not contact");
    }
}
```

```$"{nameof(pdaItem)} was not of type {nameof(Contact)}";
}
  // ...
}
```
