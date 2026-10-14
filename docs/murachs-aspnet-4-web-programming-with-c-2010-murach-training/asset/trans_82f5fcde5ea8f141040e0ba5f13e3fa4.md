

# AccessDataSource 类的 Select 方法

| 方法 | 描述 |
| --- | --- |
| Select(selectOptions) | 返回一个 IEnumerable 对象，其中包含从底层 Access 数据库检索到的行。要获取所有行，selectOptions 参数应为 DataSourceSelectArguments.Empty。 |

# 用于检索行的 DataView 类的成员

| 属性 | 描述 |
| --- | --- |
| RowFilter | 用于过滤从 Access 数据库检索到的行的字符串。 |
| 索引器 | 描述 |
| [index] | 返回指定索引位置的行的 DataRowView 对象。 |

# 用于检索列的 DataRowView 类的成员

| 索引器 | 描述 |
| [index] | 以对象形式返回指定索引位置的列的值。 |
| [name] | 以对象形式返回指定名称的列的值。 |

# 获取所选产品的产品信息的代码

```
DataView productsTable = (DataView)
    AccessDataSource1.Select(DataSourceSelectArguments.Empty);
productsTable.RowFilter =
    "ProductID = '" + ddlProducts.SelectedValue + "'";
DataRowView row = (DataRowView) productsTable[0];

Product p = new Product();
p.ProductID = row["ProductID"].ToString();
p.Name = row["Name"].ToString();
p.ShortDescription = row["ShortDescription"].ToString();
p.LongDescription = row["LongDescription"].ToString();
p.UnitPrice = (decimal)row["UnitPrice"];
p.ImageFile = row["ImageFile"].ToString();
```

# 描述

- AccessDataSource 类的 Select 方法返回一个 IEnumerable 对象，其中包含从 Access 数据库检索到的行。要处理这些行，必须将 IEnumerable 对象强制转换为 DataView 对象。
- DataView 类的 RowFilter 属性允许您根据条件字符串过滤数据视图中的行。
- 您可以使用 DataView 类的索引器以 DataRowView 对象的形式返回特定行。然后，您可以使用 DataRowView 类的索引器返回指定列的值。列的索引器可以是表示列在行中位置的整数，也可以是表示列名称的字符串。
- DataView 和 DataRowView 类存储在 System.Data 命名空间中。

# 如何使用会话状态

在第 1 章中，您了解到 HTTP 是一种无状态协议。您还了解到 ASP.NET 使用 *会话状态* 来跟踪每个用户会话，并且您可以使用会话状态在应用程序的执行之间维护程序值。现在，您将了解有关会话状态的工作原理以及如何使用它的更多信息。

## 会话状态的工作原理

图 3-14 显示了会话状态如何解决 ASP.NET 应用程序的状态管理问题。如您所见，会话状态通过为每个用户的会话创建一个 *会话状态对象* 来跟踪各个用户会话。此对象包含唯一标识会话的会话 ID。此会话 ID 会连同 HTTP 响应一起传回浏览器。然后，如果浏览器发出另一个请求，会话 ID 将包含在请求中，以便 ASP.NET 可以识别会话。ASP.NET 然后将会话与之前保存的会话状态对象匹配。

默认情况下，ASP.NET 将会话 ID 作为 *cookie* 发送给浏览器。然后，当浏览器向服务器发送另一个请求时，它会自动将包含会话 ID 的 cookie 与请求一起发送。在第 8 章中，您将了解有关 cookie 的更多信息。您还将学习如何通过将会话 ID 包含在页面的 URL 中而不是 cookie 中来实现会话状态。

尽管 ASP.NET 自动使用会话状态来跟踪用户会话，但您也可以使用它在应用程序的执行之间存储自己的数据。此图列出了这样做的三个典型原因。首先，您可以使用会话状态维护有关用户的信息。例如，用户登录到应用程序后，您可以使用登录信息从文件或数据库中检索有关用户的信息。然后，您可以将该信息存储在会话状态对象中，以便每次执行应用程序时都可用。

其次，您可以使用会话状态保存用户正在处理的对象。例如，考虑一个允许用户更改客户记录的维护应用程序。在这种情况下，您可以将当前正在修改的客户记录保存在会话状态对象中，以便下次执行应用程序时可用。

第三，您可以使用会话状态跟踪用户当前正在执行的操作。例如，如果维护应用程序允许用户添加或更改客户记录，您可以在会话状态对象中保存一个项目，指示用户当前是正在添加还是更改记录。这样，应用程序每次执行时都可以确定如何继续。

# ASP.NET 如何维护会话的状态

![](img/c024ccf88e28c30c07dd410d4342288f_124_0.png)

# 描述

- ASP.NET 使用 *会话状态* 来跟踪应用程序中每个用户的状态。为此，它会创建一个 *会话状态对象*。
- 会话状态对象包含一个会话 ID，该 ID 作为 *cookie* 发送回浏览器。然后，浏览器会自动将会话 ID cookie 与每个请求一起返回给服务器，以便服务器可以将浏览器与现有的会话状态对象关联起来。
- 如果您希望应用程序在不支持 cookie 的浏览器上运行，您可以配置 ASP.NET 将会话 ID 编码到应用程序每个页面的 URL 中。有关更多信息，请参阅第 8 章。
- 您可以使用会话状态对象在应用程序的执行之间存储和检索项目。

# 会话状态的典型用途

- **保留有关用户的信息**，例如用户名或用户是否已注册。
- **保存用户正在处理的对象**，例如购物车或客户记录。
- **跟踪待处理操作**，例如用户在下订单时已完成的步骤。

# 如何在会话状态中处理数据

图 3-15 显示了如何使用会话状态对象存储应用程序数据。为此，您使用此对象创建的 HttpSessionState 类的成员。要从 Web 表单访问此对象，您使用页面的 Session 属性。

会话状态对象包含由项目名称及其值组成的项目集合。将项目添加到此集合的一种方法是使用索引器，如第一个示例所示。在这里，一个名为 cart 的对象被分配给名为 Cart 的会话状态项目。如果执行此语句时 Cart 项目不存在，它将被创建。否则，Cart 项目的值将被更新。

将项目添加到会话状态集合的另一种方法是使用 Add 方法，如第二个示例所示。就像使用索引器一样，如果项目已存在，执行 Add 方法时它将被更新。否则，它将被添加到集合中。

您还可以使用索引器检索会话状态集合中项目的价值，如第三个示例所示。在这里，Cart 项目的值被检索并分配给 cart 变量。由于会话状态项目的值存储为 Object 类型，因此您通常将其强制转换为适当的类型。在此示例中，Cart 项目的值被强制转换为排序列表，因为 cart 变量被定义为排序列表。

由于会话状态对象使用宝贵的服务器内存，因此您应避免使用它来存储大型项目。或者，如果您必须将大型项目存储在会话状态中，则应在完成后立即将其删除。为此，您使用 Remove 方法，如本图中的第四个示例所示。

本图中的前四个示例使用页面的 Session 属性来访问会话状态对象。然而，由于 Session 是 System.Web.UI.Page 类的属性，因此您只能从继承 System.Web.UI.Page 类的类中使用此属性。换句话说，您只能从页面的代码隐藏文件中使用它。要从不继承 System.Web.UI.Page 类的类（例如数据库或业务类）访问会话状态，您使用当前请求的 HttpContext 对象的 Session 属性。要获取此 HttpContext 对象，您使用 HttpContext 类的 Current 属性，如本图中的最后一个示例所示。

