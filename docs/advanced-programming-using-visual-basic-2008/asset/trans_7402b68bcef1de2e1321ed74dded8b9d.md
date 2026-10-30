

默认使用 Microsoft Access 所需的设置。由于我们使用的是 SQL Server，因此将使用 SqlDataSource。本章后面你将使用 ObjectDataSource 控件来处理多层应用程序。

## 向 Web 项目添加数据

为了便于在课堂和家中工作，我们将数据库包含在项目文件夹中。请注意，对于工业界的生产任务，你的最终应用程序将连接到数据库服务器。在创建新的 Web 站点项目后，右键单击 App_Data 文件夹并从上下文菜单中选择 Add Existing Item。从中浏览找到数据库并将其添加到项目中。你应该在配置数据源之前执行此步骤。

### 添加 SqlDataSource 控件

当你将 SqlDataSource 控件拖到 Web 页面时，你会在页面上看到该控件。它在设计时出现，但在运行时不出现。打开智能标记并选择 Configure Data Source（图 8.2）。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_376_0.png)

**Figure 8.2** A SqlDataSource control on a Web Form; select Configure Data Source to set up the database access.

配置数据源向导会让你感到熟悉（图 8.3）。选择 New Connection 并浏览到项目 App_Data 文件夹中的数据库文件。选择将连接保存到应用程序配置文件选项。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_376_1.png)

**Figure 8.3** In the familiar Configure Data Source wizard, you can set up a new connection for the data source.

向导的下一页要求你配置 Select 语句。你可以选择指定自定义 SQL 语句或存储过程，也可以选择从表或视图中选择列（图 8.4）。同时请注意指定仅返回唯一行的复选框，以及用于自定义 SQL 语句的 WHERE 和 ORDER BY 按钮。你可以展开 Name 列表以选择数据库中的任何单个表。请注意，选择指定自定义 SQL 语句或存储过程选项会给你机会打开过去使用过的标准查询设计器。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_377_0.png)

**Figure 8.4** The Configure Data Source wizard can help you set up the SQL SELECT statement.

### 使连接字符串动态化

连接字符串会自动创建并放置在 Web.config 文件中，其中包含指向目录的硬编码路径：

```
connectionString="Data Source=.\\SQLEXPRESS;AttachDbFilename=&quot;C:\\Documents and Settings\\UserName\\Desktop\\Northwind.MDF&quot;;Integrated Security=True;User Instance=True" providerName="System.Data.SqlClient"
```

为了使项目具有可移植性，删除绝对路径名并替换为 "|DataDirectory|"（输入竖线但不带引号）。此约定表示数据库位于项目的 App_Data 文件夹中。

```
<connectionStrings>
    <add name="pubsConnectionString"
         connectionString="Data Source=.\\SQLEXPRESS;AttachDbFilename=&quot;|DataDirectory|pubs.MDF&quot;;Integrated Security=True;User Instance=True"
         providerName="System.Data.SqlClient" />
</connectionStrings>
```

## 在 DetailsView 控件中显示数据

另一种显示数据的方法是一次显示一条记录，使用 DetailsView 控件。同样，无需编写代码；你只需添加数据源和详细信息控件。配置数据源并为详细信息数据控件分配数据源。

与网格一样，列名默认用作 DetailsView 控件上的字段标签（图 8.6）。在智能标记上选择 Enable Paging 可提供其他记录的链接，这仅适用于非常小的表。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_379_0.png)

**Figure 8.6** A DetailsView control displays individual records without writing any code. The links for other records are provided by the Enable Paging option on the smart tag.

你可以通过从 DetailsView 的智能标记中选择 Edit Fields 来自定义数据的显示。要手动设置标题，请从 BoundField 列表中选择一个字段；该字段的属性会出现，你可以在其中设置 HeaderText 属性（图 8.7）。你还可以重新排序字段并添加和删除显示中的字段。从 Selected Fields 列表中选择一个字段并单击 Delete 按钮即可将其从显示中删除。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_379_1.png)

**Figure 8.7** Set properties of the bound fields, including the HeaderText, in the Fields dialog box. You also can reorder the fields and add and remove fields.

Fields 对话框和控件的智能标记都有添加新字段的选项。与 GridView 类似，你可以将 DetailsView 控件的 Width 属性设置为百分比，例如 80%。

## 在 FormView 控件上显示数据

另一种在单独字段中显示数据的选项是 **FormView** 控件。与 DetailsView 类似，FormView 一次显示一条记录，但你对字段布局的控制更多。

要使用 FormView 控件，首先添加并配置你的数据源，然后添加 FormView 控件。当你将 FormView 对象设置为数据源时，包含绑定字段的模板会自动生成。要修改布局，必须编辑模板。请注意图 8.8 中的其他记录链接；该选项是通过在控件的智能标记上选择 *Enable Paging* 创建的。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_380_0.png)

**Figure 8.8** Bound data are displayed in a FormView control. The links are provided by the Enable Paging option.

要修改 FormView 的布局，请从智能标记中选择 *Edit Templates*。选择 *ItemTemplate* 时（图 8.9），你可以直接在表单上的模板中输入文本。通过选择和编辑显示的模板来修改标题。你可以更改字段的顺序、删除字段、更改标签中的文本或更改控件的类型。完成更改后，返回智能标记并选择 *End Template Editing*。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_380_1.png)

**Figure 8.9** You can select the option to edit the item template or several other templates when you select *Edit Templates* from the FormView's smart tag.

要查看 FormView 中改进格式的示例，请查看 Ch08Bindings 的设计视图（图 8.10）。添加了标题“Publishing Contact Details”并使用 H1 HTML 块格式进行了格式化。为了使标签和数据字段对齐，在项目模板中添加了一个表，将控件移入表格单元格，并编辑了字段的标识标签。请注意，City、State 和 Zip 字段出现在同一行，城市后面带有一个逗号。输出看起来很棒，而且仍然没有代码。

要格式化 FormView 的模板，你可以添加表、添加文本并应用格式。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_381_0.png)

### 检查数据绑定

Web 应用程序的实际数据绑定与 Windows 版本非常不同。要查看绑定，请打开 Ch08Bindings，选择 FormView 控件上的智能标记，然后选择 Edit Templates。接下来，单击 PublIDLabel 控件并从其智能标记中选择 Edit DataBindings。请注意，PublIDLabel 使用 Text 作为可绑定属性（图 8.11）。Text 的绑定指定该字段绑定到数据源中的 PublID。

PublIDLabel 的 Text 属性的数据绑定是通过为 Text 选择绑定完成的。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_381_1.png)

你可能想选中 Show all properties 复选框以查看可用于绑定的不同属性数量。你通常使用 Text 属性，因为你希望数据显示。

## 在下拉列表中显示数据

你可以使用工具箱标准部分中的多个控件来显示绑定数据。任何具有 DataSource 属性的控件都可以绑定到数据。DropDownList 控件可以绑定到数据并用于选择记录，其方式类似于 Windows 应用程序中的组合框选择。但是，你必须使用参数化查询来显示选择的結果。

以下逐步练习使用数据绑定下拉列表来选择记录。DropDownList 控件的 ViewState 属性在一次调用到下一次调用之间维护列表的内容。但是，如果应用程序具有多个页面并且用户可以在页面之间导航，则必须采取措施维护列表内容。参见本章后面的“Maintaining the State of List Boxes”。

### 创建参数化查询—逐步操作

在 Web 应用程序中从下拉列表中显示选择的步骤与 Windows 版本不同。以下逐步练习将带你完成设置控件和编写参数化查询以检索所选记录的匹配记录的过程。

**设置数据库访问**

- STEP 1: 创建一个名为 Ch08DropDownList 的新 Web 站点项目。选择解决方案名称并将解决方案文件保存在项目文件夹中。
- STEP 2: 将 DOCUMENT Title 属性设置为“Ch08DropDownList”。
- STEP 3: 选择 App_Data 文件夹，右键单击并选择 Add Existing Item。添加 Pubs.mdf 文件。
- STEP 4: 从工具箱的数据选项卡添加 SqlDataSource 控件。将控件命名为 StoresSqlDataSource。配置它以连接到项目 App_Data 文件夹中 Pubs 数据库中的 stores 表。仅选择 stor_id 和 stor_name 字段。
- STEP 5: 编辑 Web.config 文件以使项目具有可移植性：从连接字符串中删除整个硬编码路径并替换为“|DataDirectory|\Pubs.mdf”。AttachDbFilename 属性应如下所示：

```
AttachDbFilename=|DataDirectory|\Pubs.mdf;
```

**添加并配置下拉列表**

- STEP 1: 在表单上放置一个 DropDownList 控件并将其命名为 StoreNameDropDownList。
- STEP 2: 在控件的智能标记中，选择 Choose Data Source。在 Data Source Configuration Wizard 中（图 8.12），将数据源设置为 StoresSqlDataSource，显示 stor_name，stor_id 作为值的字段。值用于参数化查询，以检索所选商店的匹配数据。单击 OK。注意：如果显示和值列表未填充，请在 Choose Data Source 对话框上单击 Refresh Schema 链接。

