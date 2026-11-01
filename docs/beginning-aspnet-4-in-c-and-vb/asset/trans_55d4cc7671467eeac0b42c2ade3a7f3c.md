
```csharp
connection.Open();
var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
while (reader.Read())
{
    SqlXml xml = reader.GetSqlXml(2);
    var doc = new XmlDocument();
    doc.LoadXml(xml.Value);

    XmlNode examNode = doc.SelectSingleNode("//Exam");
    Console.WriteLine("Exam: {0}", examNode.Attributes["Number"].Value);
    XmlNode titleNode = examNode.SelectSingleNode("./Title");
    Console.WriteLine("Title: {0}", titleNode.InnerText);
    Console.Write("Course(s): ");

    foreach (XmlNode courseNode in examNode.SelectNodes("./Course"))
    {
        Console.Write("{0} ", courseNode.InnerText);
    }
    Console.WriteLine();
}
reader.Close();
```

代码片段 XmlSamples/Program.cs

> 第33章“操作XML”中讨论了 XmlReader 和 XmlDocument 类。

在 .NET 4 中，还有另一种从数据库访问 XML 列的方法。你可以将 LINQ to SQL 和 LINQ to XML 结合使用，这样可以使编程代码更简洁。

你可以从“数据”模板类别中选择“ADO.NET 实体数据模型”模板，使用 ADO.NET 实体框架设计器。将文件命名为 ExamsModel.edmx，以为 SqlServerSample 数据库创建映射。选择 Exams 表，并选择“将对象名称复数形式转换为单数”选项。使用向导创建模型后，将打开设计图面，如图 34-4 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1036_0.png)

图 34-4

设计器创建的数据上下文类名为 ExamsEntities，并定义了一个属性 Exams 用于返回所有考试行。这里使用 foreach 语句遍历所有记录。当然，如果并非需要所有记录，你也可以定义一个带 where 表达式的 LINQ 查询。Exam 类根据数据库表中的列定义了属性 Id、Number 和 Info。Info 属性的类型为 string。使用 XElement 类，可以通过命名空间 System.Xml.Linq 中的 LINQ to XML 类来解析和访问该字符串。调用 Element() 方法并传递 XML 元素 Exam 的名称，会返回一个 XElement 对象，然后使用该对象以更简单的方式访问 Number 属性和 Title、Course 元素的值，就像之前使用 XmlDocument 类那样：

```csharp
using System;
using System.Xml.Linq;

namespace Wrox.ProcSharp.SqlServer
{
    class Program
    {
        static void Main()
        {
            using (ExamsEntities data = new ExamsEntities())
            {
                foreach (Exam item in data.Exams)
                {
                    XElement exam = XElement.Parse(item.Info);
                    Console.WriteLine("Exam: {0}", exam.Attribute("Number").Value);
                    Console.WriteLine("Title: {0}", exam.Element("Title").Value);
                    Console.Write("Course(s): ");
                    foreach (var course in exam.Elements("Course"))
                    {
                        Console.Write("{0} ", course.Value);
                    }
                    Console.WriteLine();
                }
            }
        }
    }
}
```

ADO.NET 实体框架和 LINQ to XML 分别在第31章“ADO.NET 实体框架”和第33章“操作XML”中讲解。

## 查询数据

到目前为止，你还没有看到 XML 数据类型真正强大的功能。SQL SELECT 语句可以与 XML XQuery 结合使用。

下面展示了一个 SELECT 语句与 XQuery 表达式结合以读取 XML 值的示例：

```sql
SELECT [Id], [Number], [Info].query('/Exam/Course') AS Course FROM [Exams]
```

XQuery 表达式 /Exam/Course 访问作为 Exam 元素子元素的 Course 元素。该查询的结果返回 ID、考试编号和课程：

| Id | 编号 | 课程 |
|---:|:-------|:-------|
| 1 | 70-502 | `<Course>6460</Course>` |
| 2 | 70-562 | `<Course>2310</Course><Course>6463</Course>` |
| 3 | 70-561 | `<Course>2310</Course><Course>6464</Course>` |

使用 XQuery 表达式，你可以创建更复杂的语句来查询单元格 XML 内容中的数据。下一个示例将考试信息中的 XML 转换为列出课程信息的 XML：

```sql
SELECT [Info].query('
    for $course in /Exam/Course
    return
<Course>
    <Exam>{ data(/Exam[1]/@Number) }</Exam>
    <Number>{ data($course) }</Number>
</Course>')
AS Course
FROM [Exams]
WHERE Id=2
```

这里，仅用 `SELECT [Info] FROM Exams WHERE Id = 2` 选择单行。利用该 SQL 查询的结果，使用了 XQuery 表达式的 `for` 和 `return` 语句。`for $course in /Exam/Course` 遍历所有 Course 元素。`$course` 声明一个变量，每次迭代都会设置该变量（类似于 C# 的 foreach 语句）。在 `return` 语句之后，定义了每一行查询的结果。每个 Course 元素的结果都被 `<Course>` 元素包围。嵌入 `<Course>` 元素内部的是 `<Exam>` 和 `<Number>`。`<Exam>` 元素内的文本由 `data(/Exam[1]/@Number)` 定义。`data()` 是一个 XQuery 函数，返回参数指定节点的值。节点 `/Exam[1]` 用于访问第一个 `<Exam>` 元素；`@Number` 指定 XML 属性 `Number`。`<Number>` 元素内的文本由变量 `$course` 定义。

> 与 C# 不同，C# 中集合的第一个元素使用索引 0 访问，而在 XPath 中集合的第一个元素使用索引 1 访问。

此查询的结果如下所示：

```xml
<Course>
    <Exam>70-562</Exam>
    <Number>2310</Number>
</Course>
<Course>
    <Exam>70-562</Exam>
    <Number>6463</Number>
</Course>
```

你可以修改 XQuery 语句，添加 where 子句来筛选 XML 元素。以下示例仅当课程编号的值高于 2562 时，才从 XML 列返回课程：

```sql
SELECT [Info].query('
    for $Course in /Exam/Course
    where ($Course > 2562)
    return
    <Course>
        <Exam>{ data(/Exam[1]/@Number) }</Exam>
        <Number>{ data($Course) }</Number>
    </Course>')
AS [Course]
FROM [Exams]
WHERE Id=2
```

结果缩减为仅一个课程编号：

```xml
<Course>
    <Exam>70-562</Exam>
    <Number>6463</Number>
</Course>
```

SQL Server 中的 XQuery 允许使用其他几个 XQuery 函数来获取最小值、最大值或汇总值，处理字符串、数字，检查集合中的位置等。

下一个示例展示了使用 `count()` 函数获取 `/Exam/Course` 元素的数量：

```sql
SELECT [Id], [Number], [Info].query('
    count(/Exam/Course)')
    AS "Course Count"
FROM [Exams]
```

返回的数据显示每场考试的课程数量：

| Id | 编号 | 课程数量 |
|---:|:-------|-------------:|
| 1 | 70-502 | 1 |
| 2 | 70-562 | 2 |
| 3 | 70-561 | 2 |

## XML 数据修改语言（XML DML）

当微软在 SQL Server 2005 中实现 XQuery 时，按照 W3C（http://www.w3c.org）的定义，XQuery 只允许查询数据。由于 XQuery 的这一限制，微软定义了一个名为“XML 数据修改语言”（XML DML）的 XQuery 扩展。

> 如今，XQuery Update Facility 1.0 自 2009 年 6 月 9 日起成为候选推荐标准。该推荐标准由 IBM、Oracle 和 Red Hat 提出，与 XML DML 不同。

XML DML 使得可以通过以下 XQuery 扩展来修改 XML 数据：insert、delete 和 replace value of。

本节将介绍一些在单元格中插入、删除和修改 XML 内容的示例。

你可以使用 insert 关键字在 XML 列中插入一些 XML 内容，而无需替换整个 XML 单元格。这里，`<Course>2555</Course>` 作为第一个 Exam 元素的最后一个子元素被插入：

```sql
UPDATE [Exams]
SET [Info].modify('
    insert <Course>2555</Course> as last into Exam[1]')
WHERE [Id]=3
```

XML 内容可以使用 delete 关键字删除。在第一个 Exam 元素内，最后一个 Course 元素被删除。最后一个元素通过 `last()` 函数来选择：

```sql
UPDATE [Exams]
SET [Info].modify('
    delete /Exam[1]/Course[last()]')
FROM [Exams] WHERE [Id]=3
```

也可以更改 XML 内容。这里使用了关键字 `replace value of`。表达式 `/Exam/Course[text() = "6463"]` 仅访问文本内容包含字符串 6463 的 `Course` 子元素。对于这些元素，仅使用 `text()` 函数访问文本内容以进行替换。即使查询仅返回单个元素，仍然需要明确指定仅一个元素进行替换。这就是为什么显式使用 `[1]` 指定返回的第一个文本元素。2599 指定新的课程编号为 2599：

```sql
UPDATE [Exams]
SET [Info].modify('
    replace value of (/Exam/Course[text() = "6463"]/text())[1] with 2599')
FROM [Exams]
```

## XML 索引

如果经常在 XML 数据中搜索某些特定元素，可以在 XML 数据类型内指定索引。XML 索引必须区分为主 XML 索引类型和辅助 XML 索引类型。主 XML 索引是针对 XML 值的完整持久化表示创建的。

以下 SQL 命令 `CREATE PRIMARY XML INDEX` 在 Info 列上创建索引 idx_exams：

```sql
CREATE PRIMARY XML INDEX idx_exams on Exams (Info)
```

如果查询包含直接访问 XML 类型中的 XML 元素的 XPath 表达式，主索引将无济于事。对于 XPath 和 XQuery 表达式，可以使用 XML 辅助索引。如果创建 XML 辅助索引，则主索引必须已存在。对于辅助索引，必须区分以下索引类型：

- PATH 索引
- VALUE 索引
- PROPERTY 索引

如果使用了 `exists()` 或 `query()` 函数，并通过 XPath 表达式访问 XML 元素，则使用 PATH 索引。使用 XPath 表达式 `/Exam/Course` 时，创建 PATH 索引可能会很有用：

