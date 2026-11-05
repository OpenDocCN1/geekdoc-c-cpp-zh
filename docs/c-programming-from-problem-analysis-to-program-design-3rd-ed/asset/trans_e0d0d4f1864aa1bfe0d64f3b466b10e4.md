
```csharp
{
    this.lblClassif.Text = "Special Students ";
}
this.lblClassif.Text += " Always Welcome!";
}
}
}
```

## AccessDataSource

与其在 btnShowMembers_Click() 方法中编写程序语句来连接数据库并检索数据，你可以使用数据可视化配置工具，让这些语句自动为你生成。你会回想起第14章中，当你使用 Visual Studio 或 Visual Web Developer Express 版产品将数据绑定控件拖到应用程序上时，控件上会出现一个智能标记，使你可以选择绑定数据源。.NET 包含数据源类，可减少访问各个 Data Provider 类的需要。AccessDataSource 类简化了将 ASP.NET Web 页连接到 Access 数据库的过程。AccessDataSource 是一个特殊类，它实际上继承自 SqlDataSource，并提供了专门用于 Access 数据库的附加功能。

AccessDataSource 和 SqlDataSource 类都使用 SQL 查询来执行数据检索。每个类都有大量可设置的属性，以及许多可编程的公共和受保护方法和事件。鼓励你浏览 MSDN 文档以了解更多关于这些类的信息。AccessDataSource 控件的独特特征之一是，你不需要设置 Connection String 属性来将控件绑定到数据库。你只需使用 DataFile 属性确定 Access .mdb 文件的位置，AccessDataSource 对象就会处理到底层数据库的连接。

你会回想起，在较早的示例中，member.mdb 数据库的位置或路径是硬编码的。使用 AccessDataSource 控件对象，你可以提供数据库的相对路径。这使部署或移动数据驱动的 Web 站点更容易。你不再需要更改代码来反映数据库实际存储的位置。首次构建新 Web 站点时，应创建一个名为 App_Data 的文件夹。App_Data 文件夹由 ASP.NET 保留用于存储数据文件。这是你应存储 Access 数据库文件的位置。

### 使用可视化工具进行连接

较早的解决方案使用 DataGrid 显示数据库记录。为了说明可视化配置工具的用法，从“数据工具箱”中选择一个 GridView 对象并放到页面上。当控件对象放到页面上时，其智能标记会显示“选择数据源”选项，如图 15-26 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1000_0.png)

**图 15-26** 将数据源绑定到 GridView

选择 **新建数据源** 可启动 **数据源配置向导**。正如你在第14章所见，可以通过多种不同方式打开此工具。你可以查看 **服务器资源管理器** 窗口，并从那里添加连接。你也可以从 **数据工具箱** 将 **AccessDataSource 对象** 拖到页面上，然后设置其属性。通过将 **GridView 对象** 拖到页面上并使用其智能标记，你可以将数据连接绑定到其基础数据源。如图 15-27 所示，你可以确定应用程序应从哪里获取数据。

![](img/e33ae760e23d89eac66541252ad65de8_1000_1.png)

**图 15-27** 连接到 Access 数据库

当你选择 **Access 数据库**（如图 15-27 所示）时，将创建 AccessDataSource 类的一个实例。如果你为数据源指定 ID，该名称将成为窗体上控件上方显示的选择器标识符。选择 **数据库** 会创建 SqlDataSource 的实例。如果选择 **数据库**，下一个对话框将允许你创建 Connection string。你可以将此选项用于 Access 数据库。但是，如果你选择 **Access 数据库**，则不必设置 Connection string 属性；你只需确定 Access .accdb 文件的位置，如图 15-28 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1001_0.png)

**图 15-28** Access 数据库的相对地址

将 Access 数据库放入 **App_Data** 目录后，浏览到该位置，就会设置相对路径，如图 15-28 所示。

你可以使用 **解决方案资源管理器** 窗口，通过右键单击 **App_Data** 文件夹并选择 **添加现有项**，将数据库放入 **App_Data** 目录。然后可以 **浏览** 到其原始位置。

现在数据库通过相对路径引用（例如，`~/App_Data/member.accdb`）。你将在 **设计** 模式下看到页面上出现 **AccessDataSource** 对象的新控件，如图 15-29 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1002_0.png)

**图 15-29** AccessDataSource 对象

如图 15-29 所示，AccessDataSource 的 DataFile 属性被设置为数据库的相对地址。如果你移动 Web 站点，ASP.NET 将在应用程序的 App_Data 文件夹中查找数据库。

找到文件后，配置数据源向导使你能够确定要在 GridView 上显示哪些表和字段。如图 15-30 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1002_1.png)

**图 15-30** 确定要检索的数据

如图 15-30 所示，有一个标记为 **Name** 的下拉列表，可用于选择数据库表。如果选择 **WHERE** 按钮，将启动查询生成器工具。若要使项按特定字段升序或降序显示，可使用 **Order By** 选项。对于 WebControls 应用程序，记录按 **LastName** 排序。如图 15-30 中显示底部所示，将根据你的选择生成 SQL select 语句。

完成数据源配置后，GridView 的智能标记中会提供选项。**GridView 任务** 列表如图 15-31 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1003_0.png)

**图 15-31** GridView 任务

如图 15-31 所示，你现在有启用分页、排序和选择的选项。选择 **启用排序** 选项后，你可以选择某一列，并让表按该字段重新排序。如果要更改列标题，请使用 **编辑列** 选项。**编辑列** 选项会显示一个对话框，可在其中更改每个字段的属性。每个字段都有许多属性，分为 **Accessibility**、**Appearance**、**Behavior**、**Data** 和 **Style**。姓氏和名字的 **HeaderStyle** 的 **BackColor** 属性均设置为黄色（#FFFFC0）。

### 设置 Visible 属性

使用 GridView 的 WebControls 应用程序的 btnShowMembers_Click() 方法不再需要代码来连接数据库并填充页面上的控件。回想一下，这是由 **配置数据源** 向导在后台完成的。如果你查看示例 15-14 和 15-15，你会注意到 btnShowMembers_Click() 方法中的第一行代码是一个语句，当用户单击 **See Current Members** 按钮时，使表格上方的标签可见。如果你还想等到用户单击此按钮后再显示 GridView 对象，则应将 Label 和 GridView 的 Visible 属性初始设置为 false。需要向此方法再添加一行代码，使 GridView 可见。新的 btnShowMembers_Click() 如示例 15-16 所示。所有数据库连接代码均已删除。

### 示例 15-16

```csharp
protected void btnShowMembers_Click(object sender,
                                    System.EventArgs e)
{
    lblMembers.Visible = true;
    this.GridView1.Visible = true;
}
```

### 修改数据

默认情况下，GridView 控件以只读格式在 Web 窗体上显示数据。要允许用户编辑存储在 GridView 对象中的数据，你可以使用“高级”按钮从数据源配置工具配置 select 语句。此“高级”按钮如图 15-30 所示。选择此选项会生成所需的其他 Insert、Delete 和 Update SQL 语句。

要使用此功能，在数据源配置期间，所有主键值都必须作为 select 语句的一部分被检索。键字段不必显示在 GridView 上。配置完成后，可以使用智能标记移除它们；但是，查询必须返回它们的值。

> 注意不要在显示内容中遗漏主键结果。如果你已指定某个键字段不能为空，那么当该键未输入值时，你将无法添加记录。

在 InsertCommand、UpdateCommand 和 DeleteCommand 的 SQL 语句可用后，GridView 的智能标记会显示 **启用编辑** 和 **启用删除** 的附加选项。如果选择这些选项，将向 GridView 表中添加一个附加列，如图 15-32 所示。

![](img/e33ae760e23d89eac66541252ad65de8_1004_0.png)

**图 15-32** 修改数据表

