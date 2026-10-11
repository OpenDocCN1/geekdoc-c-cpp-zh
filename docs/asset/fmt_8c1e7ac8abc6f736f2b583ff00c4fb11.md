
要编写执行分组、排序及其他聚合函数的查询语句，请按照以下步骤操作。如果你已关闭 `Visual Studio`，请先重复上一项练习。请务必在结束本练习时保持 `Visual Studio` 处于打开状态，因为你稍后会用到这个应用程序。

- 1. 编写一个新的查询，按姓氏的首个字符对 `contacts` 集合进行分组。
- 2. 编写一个 `foreach` 语句来打印分组键，并包含一个嵌套的 `foreach` 语句来打印组中每个联系人的姓氏。
- 3. 按 `Ctrl+F5` 运行应用程序。输出结果应与图 12.4 相似。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_295_0.png)

**图 12.4**

数据分组

## 连接数据

`LINQ` 还允许你通过将多个数据源连接到一个或多个公共字段上来合并它们。连接数据对于查询那些关系无法直接跟踪的数据源至关重要。与 `SQL` 不同，`SQL` 支持使用多种不同的运算符进行连接，而 `LINQ` 中的连接操作是基于键的相等性的。

在扩展之前仅使用 `Contact` 类的示例的基础上，执行连接操作至少需要两个类。`Contact` 类再次展示在清单 12.9 中，同时还包含一个新的 `JournalEntry` 类。继续假设 `contacts` 列表是通过调用 `GetContacts` 填充的，而 `journal` 列表是通过调用 `GetJournalEntries` 填充的。

### 清单 12.9 Contact 和 JournalEntry 类

```csharp
class Contact
{
    public int Id { get; set; }
    public string Company { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
    public string Address { get; set; }
    public string City { get; set; }
    public string StateProvince { get; set; }
}

class JournalEntry
{
    public int Id { get; set; }
    public int ContactId { get; set; }
    public string Description { get; set; }
    public string EntryType { get; set; }
    public DateTime Date { get; set; }
}

IEnumerable<Contact> contacts = GetContacts();
IEnumerable<JournalEntry> journal = GetJournalEntries();
```

`LINQ` 中最简单的 *join* 查询在功能上等同于 `SQL` 中的 *inner join*，并使用 *join* 子句。与可以使用多种不同运算符的 `SQL` *joins* 不同，`LINQ` 中的 *joins* 只能使用相等运算符，被称为**等值连接**（equijoins）。

清单 12.10 展示了一个查询，该查询使用 `Contact.ID` 和 `JournalEntry.ContactId` 字段作为连接键，将 `Contact` 对象列表连接到 `JournalEntry` 对象列表。

### 清单 12.10 使用 Join 的 LINQ 查询

```csharp
var result =
    from contact in contacts
    join journalEntry in journal
    on contact.Id equals journalEntry.ContactId
    select new
    {
        contact.FirstName,
        contact.LastName,
        journalEntry.Date,
        journalEntry.EntryType,
        journalEntry.Description
    };
```

清单 12.10 中的 *join* 子句创建了一个名为 `journalEntry` 的 *范围变量*（range variable），其类型为 `JournalEntry`，然后使用 *equals* 运算符连接这两个数据源。

`LINQ` 还有一个 *group join*（分组连接）的概念，在 `SQL` 查询中没有对应的部分。*group join* 使用 *into* 关键字，并创建具有层次结构的结果。就像你对 *group* 子句所做的那样，你需要嵌套的 *foreach* 语句来访问结果。

**注意！**

**顺序很重要**

在处理 `LINQ` *joins* 时，顺序很重要。要被连接的数据源必须位于 *equals* 运算符的左侧，而连接的数据源必须位于右侧。在此示例中，`contacts` 是要被连接的数据源，而 `journal` 是连接的数据源。

幸运的是，编译器可以捕获这类错误并生成编译错误。如果你在 `join` 子句中交换参数，你会得到以下编译错误：

> 名称 'journalEntry' 不在 'equals' 左侧的作用域内。请考虑交换 'equals' 两侧的表达式。

另一个需要注意的重要事项是，`join` 子句使用的 `equals` 运算符与相等性（`==`）运算符不同。

清单 12.11 展示了一个连接 `contacts` 和 `journal` 的查询，并返回按联系人姓名分组的结果。组中的每个条目都有一个由返回的匿名类型中的 `JournalEntries` 属性表示的日志条目枚举集合。

### 清单 12.11 使用 Group Join 的 LINQ 查询

```csharp
var result =
    from contact in contacts
    join journalEntry in journal
    on contact.Id equals journalEntry.ContactId
    into journalGroups
    select new
    {
        Name = contact.LastName + ", " + contact.FirstName,
        JournalEntries = journalGroups
    };
```

## 扁平化数据

虽然选择数据和连接数据通常返回形状正确的结果，但这种层次结构有时处理起来会显得繁琐。`LINQ` 允许你创建返回扁平化数据的查询，方式与查询 `SQL` 数据源时非常相似。

假设你修改 `Contact` 和 `JournalEntry` 类，在 `Contact` 类中添加一个名为 `Journal` 的 `List<JournalEntries>` 字段，并从 `JournalEntry` 类中移除 `ContactId` 属性，如清单 12.12 所示。

### 清单 12.12 修订后的 Contact 和 JournalEntry 类

```csharp
class Contact
{
    public int Id { get; set; }
    public string Company { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}
```

```csharp
public string Address { get; set; }
public string City { get; set; }
public string StateProvince { get; set; }
public List<JournalEntry> Journal;
}

class JournalEntry
{
    public int Id { get; set; }
    public string Description { get; set; }
    public string EntryType { get; set; }
    public DateTime Date { get; set; }
}

IEnumerable<Contact> contacts = GetContacts();
```

然后，你可以使用以下查询对联系人集合进行查询，以获取特定联系人的日记条目列表，如下所示（列表 12.13）。

### 列表 12.13 选择可枚举集合的 LINQ 查询

```csharp
var result =
    from contact in contacts
    where contact.Id == 1
    select contact.Journal;

foreach(var item in result)
{
    foreach(var journalEntry in item)
    {
        Console.WriteLine(journalEntry);
    }
}
```

虽然这样可行并能返回结果，但它仍然需要嵌套的 `foreach` 语句才能生成正确的结果。幸运的是，`LINQ` 提供了一种查询语法，支持从多个数据源进行选择，从而能够以扁平化的方式返回数据。列表 12.14 中的代码展示了如何编写此查询，通过使用多个 `from` 子句，只需一个 `foreach` 语句即可。

### 列表 12.14 选择扁平化数据的 LINQ 查询

```csharp
var result =
    from contact in contacts
    from journalEntry in contact.Journal
    where contact.Id == 1
    select journalEntry;

foreach(var journalEntry in result)
{
    Console.WriteLine(journalEntry);
}
```

## 标准查询运算符方法

你刚刚看到的所有查询都使用声明式查询语法；然而，它们也可以用标准查询运算符方法调用来编写，这些方法实际上是定义在 `System.Linq` 命名空间中的 `Enumerable` 类的扩展方法。编译器将使用声明式语法的查询表达式转换为等效的查询运算符方法调用。

只要你在 `using` 语句中包含 `System.Linq` 命名空间，就可以看到任何实现了 `IEnumerable<T>` 接口的类上的标准查询运算符方法，如图 12.5 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_299_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_299_1.png)

虽然声明式查询语法支持几乎所有的查询操作，但有一些操作，例如 `Count` 或 `Max`，没有等效的查询语法，必须以方法调用的形式表达。由于每个方法调用都返回一个 `IEnumerable`，因此你可以通过串联方法调用来组合复杂的查询。这就是编译器在编译你的声明式查询表达式时替你做的事情。

列表 12.15 展示了使用方法语法而非声明式语法的列表 12.4 中的相同查询，两者的输出将是相同的。`Where` 方法对应于 `where` 子句，而 `Select` 方法对应于 `select` 子句。

### 声明式还是方法语法

使用声明式语法还是方法语法的选择完全是个人偏好，取决于你觉得哪一种更易读。无论选择哪一种，执行查询的结果都将相同。

*顺便提及*

### 列表 12.15 使用方法语法的 LINQ 查询

```csharp
var result = contacts
    .Where(contact => contact.StateProvince == "FL")
    .Select(contact => new { contact.FirstName, contact.LastName });

foreach(var name in result)
{
    Console.WriteLine(name.FirstName + " " + name.LastName);
}
```

## 语言子表达式（Lambdas）

在列表 12.15 中，你可能注意到传递给 *Where* 和 *Select* 方法的参数与你之前使用的不同。这些参数实际上包含代码而不是数据类型。在第 6 小时“事件和事件处理”中，你学习了委托，它允许将方法作为参数传递给其他方法，以及匿名方法，它允许你编写一个未命名的内联语句块，可以在委托调用中执行。

这些概念的组合就是 `lambda`，它是一种可以包含表达式和语句的匿名函数。`Lambdas` 使你能够以更方便、更紧凑的方式编写通常使用匿名方法或泛型委托编写的代码。

### 顺便提及

#### Lambdas 和委托

由于 `lambdas` 是编写委托的更紧凑方式，你可以在通常使用委托的任何地方使用它们。因此，`lambda` 的正式参数类型必须与相应的委托类型完全匹配。返回类型也必须能隐式转换为主委托的返回类型。

虽然 `lambdas` 没有类型，但它们可以隐式转换为任何兼容的委托类型。这种隐式转换使你无需显式赋值即可传递它们。

`C#` 中的 `lambdas` 使用 `lambda` 运算符 (`=>`)。如果你在方法上下文中思考 `lambda`，运算符的左侧指定正式参数列表，运算符的右侧包含方法体。适用于匿名方法的所有限制也适用于 `lambdas`。

列表 12.15 中 *Where* 方法的参数 `contact => contact.StateProvince == "FL"` 读作“contact 指向 contact.StateProvince 等于 FL”。

### 捕获和定义的变量

`Lambdas` 还具有“捕获”变量的能力，这些变量可以是包含方法的局部变量或参数。这使得 `lambda` 的主体可以通过名称访问被捕获的变量。如果被捕获的变量是局部变量，则必须在 `lambda` 中使用它之前确保其已被赋值。被捕获的参数不能是 `ref` 或 `out` 参数。

然而，要小心，因为被 `lambdas` 捕获的变量在引用它的委托超出作用域之前不会 eligible 垃圾回收。在 `lambda` 内部引入的任何变量在外部包含方法中不可见。这也适用于输入参数名称，因此你可以对多个 `lambdas` 使用相同的标识符。

**你知道吗？**

## 表达式 Lambdas

当 `lambda` 在运算符右侧包含表达式时，它是一个**表达式 lambda**，并返回该表达式的结果。表达式 `lambda` 的基本形式是

```csharp
输入参数 => 表达式
```

如果只有一个输入参数，括号是可选的。如果你有任何其他数量的输入参数，包括没有参数，则括号是必需的。

正如泛型方法可以推断其类型参数的类型一样，`lambdas` 也可以推断其输入参数的类型。如果编译器无法推断类型，你可以显式指定类型。列表 12.16 展示了表达式 `lambda` 的不同形式。

### 列表 12.16 表达式 Lambda 示例

```csharp
x => Math.Pow(x, 2)
(x, y) => Math.Pow(x, y)
() => Math.Pow(2, 2)
(int x, string s) => s.Length < x
```

如果你将表达式 `lambda` 的表达式部分视为方法的主体，那么表达式 `lambda` 包含一个隐式 `return` 语句，返回表达式的结果。

### 包含方法调用的表达式 Lambdas

虽然列表 12.16 中的大多数示例在运算符右侧使用了方法，但如果你创建将在另一个领域（如 `SQL Server`）中使用的 `lambdas`，你不应该使用方法调用，因为它们在 `.NET Framework` 公共语言运行时边界之外没有意义。

### 试一试

**使用表达式 Lambdas**

按照这些步骤，你将学习如何使用表达式 `lambdas` 与 `LINQ` 查询方法。如果你关闭了 `Visual Studio`，请先重复上一个练习。

- 1. 修改你在之前练习中编写的声明式查询表达式，以使用相应的标准查询方法。
- 2. 按 `Ctrl+F5` 运行应用程序。输出应与之前练习的输出匹配。

## 语句 Lambdas

在右侧由花括号包围一个或多个语句的 `lambda` 称为语句 `lambda`。语句 `lambda` 的基本形式是

```csharp
(输入参数) => { 语句; }
```

与表达式 `lambdas` 一样，如果只有一个输入参数，括号是可选的；否则，它们是必需的。语句 `lambdas` 也遵循相同的类型推断规则。

虽然表达式 `lambdas` 包含隐式 `return` 语句，但语句 `lambdas` 不包含。你必须显式指定语句 `lambda` 中的 `return` 语句。`return` 语句仅使 `lambda` 表示的隐式方法返回，而不是外部包含的方法。列表 12.17 展示了语句 `lambda` 的不同形式。

### 列表 12.17 语句 Lambda 示例

```csharp
(x) => { return x++; };

CheckBox cb = new CheckBox();
cb.CheckedChanged += (sender, e) =>
{
    MessageBox.Show(cb.Checked.ToString());
};

Action<string> myDel = n =>
{
    string s = n + " + "World";
    Console.WriteLine(s);
};

myDel("Hello");
```

语句 `Lambda` 表达式不能包含目标位于 `Lambda` 表达式自身作用域之外的 `goto`、`break` 或 `continue` 语句。类似地，正常的范围规则会阻止从外层 `Lambda` 表达式分支进入嵌套的 `Lambda` 表达式。

## 预定义委托
