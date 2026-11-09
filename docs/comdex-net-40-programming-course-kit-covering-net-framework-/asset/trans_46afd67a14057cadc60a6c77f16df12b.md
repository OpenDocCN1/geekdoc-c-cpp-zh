
图 ASP-6.4.4

图 ASP-6.4.5

此时出现“图表区域集合编辑器”对话框。

- 13. 单击“图表区域集合编辑器”对话框中的 **确定** 按钮。
- 14. 将 **Default.aspx** 页面设置为起始页。
- 15. 按 **F5** 键执行应用程序。应用程序的输出出现，如图 ASP-6.4.6 所示：

图 ASP-6.4.6

学习完 Chart 控件后，我们来学习 QueryExtender 控件。

## 使用 QueryExtender 控件

QueryExtender 控件是一种数据绑定控件，可帮助仅从数据库中检索满足特定条件的记录。换言之，QueryExtender 控件会筛选记录。筛选记录有助于在网页上以各种方式显示记录，而不影响数据集。表6.32列出了 QueryExtender 控件的值得注意的属性。

**表6.32：QueryExtender 类的值得注意的属性**

| 属性 | 描述 |
| --- | --- |
| `ClientIDMode` | 为控件生成 ClientID 属性 |
| `EnableViewState` | 决定控件是否自动保存其视图状态 |
| `TargetControlID` | 保存目标控件的 ID |

| 属性 | 描述 |
| --- | --- |
| `ViewStateMode` | 确定是否为图表控件启用视图状态 |
| `Visible` | 决定控件是否应可见 |

表6.33列出了 QueryExtender 类的一些值得注意的方法。

**表6.33：QueryExtender 类的值得注意的方法**

| 方法 | 描述 |
| --- | --- |
| `ApplyStyleSheetSkin` | 将样式表中定义的样式应用到控件 |
| `DataBind` | 将数据源控件与数据库绑定 |
| `Dispose` | 使控件在从内存释放之前完成最后步骤 |
| `FindControl` | 借助控件的 ID 搜索服务器控件 |
| `Focus` | 将焦点设置在控件上 |
| `HasControls` | 确定父服务器控件中的子服务器控件 |

下面通过执行以下步骤来学习如何使用 QueryExtender 控件：

- 1. 单击 **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010。**
- 2. 从菜单栏中选择 **文件→新建→网站**。
  此时出现“新建网站”对话框。
- 3. 从中间模板窗格中选择 **Visual C#→ASP.NET 网站**。
- 4. 将 Web 应用程序的名称设置为 **QueryextenderControl。**
- 5. 单击 **确定** 按钮。
  **QueryextenderControl** 应用程序创建完成。
- 6. 在 Default.aspx 页面上拖放一个 Label、TextBox 和 Button 控件。
- 7. 将 **Label** 控件的 Text 属性设置为 **输入产品名称：**，并将 **Button** 控件的 Text 属性设置为 **搜索。**
- 8. 在 Web 窗体上添加 **GridView**、**QueryExtender** 和 **LinqDataSource** 控件。
- 9. 像本章前面那样为 **LinqDataSource** 配置数据库，并在“选择语句”页面中选择两列，例如 **ProductID** 和 **ProductName。**
- 10. 像本章前面那样将 GridView 的数据源设置为 **LinqDataSource1**。
- 11. 配置 QueryExtender 控件，如代码清单6.6所示：

**代码清单6.6：** 显示 Default.aspx 文件的代码

```aspx
<asp:Label ID="Label1" runat="server" Text="Enter Product Name:">
</asp:Label><asp:TextBox ID="TextBox1" runat="server" Width="178px"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Search" />
        <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False"
            DataKeyNames="ProductID" DataSourceID="LinqDataSource1">
            <Columns>
                <asp:BoundField DataField="ProductID" HeaderText="ProductID"
                    InsertVisible="False" ReadOnly="True" SortExpression="ProductID" />
                <asp:BoundField DataField="ProductName" HeaderText="ProductName"
                    SortExpression="ProductName" />
            </Columns>
        </asp:GridView>
        <br />
        <asp:QueryExtender ID="QueryExtender1" runat="server">
```

```aspx
TargetControlID="LinqDataSource1">
<asp:SearchExpression SearchType="StartsWith" DataFields="ProductName">
<asp:ControlParameter ControlID="TextBox1" />
</asp:SearchExpression>
</asp:QueryExtender>
<asp:LinqDataSource ID="LinqDataSource1" runat="server"
    ContextTypeName="DataClassesDataContext" Select="new(ProductID,
    ProductName)" EntityTypeName="TableName="Products">
</asp:LinqDataSource>
```

- 12. 像前面那样将 **Default.aspx** 页面设置为起始页。
- 13. 按 **F5** 键执行应用程序。应用程序的输出出现（图 ASP-6-47）。
- 14. 在 **搜索** 按钮旁边的文本框中输入产品名称，然后单击 **搜索** 按钮（图 ASP-6-47）。

输出显示在 GridView 控件中，如图 ASP-6-47 所示：

图 ASP-6-47

## 总结

本章学习了如何使用 ADO.NET。接着，学习了如何使用数据绑定控件（如 GridView、DataList、DetailsView、FormView 和 Repeater 控件）来显示和编辑数据库记录。还学习了使用数据绑定控件（即 ListView 和 DataPager 控件）进行分页。本章还介绍了用于访问数据的数据源控件，如 SqlDataSource、AccessDataSource、LinqDataSource、EntityDataSource 和 ObjectDataSource。还学习了如何使用 QueryExtender 控件筛选数据，以及如何使用 Chart 控件显示数据。此外，还学习了更改和修改数据绑定控件的各种样式和布局。

下一章将学习 Web 部件控件及其在 ASP.NET 4.0 中的实现。

# 第7章

# Web 部件控件

## 本章内容：

- 介绍 Web 部件控件
- 使用 Web 部件控件创建 Web 应用程序

Web 部件控件是 ASP.NET 的一组控件，允许您根据个人需求个性化网站。个性化意味着可以在运行时动态编辑网站以更改其内容、外观以及行为。Web 部件控件最初随 ASP.NET 2.0 引入，现在可用于所有新版本的 ASP.NET，例如 ASP.NET 3.0、ASP.NET 3.5 和 ASP.NET 4.0。Web 部件是允许最终用户执行各种功能以自定义正在运行的网站的外观和感觉的对象，例如打开或关闭控件、最大化或最小化网页、添加或删除内容，以及通过将控件拖动到网页上所需位置来更改控件的位置。一个网页可以有多个 Web 部件控件。应注意 Web 部件控件和 Web 部件彼此不同。Web 部件控件用于为网站创建 Web 部件。

本章学习 ASP.NET 4.0 中可用的 **WebParts** 控件，例如 **WebPartManager** 控件、**ProxyWebPartManager** 控件、**WebPartZone** 控件、**CatalogZone** 控件、**EditorZone** 控件和 **ConnectionsZone** 控件。本章还讨论这些控件的值得注意的属性、方法和事件。最后，学习使用所有这些 Web 部件控件创建网站。

现在，我们从 **WebParts** 控件的概述开始讨论。

## 介绍 Web 部件控件

如前所述，ASP.NET 中的 Web 部件控件是一组协同工作的控件，使您能够创建最终用户可以通过更改用户界面的外观和行为来修改的网页。换言之，Web 部件控件使您能够构建可在运行时动态自定义的灵活网站。

表7.1列出了 ASP.NET 4.0 中可用的各种 Web 部件控件：

**表7.1：Web 部件控件列表**

| 控件 | 描述 |
| --- | --- |
| WebPartManager | 管理网页中的所有 Web 部件控件。它没有用户界面 (UI)，并且在运行时不可见。 |
| ProxyWebPartManager | 允许开发人员在母版页中已指定 WebPartManager 控件时，在内容页中指定静态连接。 |
| WebPartZone | 描述 Web 部件控件的区域，可根据最终用户指定的要求重新定位、最大化或最小化这些控件。一个页面可以包含一个或多个 WebPartZone 控件。 |
| CatalogZone | 创建 Web 部件控件的目录。 |
| ImportCatalogPart | 导入 Web 部件控件（或用作 Web 部件控件的任何其他 ASP.NET 服务器控件）的描述文件，以便将该控件添加到网页。 |
| DeclarativeCatalogPart | 允许最终用户修改网页的功能。 |
| PageCatalogPart | 恢复网页上已删除的 Web 部件控件。它是恢复已删除的 Web 部件控件的唯一方式。 |
| EditorZone | 编辑网页上 Web 部件控件的外观、格式和结构。它是用于编辑的主要控件。 |
| LayoutEditorPart | 允许您更改链接的 Web 部件控件的面向布局的属性（如状态和标题）。当 Web 部件页处于编辑模式时，此控件可见。 |
| AppearanceEditorPart | 允许您编辑或更改网页上显示的 Web 部件控件的特性。 |

