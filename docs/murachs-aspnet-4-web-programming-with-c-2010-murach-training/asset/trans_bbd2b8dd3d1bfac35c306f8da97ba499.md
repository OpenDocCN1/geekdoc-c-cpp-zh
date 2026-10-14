

## 视角

在本章中，你已经学习了如何使用对象数据源。正如你所见，对象数据源利用了 ASP.NET 的省时数据绑定功能，同时不牺牲将表示代码与数据访问代码分离的基本原则。正因如此，你可能想要考虑使用对象数据源而不是 SQL 或 Access 数据源。

如果你决定在应用程序中使用对象数据源，那么你当然需要学习如何在代码中使用 ADO.NET。为此，我们推荐我们的 ADO.NET 书籍 for C# 程序员，它提供了完整的 ADO.NET 数据库编程课程。完成它之后，你将能够有或没有数据源地使用 ADO.NET。

## 术语

- 3-layer architecture
- presentation layer
- middle layer
- database layer
- object data source
- data access class
- business object class
- data object class
- 3-tier architecture
- reflection
- C# attribute

## 练习 17-1 创建 Customer List 应用程序

在本练习中，你将开发一个应用程序，使用两个对象数据源在所选州中显示客户列表。为了更轻松，你将从一个包含对象数据源将使用的數據访问类、起始页面、页面使用的图像和样式表以及包含指向 Halloween 数据库的连接字符串的 web.config 文件的应用程序开始。

### 查看数据访问类中的代码

- 1. 在 C:\aspnet4_cs 目录中打开 Ch17CustomerList 应用程序。
- 2. 显示 App_Code 文件夹中的 CustomerDB 类，注意它包含三个名为 GetAllStates、GetCustomersByState 和 GetConnectionString 的方法。还要注意该类被标记为 DataObject 属性，并且 GetAllStates 和 GetCustomersByState 方法被标记为 DataObjectMethod 属性。
- 3. 查看 GetAllStates 和 GetCustomersByState 方法的代码，查看它们都返回一个 IEnumerable 对象。具体来说，GetAllStates 方法返回一个包含 States 表中的 StateCode 和 StateName 列的数据读取器对象，而 GetCustomersByState 方法返回一个包含 Customers 表中的 LastName、FirstName 和 PhoneNumber 列的数据读取器对象。

### 添加下拉列表及其数据源

- 4. 在设计视图中显示页面，将下拉列表添加到主分区，并从智能标记菜单中选择 Choose Data Source 命令以显示数据源配置向导的第一步。
- 5. 选择创建新数据源的选项，在向导的第二步中选择 Object，然后单击 OK 以显示第一个 Configure Data Source 对话框。
- 6. 显示此对话框中的下拉列表，注意它仅包含 CustomerDB 类。选择此类然后单击 Next 以显示第二个 Configure Data Source 对话框。
- 7. 显示此对话框中的下拉列表，注意它包含两个被标记为数据对象方法的方法。选择 GetAllStates 方法然后单击 Finish 以返回数据源配置向导的第一步。
- 8. 显示向导中的下拉列表，注意它们都是空的。然后在第一个下拉列表中输入“StateName”，在第二个下拉列表中输入“StateCode”。
- 9. 为你刚创建的下拉列表启用自动回发，并将 ID 属性更改为适当的值。

### 添加 GridView 控件及其数据源

- 10. 在 ObjectDataSource 控件下方添加一个 GridView 控件，并将其绑定到一个从 CustomerDB 类的 GetCustomersByState 方法获取数据的新的对象数据源。此方法应从下拉列表中获取其参数的值。
- 11. 运行应用程序，显示不同州的客户，注意 GridView 中列的宽度会根据它们包含的数据而变化。
- 12. 返回设计视图，显示 GridView 控件的 Fields 对话框，注意 Auto-generate Fields 选项已选中。
- 13. 取消选中 Auto-generate Fields 选项，然后为 GetCustomersByState 方法返回的三个列添加三个绑定字段。为此，你需要手动输入 DataField 属性的列名，并且需要为 HeaderText 属性添加列标题。此外，将每列的宽度设置为 150 像素，并左对齐列标题。
- 14. 再次运行应用程序查看效果。然后关闭浏览器窗口。

## 练习 17-2 修改 Product Receipt 应用程序

在本练习中，你将修改练习 14-2 中创建的 Product Receipt 应用程序，使其使用对象数据源而不是 SQL 数据源。为了更轻松，我们将包含应用程序使用的數據访问类和业务类的代码。

### 查看起始代码

- 1. 在 C:\aspnet4_cs 目录中打开 Ch17ProductReceipt 应用程序。
- 2. 查看 Default 页面的 aspx 代码。然后运行应用程序以刷新你对其工作原理的记忆。
- 3. 查看 App_Code 文件夹中的 Product 类的代码，注意它为 ProductID、Name 和 OnHand 列定义了三个自动实现的属性。
- 4. 查看 ProductDB 类的代码。注意 GetProducts 方法返回一个 List<Product> 对象。还要注意 UpdateProduct 方法接受单个 Product 对象，因为它没有实现乐观并发。

### 添加 ObjectDataSource 控件

- 5. 向 Default 页面添加一个 ObjectDataSource 控件，并配置它以使用 ProductDB 类的 GetProducts 方法检索数据并使用 UpdateProduct 方法更新产品。
- 6. 将对象数据源的 DataObjectTypeName 属性设置为“Product”。
- 7. 将 GridView 控件的数据源从 SQL 数据源更改为你刚创建的对象数据源。当显示一个询问是否要重新生成 GridView 列字段和数据键的对话框时，单击 No。
- 8. 删除 SqlDataSource 控件，因为它不再被页面使用。
- 9. 运行应用程序并测试以确保其正确工作。完成后，关闭浏览器窗口。

### 使用设计器查看绑定字段

- 10. 显示 GridView 控件的智能标记菜单并选择 Edit Columns 命令。
- 11. 选择 ID 字段，并滚动该字段的属性直到可以看到 DataField 属性。
- 12. 显示 DataField 属性的下拉列表，注意你可以看到所有可用字段的名称。这是因为 select 方法返回一个强类型的 List<Product> 集合。

## 第 4 部分

## 专业 ASP.NET 技能

本部分由六章组成，介绍在专业 Web 应用程序中经常使用的 ASP.NET 技能。首先，第 18 章向你展示如何为应用程序使用安全连接，第 19 章向你展示如何使用 Web Site Administration Tool 和登录控件对应用程序的用户进行身份验证和授权。这些是电子商务应用程序必不可少的技能。

接下来，第 20 章向你展示如何使用电子邮件和自定义错误页面，以及如何处理用户在浏览器中单击后退按钮时可能出现的问题。这些技能对大多数专业应用程序都很有用。

第 21 章向你介绍 AJAX 并向你展示如何使用 AJAX 服务器控件。然后，第 22 章向你展示如何配置和部署应用程序，这是你为开发的每个应用程序都需要做的。到那时，你将能够以彻底专业的水平开发和部署电子商务应用程序。

最后，在第 23 章中，你将被介绍到 WCF 服务。WCF 服务允许你定义可被各种应用程序使用的操作，包括基于其他技术和平台构建的应用程序。WCF 现在是使用 ASP.NET 开发服务的标准。

由于本部分中的每一章都作为独立模块编写，你可以按任何你喜欢的顺序阅读这些章节。例如，如果你想学习如何从 Web 应用程序发送电子邮件，你可以直接跳到第 20 章。或者，如果你想学习如何配置和部署 ASP.NET 应用程序，你可以跳到第 22 章。最终，你还是想阅读所有章节，因为你至少应该了解它们提供的功能。

