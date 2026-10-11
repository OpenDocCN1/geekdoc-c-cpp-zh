
```csharp
// 调用实例方法 ConvertToUpper。
// 首先创建 Conversion 类的实例
Conversion conv = new Conversion();
string instResult = conv.ConvertToUpper("conversion");
// 调用方法 ConvertToLower。
string classResult = Conversion.ConvertToLower("CONVERSION");
```

**图 4.62** 使用类名名前缀调用类方法和实例方法的示例。图 4.62 显示了用于调用这两种方法的代码。

在某些情况下，如果人们想从这些类的任何实例上调用静态方法，查询将变得非常复杂。为了解决这个复杂的问题，开发了扩展方法（extension methods）来简化查询结构和语法。

要从现有的静态方法声明扩展方法，只需在静态方法的第一个参数上添加关键字。例如，要使 `ConvertToLower()` 方法变为扩展方法，请在该方法的第一个参数上添加该关键字，如图 4.63 所示。

现在，类方法 `ConvertToLower()` 已经转换为扩展方法，并且可以通过 `Conversion` 类的任何实例访问。

扩展方法具有以下重要属性：

- 1. 扩展方法将作为任何与扩展方法的第一个参数数据类型相同的对象的实例方法发挥工作。

- 2. 扩展方法只能在静态类中声明。

- 3. 类方法和扩展方法都以 `static` 关键字为前缀。

```csharp
public static class Conversion
{
    // 将类方法 ConvertToLower 声明为扩展方法。
    public static string ConvertToLower(this string input)
    {
        return input.ToLower();
    }
}
```

**图 4.63** 将类方法 `ConvertToLower()` 声明为扩展方法。

# 语言集成查询 (LINQ) 简介

参考图 4.63，扩展方法 `ConvertToLower` 的数据类型为 `string`，因为第一个参数的类型是 `string`。该方法声明在一个静态类中，且类和此方法都以 `static` 关键字为前缀。

## 4.9.3 隐式类型局部变量

在 LINQ 查询中，另一个称为隐式类型变量（或简写 `var`）的特性指示编译器推断局部变量的类型。随着 C# 引入匿名类型，出现了一个新问题：如果一个变量被实例化为未命类型。LINQ 查询属于强类型查询，类型为 `IEnumerable<>` 和 `IQueryable<>`，正如本章开头讨论的那样。

当这段代码未指示类型时，将遇到编译错误。在 C# 3.0 对 LINQ 的语言增强中，开发了一个新术语——隐式类型 `var`，用于解决此类问题。参考图 4.64。

这次如果你编译这段代码，将不会有错误，因为该关键字告知编译器从变量的初始化器中推断类型。在这个示例中，隐式类型变量的初始化器是 `string`。这意味着隐式类型局部变量在编译时进行静态检查，因此需要初始化器以允许编译器从其推断出类型。

有类型局部变量意味着这些变量仅在方法内部，它们不可能逃逸方法属性、索引器或其他块的范围。C# 3.0 对 LINQ 语言增强的另一个重要性点是对象初始化器。对象初始化器允许在单个表达式中分配多个属性或字段。例如，对象创建的常用模式如图 4.66 所示。在这个示例中，`Faculty` 没有具有 faculty ID、名称、办公室和头衔的构造函数；但是有四个属性……

**图 4.64** 声明一个匿名类型。

**图 4.65** 使用隐式类型变量声明匿名类型。

```csharp
var faculty = new Faculty()
{
    faculty_id = "B7880",
    faculty_name = "Ying Bai",
    office = "MTC21",
    title = "Associate Professor"
};
```

**图 4.66** 使用对象初始化器创建实例的示例。对象初始化器允许在实例化过程的同时完成所有必要的初始化以创建一个新实例。

## 4.9.4 查询表达式

为了执行任何类型的 LINQ 查询（例如 LINQ to Objects、LINQ to ADO.NET、LINQ to XML），需要有效的查询表达式。C# 3.0 中的查询表达式语法更接近 SQL 语句，并由一些子句组成。最流行的查询表达式是 `foreach` 语句。当执行它时，编译器会将其转换为一个带有 `GetEnumerator()` 和 `MoveNext()` 等调用的循环。使用 `foreach` 循环执行查询的主要优势是它在枚举数组、集合时提供了显著的简单性，并以简单的方式返回结果。查询表达式的典型语法如图 4.67 所示。

通常，查询表达式由两个块组成。图 4.67 顶部的块是 `from` 子句块，查询体（query-body）块是查询体块。`from` 子句仅负责查询信息（无查询结果），而查询体块执行实际查询并包含结果。

参考图 4.67 所示的语法，查询表达式应包含以下组件：

- 变量必须以显式（`IEnumerable<T>`）或隐式（`var`）定义。

- 查询表达式可以用查询语法或方法语法表示。

- 查询表达式必须以 `from` 子句开始，并以 `select` 或 `group` 子句结束。在第一个 `from` 子句和最后一个 `select` 或 `group` 子句之间，它可以包含一个或多个可选子句：`where`、`order by`、`join` 和 `let`。

使用 LINQ to DataSet 的所有查询都将转换为标准查询运算符（SQO）方法，如 `From()`、`Where()`、`OrderBy()`、`Join()`、`Let()` 以及 `Select()`。

```csharp
var query_variable = from [data source]
                     let [expression]
                     where [boolean expression]
                     order by [expression] ascending/descending
                     select [expression];

foreach (range_variable in query_variable)
{
    // 从 range_variable 选择或检索每个元素
}
```

**图 4.67** 查询表达式的典型语法。

```csharp
static void Main()
{
    IEnumerable<Faculty> faculty = db.Faculty.Where(f => f.faculty_id == "D.*",
    f => f.college == "U.*",
    f => f.title == "Associate Professor");

    // 执行查询产生结果
    foreach (Faculty f in faculty)
    {
        Console.WriteLine("{0}\n{1}\n{2}\n{3}\n{4}",f.name, f.title, f.office, f.phone, f.email);
    }
}
```

**图 4.68** 查询表达式的真实示例。

语言集成查询 (LINQ) 基于 .NET Framework 3.5，是 Visual Studio.NET 2008 发布的热技术。LINQ 用于查询以不同格式呈现的数据源，例如对象、DataSet、SQL Server 数据库、实体和 XML。LINQ 的创新缩小了对象世界与数据世界的差距。

本章第一部分提供了 LINQ 通用编程指南。LINQ 中广泛使用的常用接口（如 `Enumerable`、`IEnumerable<T>`、`IQuery` 和 `IQueryable<T>`）以及标准查询运算符（SQO，包括延迟和非延迟 SQO）将在该部分进行讨论。

本章第二部分给出了 LINQ 查询简介。在介绍之后，将按照下列顺序对针对不同数据源实现的 LINQ 进行详细讨论和分析。

- 1) LINQ 架构与组件

- 2) LINQ to Objects

- 3) LINQ to DataSet

- 4) LINQ to SQL

- 5) LINQ to Entities

- 6) LINQ to XML

- 7) C# 3.0 对 LINQ 的语言增强

对于上述列出的每个部分都提供了字面上的介绍和实际示例，以便读者不仅对应用于不同数据的 LINQ 技术有一个通性且全局的认识，还能对实现所需功能的程序代码有实践且真实的感受。

# 170

# 使用 C# 进行 SQL Server 数据库编程

本章提供了 12 个真实项目，帮助读者理解并跟进本章中讨论的所有技术。

在完成本章后，读者应该能够：

- 理解 LINQ 中实现的基础架构和组件

- 理解标准查询运算符（Standard Query Operators）的功能

- 理解 LINQ 中实现的通用接口，例如 LINQ to Objects、LINQ to DataSet、LINQ to Entities（实体 LINQ 实体）和 LINQ to XML。

- 理解 C# 3.0 针对 LINQ 的语言增强

- 设计并构建真实应用程序，应用 LINQ 查询对所有不同的数据源执行数据操作

- 开发并构建应用程序，应用 C# 3.0 针对 LINQ 的语言增强对数据源执行所有查询

从下一章开始，我们将侧重于通过真实项目使用 Visual C#.NET 进行数据库编程。

## 作业

### I.判断题

1. LINQ 查询是构建在 .NET Framework 3.5 之上的。

2. 用于 LINQ 查询的最流行的接口是：`IEnumerable`、`IEnumerable<T>`、`IQueryable` 和 `IQueryable<T>`。

3. `IEnumerable` 接口用于将数据源的数据类型转换为 LINQ 查询可以实现的 `IEnumerable<T>`。

4. `Enumerable` 接口继承自 `IQueryable` 类。

5. 所有标准查询运算符方法都是 `IEnumerable` 中的静态方法（`static`）。

6. `IEnumerable` 和 `IQueryable` 接口主要用于 C# 早期版本支持的非泛型集合，如 C# 1.0 或更早版本。

7. 所有 LINQ 查询表达式只能以查询语法的形式表示。

8. LINQ 查询表达式将在编译期间由 CLR 转换为标准查询运算符方法。

9. LINQ 查询中使用的变量包含了查询信息和返回的查询结果。

10. LINQ to SQL、LINQ to DataSet 和 LINQ to Entities 属于 LINQ to ADO.NET。

### II. 单选题

1. 接口 `IEnumerable` 和 `IEnumerable<T>` 之间的区别在于，前者主要用于 ____，而后者用于 _____

   a. 非泛型集合，泛型集合

   b. 泛型集合，非泛型集合

   c. 所有集合，部分集合

   d. .NET Framework 2.0, .NET Framework 3.5

2. LINQ 查询中使用的变量包含 _____

   a. 查询信息和查询结果

   b. 查询信息

   c. 查询结果

   d. 标准查询运算符

### 语言集成查询 (LINQ) 简介

3. 所有标准查询运算符 SQO 方法都定义为 ________。这意味着方法既可以作为类方法调用，也可以作为实例方法调用

   a. 类方法

   b. 实例方法

   c. 变量方法

   d. 扩展方法

4. SQO 方法之一的 `AsEnumerable()` 运算符方法用于将对象的数据类型从 ________ 转换为 ________

   a. Iterable<T>, IEnumerable<T>

   b. IEnumerable<T>, IEnumerable<T>

   c. Any, IEnumerable<T>

   d. 以上都是

5. LINQ to Objects 用于查询任何显式或隐式具有 ________ 序列或 ________ 集合的序列或集合

   a. Iterable, IQueryable<T>

   b. IEnumerable<T>, IEnumerable<T>

   c. 延迟 SQO，非延迟 SQO

   d. 泛型，非泛型

6. LINQ to DataSet 构建在 ________ 架构之上，使用该版本 ADO.NET 开发的代码在 LINQ to DataSet 应用程序中无需修改即可运行

   a. ADO.NET 2.0

   b. ADO.NET 3.0

   c. ADO.NET 3.5

   d. ADO.NET 4.0

7. 有两个流行的 LINQ to SQL 工具，以及 ________ 被广泛用于使用 LINQ to SQL 的应用程序开发

   a. 实体数据模型，实体数据模型设计器

   b. IEnumerable<T>, IEnumerable<T>

   c. SQL.Metal，对象关系设计器

   d. IQueryable, IQueryable<T>

8. LINQ 查询在实现了 ________ 接口的类上执行。由于 ________带有额外的组件，因此 LINQ to SQL 查询具有额外的运算符

   a. IEnumerable<T>, IEnumerable<T>, IQueryable<T>

   b. IEnumerable<T>, IQueryable<T>, IQueryable<T>

   c. IQueryable<T>, IEnumerable<T>, IQueryable<T>

   d. IQueryable<T>, IQueryable<T>, IEnumerable<T>

9. LINQ to Entities 在 ________ 和 ________ 的控制下执行

   a. .NET Framework 3.5, ADO.NET 3.5

   b. ADO.NET 3.5 Entity Framework, ADO.NET 3.5 Entity Framework Tools

   c. IEnumerable<T>, IEnumerable<T>

   d. 实体数据模型，实体数据模型设计器

10. 为了访问和实现 ADO.NET 3.5 EF 和 ADO.NET 3.5 EFT，开发者需要理解 ________，它是 ADO.NET 3.5 EF 的核心

    a. SQL.Metal

    b. 对象关系设计器

    c. 泛型集合

    d. 实体数据模型

11. Lambda 表达式（由 __________ 表示）是一种许多方面与 ________ 相似的语言特征

    a. =>, 标准查询运算符

    b. =>, 匿名

    c. =>, 泛型集合

    d. =>, IQueryable

12. 扩展方法被定义为可以作为 __________ 或 __________ 方法调用

    a. 类，实例

    b. IEnumerable<T>, IQueryable<T>

    c. 泛型，非泛型

    d. 静态，动态

13. 在 LINQ 查询中，数据类型 `var` 用于定义 ________，变量的实际数据类型可以通过 __________ 时间进行推断

    a. 泛型变量，调试器

    b. 隐式类型局部变量，编译器

    c. 非泛型变量，构建器

    d. IEnumerable<T>,加载器

14. 在 LINQ 查询中，查询表达式必须以 __________ 子句开始，并以 __________ 子句结束

    a. begin, select, end

    b. select, order by

    c. from, select, group

    d. 查询变量,范围循环

15. DataContext 是一个用于在项目和数据库之间建立 __________ 的类。除了此角色外，DataContext 还提供了 __________ 可在运行的标准查询运算符操作的功能

    a. 关系，执行

    b. 引用，翻译

    c. 泛型集合，转换

    d. 连接，转换

### III. 练习题

1. 解释 LINQ 的架构和组件，并使用框图说明其功能。

2. 使用 `foreach` 解释 LINQ 查询的执行过程。

3. 解释标准查询运算符的功能。

4. 解释 LINQ 查询与标准查询运算符之间的关系。

5. 解释 `IEnumerable<T>` 和 `IQueryable<T>` 的定义和功能。

6. 使用示例执行 LINQ to SQL。

```csharp
List<string> fruits = new List<string> { "apple", "banana", "mango", "orange", "strawberry" };

var query = from fruit in fruits
    where fruit.Length < 6
    select fruit;
Console.WriteLine(query);
```

7. 使用查询语法表示的 LINQ 查询如图 4.6 所示。

8. 使用对象关系设计器通过 DataContext 创建每个实体的过程。

9. 解释扩展方法和实例方法之间的区别，并尝试使用 DataContext。

10. 列出执行 LINQ to DataSet 的三个步骤。

![](img/d59a47501d0a20fc0460a9c46cfb7_202)

# 5 使用 Visual C# 进行数据选择查询
