

关于 FOR XML 查询的一个注意事项是，所有数据（XML 文本）必须通过一个包含单行单列且列名为 XML_F52E2B61-18A1-11d1-B105-00805F49916B 的结果集返回。前面代码片段的输出演示了这一注意事项（其中 . . . 表示出于简洁原因未显示的类似数据）：

```
<NewDataSet>
  <Table>
    <XML_F52E2B61-18A1-11d1-B105-00805F49916B>
      /&lt;row ShipperID="1" CompanyName="Speedy Express"
      Phone="(503) 555-9831"/&gt;
      ...
    </XML_F52E2B61-18A1-11d1-B105-00805F49916B>
  </Table>
</NewDataSet>
```

返回的单行单列的值看起来像是 XML，但它包含 /&lt; 而不是小于号，且包含 /&gt; 而不是大于号。符号 < 和 > 不能出现在 XML 数据内部，因此必须进行实体编码——即表示为 /&gt; 和 /&lt;。元素 <XML_F52E2B61-18A1-11d1-B105-00805F49916B> 中返回的数据不是 XML，而是包含在 XML 文档中的数据。

要充分利用 FOR XML 查询，数据必须作为 XML 可访问。解决这一难题的方法是 SQLCommand 类的 ExecuteXmlReader 方法。当调用此方法时，SQLCommand 对象假定其作为 FOR XML 查询执行，并将此查询的结果作为 XmlReader 对象返回。示例如下：

```
Dim connection As New _
    SqlConnection("SERVER=localhost;Integrated Security=True;Database=Northwind;")
Dim command As New _
    SqlCommand("SELECT ShipperID, CompanyName, Phone " &
        "FROM Shippers FOR XML RAW")
Dim memStream As MemoryStream = New MemoryStream
Dim xmlReader As New XmlTextReader(memStream)
connection.Open()
command.Connection = connection
xmlReader = command.ExecuteXmlReader()
' Extract results from XMLReader
```

需要为此示例导入 System.Data.SqlClient 命名空间。

此代码中创建的 XmlReader 为 XmlTextReader 类型，其派生自 XmlReader。XmlTextReader 由 MemoryStream 支持；因此，它是可使用 XmlTextReader 暴露的方法和属性遍历的 XML 内存流。流式 XML 生成和检索已在第 9 章中讨论。

使用 SQLCommand 类的 ExecuteXmlReader 方法，可以检索 FOR XML 查询的结果。使 FOR XML 样式查询如此强大的原因在于它可以配置检索的数据。三种 FOR XML 查询支持以下形式的 XML 自定义：

+   FOR XML RAW — 此类型查询将结果集的每一行返回到名为 <row> 的 XML 元素中。检索到的数据作为 <row> 元素的属性包含。属性以 FOR XML RAW 查询中的列名或列别名命名。

+   FOR XML AUTO — 默认情况下，此类型查询将结果集的每一行返回到以 FOR XML AUTO 查询中包含的表或表别名命名的 XML 元素中。检索到的数据作为此元素的属性包含。属性以 FOR XML AUTO 查询中的列名或列别名命名。通过指定 FOR XML AUTO, ELEMENTS，可以检索所有数据在元素内部，而非属性内部。所有检索到的数据必须以属性或元素形式存在。没有混用的能力。

FOR XML EXPLICIT — FOR XML 查询的此形式使可以指定返回的每个列的确切 XML 类型。与列关联的数据可以作为属性或元素返回。可以将特定 XML 类型，如 CDATA 和 ID，与返回的列关联。甚至可以使用 FOR XML EXPLICIT 查询指定数据在 XML 层次结构中的层级。此样式的查询实现起来相当复杂。

FOR XML 查询具有灵活性。使用 FOR XML EXPLICIT，可以生成任何形式的 XML 标准。需要做出的决定是 XML 配置发生的位置。使用 Visual Basic，开发人员可以使用 XmlTextReader 和 XmlTextWriter 创建任何样式的 XML 文档。使用 XSLT 语言和 XSLT 文件，可以实现同等水平的配置。SQL Server 特别是 FOR XML EXPLICIT，使同等水平的 XML 自定义成为可能，但此自定义在 SQL 级别进行，甚至可以配置为存储过程调用。在这三种选项之间做出选择应基于您对所涉及三种语言的相对熟悉程度。即，使用 FOR XML EXPLICIT 查询对于喜欢在 T-SQL 中工作的用户来说是很好的选择，而其他偏好 XSLT 或 Visual Basic 的用户会选择这些工具。

## SQL SERVER 中的 CLR 集成

随着 Microsoft 开发部门在 .NET Framework 和 Visual Basic 上工作，SQL Server 内的其他团队也在新版本的 SQL Server 上工作。SQL 团队希望利用 .NET Framework，因此他们着手将通用语言运行时（CLR）集成到 SQL Server 2005 中。这种集成意味着开发人员可以在 SQL Server 的上下文中使用 Visual Basic 代码。作为 DBA 的成功并不取决于只知道 T-SQL。此外，复杂的访问数据代码不必在数据库外部编写。对开发人员和 DBA 来说的好处是，在选择开发语言时有更大的灵活性，以及数据库编程的更多功能。

SQL Server 中默认禁用 CLR 集成。这是安全措施，因为大多数用户不需要它提供的功能。不启用它意味着黑客攻击的途径更少。为了启用使用 Visual Basic 创建 SQL 对象，需要启用集成。这是通过在 SQL Server Management Studio 控制台的查询窗口中执行以下 SQL 语句完成的：

```
sp_configure 'clr enabled', 1
GO
RECONFIGURE WITH OVERRIDE
GO
```

这不是一个轻率的决定。启用任何功能意味着黑客也可能获得该功能，如果像 CLR 集成这样强大的功能被攻破，您的服务器可能成为危险的工具。然而，.NET Framework 可用功能的范围有限。

现在你可能已经被吓得不想启用 CLR 集成了，请注意在某些情况下它是一个非常有用的工具。T-SQL 尽管功能强大，但与 Visual Basic 相比仍是一个相对有限的语言。它缺乏开发人员习惯的条件或循环结构，如 WITH 语句。此外，调试传统上在 T-SQL 中相当薄弱。最后，在 T-SQL 中使用外部库的能力有限。你可以通过在适当时使用 Visual Basic 替换 T-SQL 来规避这些限制。

## 在 T-SQL 和 Visual Basic 之间做出选择

一旦你为数据库启用了 CLR 集成，你的下一个决策集围绕着何时使用 T-SQL 和 SQL Server 的原生服务，以及何时使用 Visual Basic 和 .NET Framework。最终的选择应基于应用程序的需求，而不是因为技术新颖或有趣。表 12-2 概述了一些常见的应用程序构建场景以及哪种选项最合适。

## 表 12-2：使用 T-SQL 与 Visual Basic

| SCENARIO | T-SQL | VISUAL BASIC |
|---|---|---|
| 用户定义类型（UDT） | 通常应为首选，如果不是唯一选择 | 如果需要与其它托管代码集成，或 UDT 需要提供额外方法时可以使用。 如果 UDT 将与外部 Visual Basic 代码共享，也是个好主意。 |
| 函数和存储过程 | 如果代码要批量处理数据，或使用少量过程代码时使用 | 如果代码需要大量过程处理或计算，或需要访问外部库，如 .NET Framework 时使用 |
| 扩展存储过程 | 通常是为 SQL Server 提供新功能的主要方法。例如，`xp_sendmail` 过程使从 T-SQL 发送电子邮件成为可能。一般应避免扩展存储过程，而应以托管代码创建过程。这部分是由于创建安全扩展过程的复杂性，但主要是因为它们可能从 SQL Server 的未来版本中移除。 | 如果需要访问外部代码或库，如 .NET Framework 时使用。根据需要，代码可能仅限于在 SQL Server 上下文中工作，也可能访问外部资源，如网络服务。更好的内存管理和安全性使 Visual Basic 成为创建这些扩展存储过程的更好选择。 |
| 代码位置 | T-SQL 代码只能存在于 SQL Server 内部。这使得查询优化成为可能。 | Visual Basic 代码可能存在于 SQL Server 内部或客户端。这可能意味着你可以从客户端获取代码并改编为在 SQL Server 中运行。在这种情况下，代码更接近数据，通常会提高性能。此外，运行 SQL Server 的硬件通常比普通桌面性能更好，这又意味着代码会执行得更快。 |
| Web 服务 | T-SQL 支持创建 Web 服务，使任何函数或存储过程通过 SOAP 可用。 | 用 Visual Basic 编写的函数和存储过程可以从 SQL Server 暴露为 Web 服务。对 XML 处理和过程逻辑的更好支持可能意味着在 Visual Basic 中创建这些 Web 服务更容易。 |
| XML 处理 | T-SQL 已扩展以提供读取和写入 XML 的一些能力。这些扩展仅提供将 XML 作为整体工作的能力。 | 提供出色的 XML 处理，既可用于将文档作为整体工作，也可通过流式 API 工作。一般来说，如果你需要做大量 XML 处理，使用 Visual Basic 会让你的生活更轻松。 |

## 创建用户定义类型

SQL Server 的一个功能通常没有得到应有的关注，那就是创建用户定义类型（UDT）的能力。这使开发人员能够定义可用于列、函数、存储过程等中的新数据类型。它们可以通过对值应用特定约束，或仅仅为了更好地识别列的意图，使数据库开发更容易。例如，当面对包含数据类型为 `varchar(11)` 的列的表时，你可能仍不确定该值的用途；但如果该列的类型改为 `ssn`，你就会认识到（如果你在美国）这是一个社会安全号码。

