
图 4.49 的 D 部分显示了这种情况。这是一种非常高效的技术，极其重要，因为它是构建 XML 树最常见的场景。要将 `mobilePhone` 添加到另一个 `faculty`（例如 `faculty2`），请参考图 4.49 E 部分所示的代码。同样，`LINQ to XML` 会检查子节点是否已有了父节点。在这种情况下，子节点已经有了父节点。如果子节点已有父节点，`LINQ` 会在后续父节点上克隆该子元素。这种情况可以通过图 4.49 F 部分所示的代码来说明。

## 4.8.2.3 更新 XML

要更新 XML，你可以导航到想要替换内容的 `XElement`，然后使用 `ReplaceNodes()` 方法。例如，如果你想更改 `faculty` 第第一个 `XElement` 的电话号码，可以执行图 4.50 A 部分所示的代码。

`SetElement()` 方法设计用于处理简单内容。通过 `SetElement()`，你可以对元素进行操作。例如，我们可以使用图 4.50 B 部分所示的代码对演示的第一个电话号码进行更新。

结果将是相同的。如果没有任何电话号码，会在 `faculty` 下添加一个名为 `"phone"` 的 `XElement`。例如，你可能想为 `faculty` 添加一个办公室。如果办公室不存在，你可以插入它。这种情况如图 4.50 C 部分所示。

```csharp
A faculty.Element("phone").ReplaceNodes("750-555-0155");
```

```csharp
B faculty.SetElement("phone", "750-555-0155");
```

```csharp
C faculty.SetElement("office", "MTC-119");
```

```csharp
D faculty.SetElement("office", null);
```

# 使用 C# 进行 SQL Server 数据库编程

```csharp
faculty.Element("phone").Remove();
faculty.Elements("phone").Remove();
faculties.Element("faculty").Element("office").RemoveNodes(); faculty.SetElement("phone", null);
```

图 4.51 使用 `LINQ to XML` 删除 XML 的一些示例代码。

属性具有一个对称的方法调用 `SetAttribute()`，其功能与 `SetElement()` 类似。

## 4.8.2 删除 XML

要删除元素，请导航到要删除的内容所在并调用 `Remove()` 方法。例如，如果你想删除某个系系的第一个电话号码，请输入图 4.51 节 A 所示的代码。

`Remove()` 方法也适用于 `IEnumerable`，你可以在一次调用中删除系系的所有电话号码，如图 4.51节 B 所示。

你也可以通过使用 `RemoveNodes()` 方法删除 `XElement` 的内容。例如，你可以删除系系的第一个办公室的内容，如图 4.51节 C 所示。

另一种删除元素的方法是将其设置为 `null`，使用我们在上一节中讨论过的 `SetElement()` 方法。示例如图 4.51 节 D 所示。

## 4.8.3 操作 XML 属性

操作 `XElement` 和 `XAttribute` 类之间存在大量的对称性。然而，在 `LINQ to XML` 层次中，`XElement` 和 `XAttribute` 是不同的，并且没有派自公共基类。这是因为 XML 属性不是 XML 树中的节点；它们是与 XML 元素的无序键值对。`LINQ to XML` 区分了这种区别；在实践中，由于 XML 属性的性质，与操作 `XElement` 非常相似。

### 4.8.3.1 添加 XML 属性

添加 `XAttribute` 与添加简单的 `XElement` 非常相似。在 4.52 所示的 XML 中，注意每个电话号码都有一个类型属性，状态为 `home` 或 `work`。

你可以使用函数构造创建 `XAttribute`，方法与创建简单的 `XElement` 相同。要使用函数构造创建一个系系，请输入图 4.53 所示的代码。

正如你使用 `SetElement()` 方法更新、添加或删除简单类型一样，你也可以使用 `XElement` 上的 `SetAttribute(XName, object)` 方法。如果属性存在，它将被更新；如果不存在，则将被添加。

```xml
<faculties>
  <faculty>
    <faculty_name>Patrick Tones</faculty_name>
    <phone type="home">750-555-0144</phone>
    <phone type="work">750-555-0145</phone>
  </faculty>
</faculties>
```

图 4.52 XML 属性。

语言集成查询 (`LINQ`) 简介

```csharp
XElement faculty = new XElement("faculty",
    new XElement("faculty_name", "Patrick Tones"),
    new XElement("phone",
        new XAttribute("type", "home"),
        "750-555-0144"),
    new XElement("phone",
        new XAttribute("type", "work"),
        "750-555-0145"));
```

图 4.53 创建 `XAttribute` 的示例代码。

## 4.8.3.2 获取 XML 属性

访问 `XAttribute` 的主要方法是在 `XElement` 上使用 `Attribute(XName)` 方法。例如，为了使用类型属性获取联系人的家庭电话号码，可以使用图 4.54 节 A 所示的代码。

注意 `Attribute(XName)` 方法的工作类似于 `Element(XName)` 方法。此外，注意存在显式转换运算符，它允许 `XAttribute` 转换为各种简单类型。

## 4.8.3.3 删除 XML 属性

如果你想删除属性，可以使用 `Remove()` 或 `SetAttribute(XName, object)` 方法，将 `null` 作为值。例如，使用 `Remove()` 方法删除第一个电话的属性，使用图 4.54 节 B 所示的代码。

或者，你可以使用带有 `null` 参数的 `SetAttribute()` 方法执行删除操作。示例如图 4.54 节 C 所示。

我们对操作 XML 元素的基本组件进行了详细讨论，现在让我们深入了解使用 `LINQ` 查询 XML。

## 4.8.4 使用 LINQ 查询 XML

`LINQ to XML` 与其他内存 XML 编程 API 的主要区别是语言集成查询 (`LINQ`)。`LINQ` 在不同数据模型之间提供了一致的查询体验，并在单个查询中混合匹配数据模型的能力。本节描述了如何使用语言集成查询处理 XML。下一节包含了跨数据模型使用语言集成查询的一些示例。

标准查询运算符对 `IEnumerable<T>` 执行完整查询。标准查询运算符暴露了 `IEnumerable<T>` 对象的方法，并由任何其他方法调用。这种调用方法的方法被称为显式点符号。

图 4.54 获取和删除 `XAttribute` 的示例代码。

除了标准查询运算符外，还有五个常用查询运算符的查询表达式：

- `Where`
- `Select`
- `SelectMany`
- `OrderBy`
- `GroupBy`

查询表达式在显式点符号之上提供了一个易于使用的层，类似于 `foreach` 是一种由调用 `GetEnumerator()` 和循环组成的易于使用的机制。在处理 XML 时，你可能会发现这两种方法都有用。点符号的指导将给你 XML 语言集成查询背后的原理，并帮助你理解查询表达式如何简化问题。

`LINQ to XML` 与语言集成查询的集成体现在三个方面：
1) 利用标准查询运算符
2) 使用 XML 查询扩展
3) 使用 XML 转换

第一个对于任何启用语言集成查询的数据访问技术都是常见的，并有助于一致的查询体验。后两个是 XML 特有的查询和转换功能。

### 4.8.4.1 标准查询运算符和 XML

`LINQ to XML` 以一致的方式充分利用标准查询运算符映射实现 `IEnumerable` 接口的集合。我们在第 4.1 节中详细讨论了标准查询运算符。

# 使用 C# 进行 SQL Server 编程

```xml
A from in faculties.Elements("faculty")
where (string) f.Element("office") == "MTC-3,*"
orderby (string) f.Element("faculty_name")
select (string) f.Element("faculty_name");
```

```xml
B from in faculties.Elements("faculty"), p in faculties.Elements("phone")
where (string) f.Element("faculty_id") == "B"&& p.Value.StartsWith("750")
orderby (string) f.Element("faculty_name")
select f;
```

```xml
C from in students.Elements("student"), average = students.Elements("student")
Average(x) => (int) x.Element("gpa")
where (int) s.Element("gpa") > average
select s;
```

**图 4.57** 使用 XML 执行查询的示例代码。

图 4.57 中 A 部分所示的查询根据 `faculty_name` 获取所有系所有的办公室，并将它们作为字符串返回（该查询的结果为 `IEnumerable<string>`）。

图 4.57 中 B 部分所示的查询获取所有 `faculty_id` 以 B 开头且代码为 750 的系成员，并按 `faculty_name` 排序。该查询的结果为 `IEnumerable<XElement>`。

图 4.57 中 C 部分显示的另一个示例获取 GPA 大于平均 GPA 的学生。

## 4.8.4.4 在 LINQ to XML 中使用 XPath 和 XSLT

`LINQ to XML` 支持一组“桥接类”，允许其与 `System` 命名空间中的现有功能协同工作，包括 `XPath` 和 `XSLT`。需要注意的是，`System.Xml` 在 "Oras" 中提供了这些规范的 1.0 版本。

通过在每个项目的代码窗口的命名空间声明部分添加此命名空间 `using System.Xml.XPath;` 来引用命名空间，即可启用支持 `XPath` 的扩展方法。

这引入了用于创建 Navigator 对象的 `Navigator` 重载、用于评估 XPath 表达式的 `XPathEvaluate` 重载，以及工作类似于 `System.Xml` API 中的 `SingleNode` 和 `XPathSelectNodes` 类似的 `XPathSelectElement` 重载。与 DOM 一样，必须传入一个 `Resolver` 对象。例如，要显示所有名为 `"phone"` 的元素，可以编写以下代码：

```csharp
foreach (var phone in faculties.XPathSelectElements("phone"))
    Console.WriteLine(phone);
```

同样，通过在每个项目的代码窗口上输入 `using System.Xml` 命名空间声明来启用 `Xsl`。这允许你使用 `XDocument` 方法创建 `Navigator` 并将其传递给 `Transform()`。

## 4.8.4.5 混合 LINQ 和其他数据模型

`LINQ` 通过标准查询操作符和下一节将讨论的 Lambda 表达式，为跨数据源提供了一致的查询体验。它还提供了在单个查询中匹配启用 `LINQ` 的数据模型的能力，这通过使用我们的 `CSE_DEPT` 数据库，提供了一个关系数据与 XML 两种常见场景的简单示例。

### 4.8.4.5.1 从数据库读取数据到 XML

图 4.58 显示了一个简单的示例，从 `CSE_DEPT` 数据库（使用 `LINQ to SQL`）读取以获取表中的系，然后将它们转换为 XML。

### 4.8.4.5.2 读取 XML 并更新数据库

你也可以读取 XML 并将信息放入数据库。对于此示例，假设你正在获取一组 XML 格式的系成员。为了简单起见，更新记录仅包含更改。首先，让我们创建一个示例 XML，如图 4.59 所示。要完成此更新，你查询每个元素并调用数据库用该数字更新相应的列。实现此功能的示例代码在图 4.60 中。

```csharp
Element Faculties = new XElement("Elements",
from f in db.Faculties
where f.faculty_id == ""
select new Element("Faculty",
new XAttribute("facultyName", f.name),
new XElement("Office", f.office),
new XElement("Title", f.title),
new XElement("Phone", f.phone),
new XElement("Email", f.email)));
Console.WriteLine(Faculties);
```

**图 4.58** 使用 XML 执行查询的示例代码。

```csharp
foreach (var phone in faculties.Elements("faculty"))
{
  Element faculty = db.Faculties.First(f=>f.faculty_id == (string)f.Element("faculty_id"));
  faculty.Phone = (string)f.Element("phone");
}
db.SubmitChanges();
```

**图 4.59** 示例 XML。

**图 4.60** 读取和更新数据库的示例代码。

# 使用 C# 进行 SQL Server 编程

到此时，我们已经完成了对 `LINQ to XML` 的讨论。接下来，我们将更仔细查看 C# 3.0 对 `LINQ` 的语言增强。

## 4.9 C# 3.0 语言增强

与 C# 2.0 相比，C# 3.0 增加了大量的增强，以类型安全的方式支持数据查询；这些增强主要是为了支持语言集成查询 (`LINQ`)。

C# 3.0 引入了几个基于 C# 2.0 的语言扩展，以支持高阶、函数式类库的创建和使用。这些扩展能够构建具有与关系数据库和 XML 查询语言等表达能力的组合式 API。

除了通用的 `LINQ` 主题外，还对 C# 3.0 进行了特殊的改进。这些改进的主要组件包括：
- Lambda 表达式
- 扩展方法
- 隐式类型局部变量
- 查询表达式

让我们逐一详细讨论这些主题。

### 4.9.1 Lambda 表达式

Lambda 表达式在许多方面与匿名方法相似的特征。如果 Lambda 表达式先开发并实现到语言中，那么就不需要匿名方法了。使用 Lambda 表达式的基本思想是你可以将代码视为数据。在 C# 的早期版本中（如 C# 1.0），向方法传递字符串、引用类型等是非常常见的，以便方法可以处理这些值。匿名方法和 Lambda 表达式将值的范围扩展到了代码块。这个概念在函数式编程中很常见。

Lambda 表达式的语法 (`=>`) 后面跟着一个表达式、逗号分隔的参数列表以及语句。对于更复杂的 Lambda 表达式，语句块后面可以跟着 Lambda 运算符。C# 中使用 Lambda 表达式的一个简单示例如下：

```csharp
x => y
```

其中 Lambda 运算符左侧的 `x` 是输入参数，Lambda 运算符右侧的 `y` 是输出参数。输入和输出参数的数据类型应该由委托 显式指示。因此，Lambda 表达式与委托 紧密相关。这个 Lambda 表达式可以读为输入和输出。这种简单 Lambda 表达式的语法可以写为：

```csharp
(param1, param2, ...) => output
```

应该使用括号覆盖所有的输入参数。对于更复杂的 Lambda 表达式，应该采用语句块。这种语法的示例如下所示：

```csharp
(x, y) => { if (x > y) return x; else return y; }
```

# 166 使用 C# 进行 SQL Server 数据库编程

```csharp
public static class Conversion
{
    public static string ConvertToUpper(string input)
    {
        return input.ToUpper();
    }
    public static string ConvertToLower(string input)
    {
        return input.ToLower();
    }
}
```

**图 4.61** 实例方法 `ConvertToUpper` 的示例。
