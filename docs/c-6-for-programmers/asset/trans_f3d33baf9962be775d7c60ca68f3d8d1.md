

ID 号、名字和姓氏（分别对应）。图 20.4 包含 Authors 表的示例数据。

| 列 | 描述 |
|---|---|
| AuthorID | 作者在数据库中的 ID 号。在 Books 数据库中，这个整数列被定义为标识列，也称为自动递增列——每当表中插入一行时，AuthorID 值会自动增加 1，以确保每一行都有唯一的 AuthorID。这是*主键*。 |
| FirstName | 作者的名字（字符串）。 |
| LastName | 作者的姓氏（字符串）。 |

**图 20.3** | Books 数据库的 *Authors* 表。

| AuthorID | FirstName | LastName |
|---:|---|---|
| 1 | Paul | Deitel |
| 2 | Harvey | Deitel |
| 3 | Abbey | Deitel |
| 4 | Sue | Green |
| 5 | John | Purple |

**图 20.4** | *Authors* 表中的数据。

## Titles 表

Titles 表（如图 20.5 所述）由四列组成，用于维护数据库中每本书的信息，包括其 ISBN、书名、版次和版权年份。图 20.6 包含 Titles 表中的数据。

| 列 | 描述 |
|---|---|
| ISBN | 书的 ISBN（字符串）。该表的主键。ISBN 是“International Standard Book Number”（国际标准书号）的缩写——全球出版商使用的一种编号方案，用于为每本书提供*唯一*的识别号。 |
| Title | 书的标题（字符串）。 |
| EditionNumber | 书的版次（整数）。 |
| Copyright | 书的版权年份（字符串）。 |

**图 20.5** | Books 数据库的 *Titles* 表。

| ISBN | Title | EditionNumber | Copyright |
|---|---|---|---|
| 0132151006 | Internet & World Wide Web How to Program | 5 | 2012 |
| 0133807800 | Java How to Program | 10 | 2015 |
| 0132575655 | Java How to Program, Late Objects Version | 10 | 2015 |
| 0133976890 | C How to Program | 8 | 2016 |
| 0133406954 | Visual Basic 2012 How to Program | 6 | 2014 |
| 0134601548 | Visual C# How to Program | 6 | 2017 |
| 0134448235 | C++ How to Program | 10 | 2016 |
| 0134444302 | Android How to Program | 3 | 2016 |
| 0134289366 | Android 6 For Programmers: An App-Driven Approach | 3 | 2016 |
| 0133965260 | iOS 8 for Programmers: An App-Driven Approach with Swift | 3 | 2015 |
| 0134021363 | Swift for Programmers | 1 | 2015 |

图 20.6 | Books 数据库的 Titles 表中的数据。

## Books 数据库的 AuthorISBN 表

AuthorISBN 表（如图 20.7 所述）由两列组成，用于维护每本书的 ISBN 及其对应作者的 ID 号。该表将作者与其书籍关联起来。AuthorID 列是一个外键——该表中的一列，与另一个表中的主键列（即 Authors 表中的 AuthorID）匹配。ISBN 列也是一个外键——它与 Titles 表中的主键列（即 ISBN）匹配。一个数据库可能由许多表组成。数据库设计者的目标之一是最小化数据库各表之间重复数据的数量。外键在数据库表创建时指定，用于链接多个表中的数据。该表中的 AuthorID 和 ISBN 列共同构成一个复合主键。该表中的每一行都将一位作者唯一地匹配到一本书的 ISBN。图 20.8 包含 Books 数据库的 AuthorISBN 表中的数据。

| 列 | 描述 |
|---|---|
| AuthorID | 作者的 ID 号，是 Authors 表的外键。 |
| ISBN | 书的 ISBN，是 Titles 表的外键。 |

图 20.7 | Books 数据库的 AuthorISBN 表。

| AuthorID | ISBN | AuthorID | ISBN |
|---|---|---|---|
| 1 | 0132151006 | 1 | 0132575655 |
| 1 | 0133807800 | 1 | 0133976890 |

图 20.8 | Books 数据库的 AuthorISBN 表中的数据。（共 2 部分中的第 1 部分。）

## 表之间的关系

图 20.9 中连接各表的线条表示表之间的关系。考虑 Authors 表和 AuthorISBN 表之间的线条。在 Authors 表的一端有一个 1，而在 AuthorISBN 表的一端有一个无穷大符号（∞）。这表示一对多关系——对于 Authors 表中的每一位作者，在 AuthorISBN 表中可以有任意数量的该作者所写书籍的 ISBN（即一位作者可以写任意数量的书）。请注意，关系线条将 Authors 表中的 AuthorID 列（AuthorID 是主键）与 AuthorISBN 表中的 AuthorID 列（AuthorID 是外键）链接起来——表之间的线条将主键与匹配的外键链接起来。

Titles 表和 AuthorISBN 表之间的线条说明了一对多关系——一本书可以由多位作者撰写。请注意，表之间的线条将 Titles 表中的主键 ISBN 与 AuthorISBN 表中对应的外键链接起来。图 20.9 说明 AuthorISBN 表的唯一目的是在 Authors 表和 Titles 表之间提供多对多关系——一位作者可以写很多书，而一本书可以有很多位作者。

## 20.4 LINQ to Entities 与 ADO.NET Entity Framework

使用 ADO.NET Entity Framework 时，你可以通过 IDE 根据数据库架构生成的类与数据库交互。你将通过向项目添加新的 ADO.NET Entity Data Model 来启动此过程（如第 20.5.1 节所述）。

### 在 Entity Data Model 中生成的类

对于 Books 数据库中的 Authors 表和 Titles 表，IDE 在数据模型中各创建两个类：

- 第一个类表示表的一行，并为表中的每一列包含属性。此类的对象——称为行对象——存储表中各行的数据。IDE 使用表复数名称的单数形式作为行类的名称。对于 Books 数据库的 Authors 表，行类的名称是 Author；对于 Titles 表，行类的名称是 Title。
- 第二个类表示表本身。此类的对象存储一个行对象集合，对应于表中的所有行。Books 数据库的表类分别命名为 Authors 和 Titles。

一旦生成，实体数据模型类在 IDE 中便拥有完整的 IntelliSense 支持。第 20.7 节演示了利用 Books 数据库各表之间的关系来联接数据的查询。

### Entity Data Model 中的表间关系

你会注意到，我们没有提及 Books 数据库的 AuthorISBN 表。回想一下，该表将

- Authors 表中的每位作者与其在 Titles 表中的书籍关联起来，以及
- Titles 表中的每本书与其在 Authors 表中的作者关联起来。

实体数据模型生成的类包含表之间的关系。例如，Author 行类包含一个名为 Titles 的导航属性，该属性提供对 Title 对象的访问，这些对象表示该作者撰写的所有书籍。IDE 会自动在“Title”后添加“s”，以表明该属性表示 Title 对象的集合。类似地，Title 行类包含一个名为 Authors 的导航属性，该属性提供对 Author 对象的访问，这些对象表示某本书的作者。

### DbContext 类

**DbContext**（命名空间 **System.Data.Entity**）管理程序与数据库之间的数据流。当 IDE 生成*实体数据模型*的行类和表类时，它还会创建一个 DbContext 的派生类，该派生类特定于所操作的数据库。对于 Books 数据库，这个派生类具有针对 Authors 表和 Titles 表的属性。你将看到，这些属性可以用作在 LINQ 查询和 GUI 中操作数据的数据源。对 DbContext 管理的数据所做的任何更改都可以使用 DbContext 的 **SaveChanges** 方法保存回数据库。

### IQueryable\<T\> 接口

LINQ to Entities 通过接口 **IQueryable\<T\>** 工作，该接口继承自第 9 章中介绍的接口 **IEnumerable\<T\>**。当对 **IQueryable\<T\>** 对象执行的 LINQ to Entities 查询在数据库上运行时，结果会被加载到相应实体数据模型类的对象中，以便在代码中方便地访问。

### 使用扩展方法操作 IQueryable\<T\> 对象

回想一下，扩展方法在不修改现有类源代码的情况下为其添加功能。在第 9 章中，我们介绍了几种 LINQ 扩展方法，包括 First、Any、Count、Distinct、ToArray 和 ToList。这些方法定义为 Enumerable 类（命名空间 System.Linq）的静态方法，可以应用于任何实现 IEnumerable\<T\> 接口的对象，例如数组、集合以及 LINQ to Objects 查询的结果。

在本章中，我们结合使用 LINQ 查询语法和 LINQ 扩展方法来操作数据库内容。我们使用的扩展方法定义为 Queryable 类（命名空间 System.Linq）的静态方法，可以应用于任何实现 IQueryable\<T\> 接口的对象——这些对象包括各种实体数据模型对象以及 LINQ to Entities 查询的结果。

## 20.5 使用 LINQ 查询数据库

在本节中，我们演示如何

- *连接*数据库，
- *查询*数据库，以及
- *显示*查询结果。

本节中的代码很少——IDE 提供了*可视化编程工具和向导*，简化了应用中数据的访问。这些工具建立数据库连接，并创建通过 Windows Forms GUI 控件查看和操作数据所需的对象——这种技术称为数据绑定。

