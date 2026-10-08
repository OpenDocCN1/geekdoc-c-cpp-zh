

# 第 22 章 数据库与 LINQ

## 表之间的关系

图 22.9 中连接表的线表示表与之间的关系。考虑 `Authors` 表和 `AuthorISBN` 表之间的线。在连接的一端是 1，在 `AuthorISBN` 端是无限大符号（∞）。这表示一种一对多的关系——对于 `Authors` 表中的每个作者，`AuthorISBN` 表中可以有该作者编写的任意数量的 ISBN（也就是说一个作者可以写任意数量的书）。注意，该关系将 `Authors` 表中的 `AuthorID` 列（其中 `AuthorID` 是主键）连接到 `AuthorISBN` 表中的 `AuthorID` 列（其中 `AuthorID` 是外键）——表之间的线将主键与匹配键连接起来。

`Titles` 表和 `AuthorISBN` 表之间的线说明了一对多的关系——一本书由多个作者编写。表与表之间的线将 `Titles` 表中的主键 `ISBN` 连接到 `AuthorISBN` 表中相应的外键。图 22.9 所示，`AuthorISBN` 表的唯一目的是在 `Authors` 表和 `Titles` 表之间提供多对多的关系——一个作者可以写很多书，一本书可以有很多作者。

## 22.4 LINQ to Entities 和 ADO.NET Entity Framework

使用 ADO.NET Entity Framework，你通过 IDE 根据数据库架构生成的类与数据库进行交互。你将通过向项目添加新的 ADO.NET Entity 数据模型来启动此操作（你将在第 22.5.1 节中看到）。

### 在实体数据模型中生成的类

对于 `Books` 数据库中的 `Authors` 和 `Titles` 表，IDE 在每个数据模型中创建了两个类：

- 第一个类表示表的一行，并包含表中每列的属性。该类的对象——称为**行对象**——存储了表中单行的数据。IDE 使用表复数形式名称的单数形式作为类名。对于 `Books` 数据库的表，行的名称是 `Author`，对于 `Titles` 表，是 `Title`。
- 第二个类表示表本身。该类的对象存储了与表中的所有行相对应的的对象集合。`Books` 数据库的表类命名为 `Authors` 和 `Titles`。

一旦生成，实体数据模型类在 IDE 中就具有 IntelliSense 支持。第 22.7 节演示了使用 `Books` 数据库表之间的关系进行数据连接查询。

### 实体数据模型中表之间的关系

你会注意到我们没有提到 `Books` 数据库的 `AuthorISBN` 表。回想一下该表连接了

- `Authors` 表中的每个作者到该作者在 `Titles` 表中的书籍，以及
- `Titles` 表中的每本书到该书在 `Authors` 表中的作者。

实体数据模型生成的类包含了表与之间的关系。例如，`Author` 类包含一个名为 `Titles` 的导航属性，它提供了访问代表该作者所有书籍的 `Title` 对象的方法。IDE 自动在 "Title" 后面加上 "s"，以表示该属性代表 `Title` 对象集合。同样， `Row` 类包含一个名为 `Authors` 的导航属性，它提供了访问代表特定书籍作者的 `Authors` 方法。

### DbContext 类

`DbContext`（命名空间 `System.Data.Entity`）管理程序与数据库之间的数据流。当 IDE 生成实体数据模型的行类和表类时，它还会创建一个特定于所操作数据库的 `DbContext` 类。此派生类具有 `Authors` 和 `Titles` 表的属性。正如你将看到的，这些可以作为 LINQ 查询和 UI 中操作数据的源。对 `DbContext` 管理的数据任何更改都可以使用 `SaveChanges` 方法保存回数据库。

### IQueryable<T> 接口

LINQ to Entities 通过 `IQueryable<T>` 工作，该接口继承自第 9 节引入的 `IEnumerable<T>`。当针对 `IQueryable<T>` 的 LINQ to Queries 查询对数据库执行时，结果会被加载到相应的实体数据模型对象中以便在代码中方便地访问。

### 使用扩展方法操作 IQueryable<T> 对象

回想扩展方法可以在不修改类源代码的情况下为现有类添加功能。在第 9 节中，我们引入了几个 LINQ 扩展方法，包括 `First`、`Count`、`ToArray` 和 `ToList`。这些方法被定义为类 `Enumerable`（命名空间 `System.Linq`）的静态方法，可以应用于任何实现 `IEnumerable<T>` 接口的对象，例如集合以及 LINQ to Objects 查询的结果。

在本章中，我们使用 LINQ 查询和扩展方法的结合来操作数据库内容。我们使用的扩展方法被定义为类 `Queryable`（命名空间 `System.Linq`）的静态方法，可以应用于任何实现 `IQueryable<T>` 接口的对象——包括各种实体数据模型对象和 LINQ to Entities 查询的结果。

## 22.5 使用 LINQ 查询数据库

在本节中，我们将演示如何

- 连接到数据库，
- 查询它并
- 显示查询结果。

本节内容不多——IDE 提供了可视化编程工具和向导，简化了应用程序中数据的访问。这些工具建立了数据库连接，并创建了通过 Windows Forms GUI 控件查看和操作数据的必要对象——这种技术被称为**数据绑定**。对于第 22.5–22.8 节的示例，我们将创建一个包含多个项目的解决方案。我们将使用一个包含多个项目的可重用类库。其他项目将是使用 ADO.NET Entity Data Model 与数据库交互的 Windows Forms。我们使用数据绑定来显示数据。

我们将执行的基本步骤是：

- 创建 ADO.NET Entity 数据模型。
- 将实体数据模型添加到项目中。
- 将表拖到设计视图中。
- 添加允许应用程序的代码。

GUI 如图 22.10 所示。当我们数据源拖到窗口时，所有的控件都会自动生成。顶部的 `BindingNavigator` 是一个控件集合，允许你导航记录。`BindingNavigator` 的控件帮助你添加记录、删除记录、修改记录并保存更改。可以通过按下添加按钮并在 DataGridView 中输入新作者。可以通过选择作者（在 DataGridView 中或通过 BindingNavigator）并按下删除按钮来删除现有记录。可以通过点击姓名字段并输入新值来编辑现有记录。点击保存按钮将更改保存到数据库。`Authors` 表不允许空值；如果你尝试保存一个不包含名和姓的记录，则会发生异常。

### 22.5.1 创建 ADO.NET Entity 数据模型类库

本节描述了从现有数据库创建实体数据模型的步骤。模型描述了你将操作的数据——在我们的案例中，是 `Books` 数据库表中表示的数据。

步骤 1：创建用于 ADO.NET Entity 数据模型的类库项目选择“文件 > 新 > 项目...”以显示新建项目对话框，从 Visual C 模板中选择“类库”并命名项目为 `BooksExamples`。点击“确定”创建项目，然后从解决方案管理器中删除 `Class1.cs` 文件。

步骤 2：向类库添加 ADO.NET Entity 数据模型为了与数据库交互，你将向类项目添加 ADO.NET 实体数据模型。这将配置到数据库的连接。

1. 添加 ADO.NET Entity 数据模型。右键点击解决方案管理器中的 `BooksExamples` 项目，然后选择“添加 > 新项...”以显示新建项对话框（图 22.11）。从“数据”类别选择“ADO.NET Entity 数据模型”并命名模型为 `BooksModel`——这将是配置实体数据模型的文件（扩展扩展为 .edmx）的名称。点击“添加”将实体数据模型添加到类库，并使用实体数据模型向导对话框。

