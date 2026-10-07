

# 154 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_182_0.png)

图 4.45 LINQ to XML 类层次结构。

## 4.8.1 LINQ to XML 类层次结构

首先，让我们对图 4.45 显示的 LINQ to XML 类层次结构有一个整体概念。观察此类层次时，应该注意以下几点：

- 1. XElement 位于类层次结构的底端，它是 LINQ to XML 的基础类。XML 树通常由 XElement 树组成。XAttributes 是与 XElement 关联的键/值对。XDocuments 只在需要时才创建，例如用于持有 DFT 或顶层 XML 处理指令（ProcessingInstruction）。所有其他 XNodes 都可以是 XElement 下的叶子节点，或者可能是 XDocument（如果它们存在于根节点）。
- 2. XAttribute 和 XNode 派生自公共基类 XObject。XAttributes 不是 XNodes，因为 XML 属性实际上是与 XML 元素关联的键值对，而不是 XML 树中的节点。这与 W3C DOM 有不同。
- 3. Text 和 XData 在此版本的 LINQ to XML 中被暴露，但如上所述，除非需要显示文本，否则最好将它们视为一种半隐藏的实现。作为用户，你可以将元素或属性内的文本值作为字符串或其他简单值取回。
- 4. 唯一可以拥有子节点的节点是 XContainer，这意味着 XDocument 或 XElement。XDocument 可以包含一个 XElement（根元素）、一个 XDeclaration（声明）或一个 ProcessingInstruction（处理指令）。XElement 可以包含另一个 XElement、一个 Attribute（属性）以及文本（多种格式传递，但在 XML 树中表示为文本）。

除了此类层次结构外，在 XML 中对齐的其他组件在 LINQ to XML 中也起着关键作用。其中之一就是 XML 名称。

XML 名称在 XML 编程 API 中通常是一个复杂的课题，但在 LINQ to XML 中表示非常简单。XML 名称由 XNamespace 对象（封装了 XML 命名空间 URI）和本地名称表示。XML 命名空间的作用与你在基于 .NET Framework 的程序中使用的命名空间相同，允许你唯一地限定类名称。这确保了你不会与其他用户或内置名称发生命名冲突。当你识别了 XML 命名空间后，可以选择一个仅在你识别的命名空间内唯一的本地名称。

## 语言集成查询 (LINQ) 简介

```c
XElement faculties = new XElement("faculties",
    new XElement("faculty",
    new XElement("faculty_name", "Patrick Tones"),
    new XElement("phone", "750-378-0144"),
    new XElement("title", "Associate Professor"),
    new XElement("office", "MTC-387"),
    new XElement("college", "Main University"),
    new XElement("email", "ptones@college.edu"),
    new XElement("faculty_id", "PS8042"))
```

**图 4.46** 使用 LINQ to XML 的示例 XElement 文件。

## 4.8.2 操作 XML 元素

LINQ to XML 提供了一组操作 XML 的方法。你可以插入、删除、复制和更新 XML。在我们继续讨论这些操作之前，首先我们需要向你展示如何使用 LINQ to XML 创建一个示例 XElement 文件。

### 4.8.2.1 从头开始创建 XElement

LINQ to XML 提供了一种创建 XML 元素的强大方法。这被称为函数式构造（functional construction）。函数式构造允许你在单个语句中创建 XML 树的全部或部分。例如，要创建 facultiesElement，可以使用图 4.46 所示的代码。

通过缩进，XElement 构造函数代表了底层 XML 的结构。函数式构造通过接受 `params object` 的 XElement 构造函数启用。函数式构造的示例所示：

```csharp
public XElement(XName faculty_name, params object[] contents)
```

contents 非常灵活，支持任何类型的对象作为 XElement 的合法子节点。参数可以是：
- 字符串：作为文本添加。这是将字符串作为元素值的推荐方法；LINQ to XML 实现将创建 XText 节点。
- XText：可以是字符串或 CData 值，作为子内容添加。这对于 CData 值更为简单。
- XElement：作为子元素添加。
- XAttribute：作为属性添加。
- ProcessingInstruction：作为子内容添加。
- Enumerable：被枚举，且这些值被递归应用。
- 其他任何内容：调用 ToString() 结果作为文本添加。

CDATA 术语意味着字符数据，用于不同的 SGML 和 XML 语言。该术语表示文档的某部分是字符数据而非非字符数据。

在上面的函数式构造示例中，字符串 ("Patrick Tones") 被传递给 faculty_name XElement 构造函数。这可能是一个变量（例如 `new XElement("faculty_name", facultyName)`），也可能是字符串以外的不同类型（例如 `new XElement("quantity", 55)`），并且可能是图 4.47 所示函数调的结果。

```csharp
class Person
{
  public string faculty_name;
  public string[] PhoneNumbers;
}

var persons = new[] {
  new Person { faculty_name = "Patrick Tones", PhoneNumbers = new[] { "750-378-0144", "750-055-0145" },
  new Person { faculty_name = "Gretchen Rivas", PhoneNumbers = new[] { "755-055-0163" }
};

XElement faculties = new XElement("faculties",
    from f in persons
    select XElement("faculty", f.faculty_name,
        from p in f.PhoneNumbers
        select XElement("phone", p)));
Console.WriteLine(faculties);
```

图 4.47 函数式构造示例。

```csharp
{
  ...
  XElement qty = new XElement("quantity", GetQuantity());
  public int GetQuantity() { return 55; }
}
```

一个使用 LINQ to XML 的示例查询。

## 4.8.2.2 插入 XML

你可以轻松地向 XML 树添加内容。要添加另一个 XElement，可以使用图 4.49 A 部分所示的 Add() 方法。此片段会将 mobilePhone 作为 faculty 的最后一个。如果你想添加到子节点的开头，可以使用 AddFirst()。如果你想在特定位置添加子节点，可以使用 AddBefore(Self) 或 AddAfter(Self) 导航到目标位置之前的子节点。例如，如果你想让 mobile 作为第二个电话，可以执行图 4.49 B 部分所示的代码。

让我们深入看看当你创建一个 XElement 且它没有父节点时的幕后机制。如果访问你的属性，你将得到 null，如图 4.49 C 部分所示。当你使用 Add() 方法将此子节点添加到父节点时，LINQ to XML 会检查该元素是否没有父节点，因此 LINQ to XML 通过将子元素的 Parent 属性设置为调用 Add() 的 XElement 来赋予父节点。

```csharp
A XElement mobilePhone = new XElement("phone", "750-555-0168");
faculty.Add(mobilePhone);
```

```csharp
B XElement mobilePhone = new XElement("phone", "750-555-0168");
XElement firstPhone = faculty.Element("phone");
firstPhone.AfterSelf(mobilePhone);
```

```csharp
C XElement mobilePhone = new XElement("phone", "750-555-0168");
Console.WriteLine(mobilePhone.Parent);
// 将输出 null
```

```csharp
D faculty.Add(mobilePhone);
Console.WriteLine(mobilePhone.Parent);
// 将输出 faculty
```

```csharp
E faculty2.Add(new XElement(mobilePhone));
```

```csharp
F faculty2.Add(new XElement(mobilePhone));
```

图 4.49 使用 LINQ to XML 插入 XML 的一些代码。

图 4.49 的 D 部分显示了这种情况。这是一种非常高效的技术，极其重要，因为它是构建 XML 树最常见的场景。要将 mobilePhone 添加到另一个 faculty（例如 faculty2），请参考图 4.49 E 部分所示的代码。同样，LINQ to XML 会检查子节点是否已有了父节点。在这种情况下，子节点已经有了父节点。如果子节点已有父节点，LINQ 会在后续父节点上克隆该子元素。这种情况可以通过图 4.49 F 部分所示的代码来说明。

## 4.8.2.3 更新 XML

要更新 XML，你可以导航到想要替换内容的 XElement，然后使用 ReplaceNodes() 方法。例如，如果你想更改 faculty 第第一个 XElement 的电话号码，可以执行图 4.50 A 部分所示的代码。

SetElement() 方法设计用于处理简单内容。通过 SetElement()，你可以对元素进行操作。例如，我们可以使用图 4.50 B 部分所示的代码对演示的第一个电话号码进行更新。

结果将是相同的。如果没有任何电话号码，会在 faculty 下添加一个名为 "phone" 的 XElement。例如，你可能想为 faculty 添加一个办公室。如果办公室不存在，你可以插入它。这种情况如图 4.50 C 部分所示。

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

