

![](img/cf7012644082c115a2181376d9b7486d_187_0.png)

图 5.17 设置与 SAP HANA XS 项目共享：第 2 部分

![](img/cf7012644082c115a2181376d9b7486d_187_1.png)

图 5.18 设置与 SAP HANA XS 项目共享：第 3 部分

## 5.4 构建应用程序数据模型

在本节中，你将开始构建应用程序的数据模型。这里，我们将从定义将存储书店数据的数据库表开始。

然后，在配置这些表之后，我们将探讨将此数据暴露给客户端层的方法。

### 5.4.1 使用核心数据服务定义持久性模型

作为完全符合 SQL 标准的数据库，使用数据定义语言 (DDL) 从 SQL 命令行创建应用程序的数据库表相当容易。然而，事实证明，SAP HANA 提供了多种定义表的替代方案，这些方案在将应用程序推广到系统环境时大大简化了物流工作。本质上，这些替代方案要求创建 SAP HANA 特定的元文件，这些元文件以逻辑术语定义表。每当我们将这些元文件部署到 SAP HANA 存储库时，SAP HANA 都会使用元数据自动为我们创建相应的物理表。如果你熟悉 ABAP 编程环境，这种行为类似于 ABAP 数据字典中的透明表定义。

如今，在 SAP HANA 中定义表或视图的新兴标准是核心数据服务 (CDS)。从概念上讲，你可以将 CDS 视为一种 SAP HANA 特定的元语言，它允许我们以通用方式定义可重用的类型、实体、视图等。出于我们的目的，我们将使用 CDS 来构建图 5.19 所示的表架构。这个简单的模型引入了一对实体（Books 和 Authors），它们通过关联表（BookAuthors）相互链接。

![](img/cf7012644082c115a2181376d9b7486d_188_0.png)

图 5.19 书店数据模型的实体-关系 (E-R) 图

要使用 CDS 创建图 5.19 所示的数据模型，必须在项目中创建一个新的 DDL 源文件。可以通过执行以下步骤来实现：

- 1. 在 SAP HANA XS 项目文件夹中，创建一个子文件夹，用于存储所有与模型相关的对象。在我们的项目中，我们将此子文件夹命名为 MODEL。可以通过在 Eclipse 中右键单击项目文件夹并选择 New > FOLDER 菜单选项来创建此文件夹。

- 2. 创建子文件夹后，通过右键单击子文件夹并选择 New > OTHER... 菜单选项来创建 DDL 文件。这将打开图 5.20 所示的新建对话框。从这里，目标对象类型包含在 SAP HANA > DATABASE DEVELOPMENT 文件夹结构中。单击 Next > 按钮继续。

![](img/cf7012644082c115a2181376d9b7486d_189_0.png)

图 5.20 创建 DDL 源文件：第 1 部分

- 3. 在下一屏幕（如图 5.21 所示），为文件命名（Bookstore-Model.hdbdd）并单击 FINISH 按钮以创建工件。

![](img/cf7012644082c115a2181376d9b7486d_190_0.png)

图 5.21 创建 DDL 源文件：第 2 部分

清单 5.1 包含我们用于创建书店数据模型的 CDS 内容。虽然对本摘要中使用的 CDS 语法进行详尽介绍超出了本书的范围，但弄清楚这里发生的事情并不太困难。基本上，我们希望基于图 5.19 中包含的 E-R 图定义的三个表被表示为实体类型。除了实体本身之外，我们还有一个名为 ISBN 的可重用类型和一个名为 BookAuthorsView 的视图，我们将稍后使用它来查询与给定书籍关联的作者。

```
namespace (account_name).hcpbook.bookstore.storefront.model;

@Schema: 'SYS_BIC'
context Bookstore {
    type ISBN: String(13);

type AmountType {
    amount: Decimal(5,2);
    currencycode: String(3);
};
};

entity Books {
  key isbnNumber: ISBN;
  title: String(100);
  publicationYear: Integer;
  pageCount: Integer;
  listprice: AmountType;
  currency: String(255);
  coverImageURL: String(255);
};

entity Authors {
  key Id: Integer;
  firstName: String(50);
  lastName: String(50);
};

entity BookAuthors {
  key isbnNumber: ISBN;
  key author: Association to Authors;
};

define view BookAuthorsView as SELECT FROM BookAuthors {
  isbnNumber,
  author.firstName,
  author.lastName
};
```

清单 5.1 使用 CDS 定义书店数据模型

> **注意**
> 
> 有关 CDS 及规范中定义的各种语法选项的更多信息，我们强烈建议你下载一份 SAP HANA Core Data Services (CDS) 参考指南，可在 http://help.sap.com/hana_platform 在线获取。

### 5.4.2 将数据模型作为 OData 服务公开

如我们在第 5.1 节中所述，我们书店应用程序的用户界面将基于 SAPUI5 技术。从集成角度来看，这意味着我们必须通过某种 REST-based 服务来公开数据模型。由于 SAPUI5 非常适合使用 OData-based 服务，让我们看看将数据模型作为 OData 服务公开需要什么。

事实证明，SAP HANA 使将第 5.4.1 节中构建的数据模型作为 OData 服务公开变得异常容易。为此，我们使用 XS OData 对象类型，它定义了一种抽象语法，用于将 SAP HANA 数据库中的表或视图映射到 OData 服务定义中的实体。

要创建 XS OData 文件，请右键单击模型文件夹并选择 New > XS OData File 菜单选项，如图 5.22 所示。然后，在图 5.23 所示的 NEW XS ODATA SERVICE 对话框中，为服务文件指定名称（BookstoreService.xsodata）并单击 Finish 按钮。

![](img/cf7012644082c115a2181376d9b7486d_192_0.png)

图 5.22 创建 XS OData 文件：第 1 部分

清单 5.2 包含我们为示例应用程序创建的 XS OData 文件的摘录。这里，[namespace] 标记指的是我们在第 5.4.1 节中创建的 CDS 文件中用于定义实体/视图的同一命名空间。标记中的 as “[Entity_Name]” 部分将选定的表或视图分配给 OData 服务定义文件中的实体。除了实体定义本身之外，我们还在 Books 和 BookAuthors 实体之间混合了一个关联，以便我们的 SAPUI5 应用程序能够在运行时浏览此关联以读取与所选书籍关联的作者。

![](img/cf7012644082c115a2181376d9b7486d_193_0.png)

图 5.23 创建 XS OData 文件：第 2 部分

```
service namespace "hcpbook.bookstore" (
  "namespace":Bookstore.Books"
  as "Books" navigates ("Book_Authors" as "Authors");
  "namespace":Bookstore.BookAuthorsView"
  as "BookAuthors" key ("isbnNumber","firstName","lastName");
  association "Book_Authors" principal "Books"("isbnNumber")
  multiplicity "1"
  dependent "BookAuthors"("isbnNumber") multiplicity "*";
)
```

清单 5.2 示例 XS OData 文件

尽管在开始使用 SAP HANA XS OData 文件语法时存在一定的学习曲线，但这一切的主要收获是，我们可以在几行代码中在基于 SAP HANA 的持久性模型之上开发只读 OData 服务。在需要时，我们还可以通过用 SAP HANA 的专有 SQLScript 语言或服务器端 JavaScript 编写的自定义退出，将服务范围扩展到执行其他 CRUD 操作（例如，创建、更新和删除）。所有这些背后的细节都包含在 SAP HANA 开发者指南中。

### 5.4.3 从服务器端 JavaScript 消费数据模型

虽然基于 OData 的访问将是我们 SAPUI5 应用程序的首选数据消费方法，但值得注意的是，SAP HANA 编程模型还提供了另一种将数据模型暴露给客户端层的替代方案：服务器端 JavaScript。

在本书的源代码包中，你会找到一个名为 booklist.xsjs 的文件，它演示了如何使用 SQL 查询从 Books 表获取数据，然后以 HTML 表的形式返回结果。从概念上讲，你会发现这里的语法/流程与 Java Servlet/JSP 类似（请参阅清单 5.3）。也就是说，服务器端 JavaScript 文件是一个可寻址的 HTTP 对象，可用于提供各种内容：HTML、XML、JSON 等等。有关服务器端 JavaScript 的更多信息，请参阅 SAP HANA 开发者指南。

```
// Build the HTML5 output string:
$.response.contentType = "text/html";
var output =
    '<!DOCTYPE html><head><meta charset="UTF-8">' +
    '<title>HCP Book HANA XS App Demo</title></head><body>' +
    '<table><thead><tr><th>ISBN Number</th><th>Title</th><th>Year Published</th><th>Page Count</th></tr></thead>' +
    '</tbody></table>';

// Fetch the book catalog from the Books table:
var sql =
    "SELECT * FROM " +
    "\"SYS_BIC\".\"\\"account\\"\\"hcpbook.bookstore.storefront.model\\"\"" +
    ".\"BookStore.Books\"";
var conn = $.db.getConnection();
var pstmt =
    conn.prepareStatement(sql);
var rs = pstmt.executeQuery();

while (rs.next()) {
    output += '<tr>';
    output += '<td>' + rs.getString(1) + '</td>';
    output += '<td>' + rs.getString(2) + '</td>';
    output += '<td>' + rs.getString(3) + '</td>';
    output += '<td>' + rs.getString(4) + '</td>';
    output += '</tr>';
}
```

