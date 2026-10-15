
简单来说，你可以说你想要对数据执行的操作越复杂，使用 `LINQ to Objects` 而不是传统的迭代技术所获得的好处就越大。以下是使用 `LINQ to Objects` 需要了解的概念：

- `Strings`

- `Reflections`

- `File directories`

让我们详细讨论它们。

## Strings

`LINQ` 用于查询和转换字符串和字符串集合。它在文本文件中的半结构化数据中特别有用。你可以轻松地将 `LINQ` 查询与传统的字符串函数以及查询函数结合使用。在 `LINQ to Objects` 中，你可以轻松查询、分析和修改大型文本。你只需使用 `Split()` 方法将其拆分为较小的字符串。你可以将源文本拆分为单词、段落或任何其他标准，然后根据查询需要执行额外的拆分。你还可以在 `LINQ` 查询的 `where` 子句中使用 `IsMatch()` 方法。然后你可以使用 `LINQ` 查询来使用或修改你的正则表达式。

## Reflections

`.NET Framework` 类库使用反射的概念来检查 `.NET` 程序集中的元数据并创建类型和成员的集合。`LINQ` 中使用反射有助于检索与指定搜索条件匹配的方法的元数据。例如，你可以运行一个查询来检索程序集中返回可枚举类型（例如数组）的方法的名称。`System.Reflection` 命名空间用于在 `LINQ` 中使用反射。

## File Directories

`LINQ` 中的另一个附加功能是使用文件目录。你可以使用 `LINQ` 中的文件目录执行以下各种功能：

- 使用文件目录功能查找指定目录树中具有指定文件扩展名的所有文件。

- 对文件和文件夹列表执行高级分组和排序操作。

- 检索指定文件夹及其子文件夹中所有文件使用的总字节数。

- 比较两个文件夹的内容。你可以查询一个布尔值来指定两个文件是否相同。你也可以查询交集以检索两个文件夹中的文件。`FileComparer` 类用于执行这些文件目录功能。

- 使用 `FileInfo` 对象检索最大文件的大小（以字节为单位）。

- 查询在文件目录中以相同名称保存在多个位置的文件。

- 查询指定目录中所有文件的内容。

## 介绍 LINQ to ADO.NET

`LINQ to ADO.NET` 帮助你使用 `LINQ` 编程模型查询任何 `ADO.NET` 对象。它由两种独立的技术组成，`LINQ to DataSet` 和 `LINQ to SQL`。

`LINQ to ADO.NET` 的第一个组件是 `LINQ to DataSet`。该接口是对标准 `ADO.NET DataSet` 编程模型的一组扩展，允许对 `DataSet`、`DataTable` 和 `DataRow` 使用 `LINQ` 查询表达式。`LINQ to DataSet` 提供了对 `DataSet` 更丰富和优化的查询。

`LINQ to ADO.NET` 的第二个组件是 `LINQ to SQL`。该接口允许你通过使用实体类移除 `ADO.NET` 数据类型来与关系数据库交互。`LINQ to SQL` 使你能够直接查询 `SQL Server` 数据库模式。

图 27.1 描述了 `LINQ to ADO.NET` 与高级编程语言之间关系的概述：

![](img/e073a4882197be4ab61103cbe0bcb394_1360_0.png)

图 27.1：显示 `LINQ to ADO.NET` 的概述

让我们现在学习 `LINQ to ADO.NET` 所需的两种重要技术：`LINQ to DataSet` 和 `LINQ to SQL`。

### LINQ to DataSet

`DataSet` 是数据的一种非常有用的内存表示形式，并作为各种基于数据的应用程序的核心。在数据加载到 `DataSet` 之后，通常需要对数据执行额外的查询，这由 `LINQ to DataSet` 实现。

`LINQ to DataSet` 是查询缓存在 `DataSet` 对象中的数据的一种更简单、更快速的方式。`LINQ to DataSet` 通过让你在编程语言本身中编写查询来简化查询。`LINQ to DataSet` 中的函数使用运算符执行，允许你对 `DataSet` 执行 `LINQ` 查询。`ADO.NET SQL` 查询用于获取 `DataSet`。`LINQ to DataSet` 允许对任何可通过 `ADO.NET` 查询的数据库进行 `LINQ` 查询。你也可以使用 `LINQ to DataSet` 对来自一个或多个数据源的合并数据进行查询。

在使用 `LINQ to DataSet` 查询 `DataSet` 对象之前的第一步是填充 `DataSet` 对象。在 `DataSet` 对象中加载数据后，你可以对其进行查询。

`LINQ to DataSet` 的功能主要通过 `DataRowExtension` 和 `DataTableExtension` 类中的扩展方法公开。图 27.2 描述了 `LINQ to DataSet` 的关系：

![](img/e073a4882197be4ab61103cbe0bcb394_1361_0.png)

图 27.2：显示 `LINQ to DataSet` 的关系

### LINQ to SQL

`LINQ to SQL` 是 `.NET Framework 4.0` 的一个组件，专门为与 `SQL Server` 数据库协作而设计。它提供了一个运行时基础结构，用于将关系数据作为对象进行管理。它允许你编写查询以从 `SQL Server` 检索和操作数据。`LINQ to SQL` 支持你在开发 `SQL` 应用程序时所期望的所有关键功能。你可以从数据库检索数据，插入、更新和删除表中的信息。你的查询表达式被翻译成参数化 `SQL` 代码，参数被创建，并且查询在服务器上执行。`LINQ to SQL` 还支持事务、视图和存储过程。它还提供了一种将数据验证和业务逻辑规则轻松集成到你的数据模型中的方法。

`LINQ to SQL` 是一种对象关系映射（`ORM`）框架，允许 `Microsoft SQL Server` 数据库与 `.NET` 类之间直接一对一映射。在 `LINQ to SQL ORM` 映射的帮助下，与数据库表匹配的类会自动从数据库本身创建，你可以立即开始使用这些类。你可以在本章的 Immediate Solutions 部分找到 `LINQ to SQL` 的实际应用。

### 介绍 LINQ to XML

`LINQ to XML` 是在 `.NET Framework 4.0` 中读写 `XML` 数据的一种新方法。它补充了 `.NET Framework` 中的标准 `XML` 类，使使用 `XML` 变得更容易。`LINQ to XML` 为你提供了创建和查询 `XML` 数据的额外选项，从而实现更简单的代码和更快的开发。当你使用 `LINQ to XML` 时，你可以查询和修改文档，并在修改后保存文件。它提供了一个更易于使用的新对象模型，并利用了 `C#` 的改进。

`LINQ` 与 `XML` 的集成使你能够对内存中的 `XML` 文档编写查询以检索元素和属性的集合。`LINQ to XML` 的 `LINQ` 功能允许你对 `XML` 运行查询。`LINQ to XML` 提供了改进的 `XML` 编程接口。

`System.Xml.Linq` 命名空间包含 `LINQ to XML` 的类。以下是使用 `LINQ to XML` 可以执行的一些各种功能：

- 从文件或流加载 `XML`

- 将 `XML` 序列化到文件和流

- 使用函数式构造创建 `XML` 树

- 使用 `LINQ` 查询查询 `XML` 树

- 控制内存中的 `XML` 树

- 使用 `XML Schema Definition (XSD)` 验证 `XML` 树

让我们现在学习 `LINQ to XML` 与 `DOM` 方法之间的区别以及如何在 `LINQ` 中处理 `XML` 树。

### LINQ to XML 与 DOM 方法的区别

`XML Document Object Model (DOM)` 是当前占主导地位的 `XML` 编程 `API`。在 `XML DOM` 中，你自下而上地构建 `XML` 树。使用 `DOM` 创建 `XML` 树的典型方法是使用 `XmlDocument` 类。`LINQ to XML` 也支持使用 `XmlDocument` 类方法构建 `XML` 树。它还支持一种替代方法，称为函数式构造，该方法使用 `XElement` 和 `XAttribute` 构造函数构建 `XML` 树。

在 `LINQ to XML` 中，你可以直接处理 `XML` 元素和属性。你可以在不使用文档对象的情况下创建 `XML` 元素。它还直接从 `XML` 文件加载 `T:System.Xml.Linq.XElement` 对象。它还将 `T:System.Xml.Linq.XElement` 对象序列化到文件或流。当你将其与 `XML DOM` 进行比较时，`XML` 文档用作 `XML` 树的逻辑容器。在 `XML DOM` 中，节点（包括元素和属性）是在 `XML` 文档的上下文中创建的。使用 `XML DOM` 也很复杂。例如，如果你想在多个文档中使用一个元素，你必须在文档之间导入节点。这种复杂性在 `LINQ to XML` 中不存在。

使用 `LINQ to XML` 还通过消除完全处理命名空间前缀的先决条件来简化名称和命名空间。使用 `XML DOM` 不允许你更改节点的名称。作为替代，你必须创建一个新节点并将所有子节点复制到其中，这会导致丢失原始子节点标识。`LINQ to XML` 比 `XML DOM` 更简单地支持空白。

### 在 LINQ 中处理 XML 树

`LINQ to XML` 提供了一种强大的创建 `XML` 元素的方法，称为函数式构造，它能够在一行语句中创建 `XML` 树。你需要使用 `XElement` 构造函数，该构造函数接受各种类型的参数作为内容来在 `LINQ` 中创建 `XML` 树。`XElement` 构造函数采用 `Object` 类型的 `params` 数组，因此你可以向构造函数传递任意数量的对象。这有助于你使用具有复杂内容的元素。`XAttribute` 对象成为元素的属性。

当你实际创建 `XML` 树时，`XElement` 和 `XAttribute` 构造函数允许你将属性或元素的 `content` 作为参数传递给构造函数。你可以在其中传递任意数量的子元素，因为其中一个构造函数接受可变数量的参数。它支持任何类型的对象，该对象是 `XElement` 构造函数的有效子元素。在 `LINQ` 中创建 `XML` 树时，你应牢记以下规则：

- 字符串被添加为文本内容

- `XElement` 类被添加为属性

- `XAttribute` 类被添加为属性

- 对于除字符串以外的任何其他类型，你应调用 `ToString()` 方法

你可以在本章的 Immediate Solutions 部分了解更多关于在 `LINQ` 中处理 `XML` 树的内容。

### LinqDataSource 控件

`LinqDataSource` 控件使你能够通过在标记文本中设置属性在 `ASP.NET` Web 页面中使用 `LINQ`。你可以使用 `LinqDataSource` 控件创建检索或修改的 Web 页面

数据。你可以通过启用 `LinqDataSource` 控件自动创建与数据交互的命令，从而简化 Web 页面中的代码。`LinqDataSource` 控件与 `SqlDataSource` 和 `ObjectDataSource` 控件的相似之处在于，它可用于以声明方式将页面上的其他 `ASP.NET` 控件绑定到数据源。不同之处在于，`LinqDataSource` 控件不是直接绑定到数据库或泛型类，而是设计用于绑定支持 `LINQ` 的数据模型。

`LinqDataSource` 控件无法直接连接到数据库。相反，你需要与表示数据库和表的实体类进行交互。你可以使用对象关系设计器或运行 `SqlMetal.exe` 工具生成实体类，然后通过将 `ContextTypeName` 属性设置为表示数据库的类的名称，将 `LinqDataSource` 控件连接到数据库。你可以将 `TableName` 属性设置为表示数据表的类的名称，以连接到数据库中的特定表。例如，要连接到 `Northwind` 数据库的 `Employees` 表，你可以将 `ContextTypeName` 属性设置为 `Northwind`，将 `TableName` 属性设置为 `Employees` 表。类似地，要从内存中的数据集合检索数据，你可以将 `ContextTypeName` 属性设置为包含数据集合的对象。在这种情况下，你可以将 `TableName` 属性设置为返回数据集合的属性或字段。

> 注意

> 你已在本书第 26 章“`ASP.NET` 应用程序中的数据绑定”中详细了解了 `LinqDataSource` 控件。该控件值得注意的属性、方法和事件在第 26 章中列出。

## 扩展方法

`.NET Framework` 中的扩展方法允许你向现有类型添加方法，而无需创建新的派生类型。这是通过重新编译并修改原始类型来实现的。扩展方法接受参数，其中第一个参数定义它所扩展的类型。扩展方法与普通静态方法的基本区别在于，扩展方法要求第一个参数使用 `this` 关键字。你必须注意，扩展方法无法访问它所扩展的类型的私有成员。

定义 `LINQ` 扩展方法的类是 `Enumerable` 类，它位于 `System.Linq` 命名空间中。要使用扩展方法，只需导入包含在 `System.Core` 程序集中的这个命名空间。你可以使用 `Enumerable` 类中的 `Where()`、`OrderByDescending()` 和 `Select()` 方法。这些方法均返回 `IEnumerable<TSource>`。

扩展方法是一个有用的概念，尤其是在你想要扩展无法扩展的类时，例如密封类或没有源代码的类。

## 匿名方法

匿名方法允许你处理事件，而无需单独的事件处理程序。例如，如果希望在单击按钮时显示消息框，你可以使用委托和事件处理程序以标准方式处理，也可以使用匿名方法执行该操作。简而言之，匿名方法是用作委托参数的代码块。使用匿名方法的主要好处是减少需要编写的代码。使用匿名方法时，无需定义任何静态事件处理程序。匿名方法是在调用方处理事件时定义的。

使用匿名方法时，应始终记住以下几点：

- 在匿名方法中不能有目标位于匿名方法外部的跳转语句、`Break`、`GoTo` 或 `Continue`。

- 也不应在匿名方法中使用不安全代码。

- 如果需要多次编写相同的功能，则不应使用匿名方法。

匿名方法是在 `.NET Framework 2.0` 中引入的，但 `.NET Framework 3.5` 为匿名方法提供了一种名为 `Lambda` 表达式的新语法。与其传递匿名方法，你可以在 `LINQ` 中使用 `Lambda` 表达式完成相同的工作。

## Lambda 表达式

在 `.NET Framework 3.5` 中，为匿名方法引入了一种名为 `Lambda` 表达式的新语法。`Lambda` 表达式是一种匿名函数，它可以包含表达式和语句，以创建委托或表达式树类型。`Lambda` 表达式使用 `Lambda` 运算符 `=>`。`Lambda` 运算符的左侧指定输入参数，右侧指定表达式或语句，如下所示：

```
(input parameter) => expression
```

如果 `Lambda` 表达式只有一个参数，则括号是可选的。如果参数不止一个，则需要括号，并用逗号 `,` 分隔参数。使用 `Lambda` 表达式时，无需将变量添加到声明中；编译器会为你完成。

`Lambda` 表达式允许你以内联方式声明方法代码，而不是使用委托函数。它拥有更简洁的语法来实现相同的目标。

`Lambda` 表达式在编写 `LINQ` 查询表达式时非常有用，因为它们提供了一种非常紧凑且安全的方式来编写作为参数传递以供进一步计算的函数。

## 比较 Lambda 表达式与匿名方法

`Lambda` 表达式与匿名方法几乎相似，匿名方法是在 `.NET 2.0` 中引入的。与匿名方法相比，`Lambda` 表达式的优势在于它提供了更简洁、功能性更强的语法来编写匿名方法。在匿名方法中，需要花括号和 `return` 语句。`Lambda` 表达式的优势在于这些语法元素不是必需的，由编译器自动管理。

两者之间没有本质区别。这是因为 `Lambda` 表达式只是匿名方法的扩展，为编写匿名方法提供了更简洁、功能性更强的语法。换句话说，`Lambda` 表达式是一种包含表达式和语句的匿名函数，用于创建委托或表达式树类型。

## PLINQ 简介

`Parallel LINQ (PLINQ)` 是 `LINQ` 的并行实现，可以使用多个处理器执行查询。`PLINQ` 确保软件在执行环境中的并行处理器上具有可伸缩性。它适用于数据快速增长（例如电信行业）或数据异构的情况。`PLINQ` 还支持 `LINQ` 的所有运算符。此外，你可以使用 `PLINQ` 查询集合。它还可以同时运行多个 `LINQ` 查询，并利用系统上的处理器。除此之外，`PLINQ` 使用并行执行，因此查询运行速度很快。

`ASP.NET 4.0` 中的 `PLINQ` 配备了可用于取消 `PLINQ` 查询的取消类型，通过使用 `WithCancellation()` 运算符实现。由于 `PLINQ` 在多个处理器上运行，来自多个线程的异常很常见。`ASP.NET 4.0` 中的 `PLINQ` 使用 `AggregateException` 类型来收集线程抛出的所有异常。`PLINQ` 的功能继承自 `System.Linq.ParallelEnumerable` 类。

你将在本章的“即时解决方案”部分了解更多有关 `PLINQ` 实现的信息。

## 即时解决方案

### 创建 LINQ to SQL 应用程序

`LINQ to SQL` 是 `.NET Framework` 的组件，提供将关系数据作为对象进行管理的基础结构。你可以使用 `LINQ` 检索 `SQL` 数据。`LINQ to SQL` 将 `SQL` 查询转换为对象模型，并将其发送到数据库执行。让我们创建一个应用程序 `LINQtoSQL`（可在 `CD` 上获得），你可以在其中使用 `LINQ to SQL`。

> 注意

> 本章中的应用程序是使用“新建网站”对话框中的 `ASP.NET` 空网站模板创建的。创建应用程序后，你需要将 `Default.aspx` 页面添加到应用程序中。

执行以下步骤创建 `LINQ to SQL` 应用程序：

- 1. 在“解决方案资源管理器”中右键单击应用程序，然后从上下文菜单中选择“添加新项”选项。这将打开“添加新项”对话框。

- 2. 在此对话框中，选择“`LINQ to SQL` 类”模板，并将文件重命名为 `MyClasses.dbml`。`LINQ to SQL` 类的默认名称是 `DataClasses.dbml`。

- 3. 单击“添加”按钮，如图 27.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1365_0.png)

# 图 27.3：添加 LINQ to SQL 类

对象关系设计器随即打开。
