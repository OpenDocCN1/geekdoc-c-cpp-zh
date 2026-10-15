

![](img/d99870e80390742f93963da7be0b2e61_751_0.png)

# 图 21-21

你想模仿之前所做的操作，因此在第二页中选择相应的值，以从 Customers 表中选择所有列，如图 21-22 所示。单击“高级”按钮，并启用插入、更新和删除，如图 21-23 所示。单击“确定”按钮关闭“高级选项”对话框，再单击“完成”按钮关闭向导。

![](img/d99870e80390742f93963da7be0b2e61_751_1.png)

# 图 21-22

![](img/d99870e80390742f93963da7be0b2e61_751_2.png)

# 图 21-23

现在，使用 GridView 控件上的智能标记绑定到 LinqDataSource，并启用分页、排序、编辑和删除，如图 21-24 所示。同时，使用智能标记为 GridView 控件自动套用格式。

请注意，除了数据源配置向导中存在一些细微差别之外，此页面的设计过程与使用 SqlDataSource 时相同。此外，当你运行该页面时，应该会看到与之前相同的内容和行为。这种设计上的一致性正是数据源控件的一大优势。

查看 LinqDataSource 的标记，你会发现它相当简单：

```
<asp:LinqDataSource ID="LinqDataSource1" runat="server"
    ContextTypeName="DataControls.NorthwindDataContext" EnableDelete="True"
    EnableInsert="True" EnableUpdate="True" EntityTypeName="" TableName="Customers">
</asp:LinqDataSource>
```

代码片段来自 Step03-Linq.aspx

![](img/d99870e80390742f93963da7be0b2e61_752_0.png)

图 21-24

让我们稍作扩展，添加按国家/地区筛选客户的功能。在示例项目中，该筛选器添加在一个名为 Step04-LinqWithParameter.aspx 的新页面中。你也可以继续使用之前创建的页面。

为 LinqDataSource 运行“配置数据源向导”。在第二页中，单击 Where 按钮，并输入图 21-25 所示的选项，以添加基于查询字符串参数的筛选器。

![](img/d99870e80390742f93963da7be0b2e61_752_1.png)

图 21-25

再看一眼 LinqDataSource 的标记，你会发现现在有一个 Where 属性表示筛选器，还有一个 QueryStringParameter 用于获取要筛选的国家/地区名称：

```
<asp:LinqDataSource ID="LinqDataSource1" runat="server"
    ContextTypeName="DataControls.NorthwindDataContext" EnableDelete="True"
    EnableInsert="True" EnableUpdate="True" EntityTypeName=""
    TableName="Customers" Where="Country == @Country">
    <WhereParameters>
```

```
<asp:QueryStringParameter DefaultValue="Canada" Name="Country" QueryStringField="Country" Type="String" />
</WhereParameters>
</asp:LinqDataSource>
```

> 代码片段来自 Step04-LinqWithParameter.aspx

运行页面并在 URL 末尾添加“?Country=Mexico”以设置查询字符串参数。你应该会看到与图 21-26 类似的页面。

![](img/d99870e80390742f93963da7be0b2e61_753_0.png)

图 21-26

# 使用 ObjectDataSource 控件进行数据绑定

通过查询字符串传递国家/地区是可行的，但如果希望允许用户从下拉列表中选择国家/地区，又该如何呢？Northwind 数据库没有 Country 表，因此你需要通过查询获取可能的值。具体来说，你需要从 Customers 表中找出不重复的国家/地区名称集合。

你可以轻松地向 NorthwindDataContext 添加一个方法来执行查询并返回国家/地区名称。在解决方案资源管理器中右键单击 Northwind.dbml，选择“查看代码”，然后添加以下内容：

```
Public Function GetCountryNames() As String()
    Dim query = From cust In Customers
                Select cust.Country Distinct
                Order By Country

    Return query.ToArray()
End Function
```

> 代码片段来自 Northwind.vb

有了这个方法之后，你现在可以添加一个 DropDown 控件，并使用 ObjectDataSource 将其绑定到该方法。ObjectDataSource 允许你将任何其方法公开了标准 CRUD（增删改查）功能的对象用作数据源。在 GridView 上方添加一个 DropDown 控件，并在页面底部添加一个 ObjectDataSource 控件。使用 ObjectDataSource 上的智能标记打开“配置数据源向导”。

在第一页中，选择 NorthwindDataContext 作为将提供数据的业务对象，如图 21-27 所示。

![](img/d99870e80390742f93963da7be0b2e61_754_0.png)

# 图 21-27

在第二页中，你可以设置在尝试选择、插入、更新或删除时要调用的业务对象方法。你不需要更新数据，因此只需选择一个 Select 方法。在 Select 选项卡中，选择 GetCountryNames，并单击“完成”按钮完成向导（见图 21-28）。

![](img/d99870e80390742f93963da7be0b2e61_754_1.png)

# 图 21-28

当使用简单类型（即字符串、整数、日期）的数组时，配置 DropDown 控件绑定到 ObjectDataSource 会有些棘手，因为“选择数据源向导”（通过智能标记访问）会假定你想要绑定到 Select 方法返回的对象的属性，而不是对象本身。例如，如果你运行向导来绑定 GetCountryNames 返回的字符串数组，它会尝试让你显示每个字符串的长度（见图 21-29）。

![](img/d99870e80390742f93963da7be0b2e61_755_0.png)

图 21-29

在这种情况下，我们采用更“老派”一点的做法，使用属性窗口而不是设计器中的向导来设置 DropDown 控件的属性。进行数据绑定只需要将 DataSourceID 属性设置为 ObjectDataSource1。你还需要将 AutoPostBack 属性设置为 True，以便在选择新的国家/地区名称时页面会重新进行绑定。

最后，你需要更新 LinqDataSource，使其使用来自 DropDown 控件的值，而不是通过查询字符串传递的值。打开 LinqDataSource 控件的“配置数据源向导”，在第二页单击 Where 按钮。在弹出的对话框中，删除现有表达式，并使用图 21-30 所示的值添加一个新表达式。

![](img/d99870e80390742f93963da7be0b2e61_755_1.png)

图 21-30

运行项目时，你应该只会看到来自下拉列表中所选国家/地区的客户。页面看起来应该与图 21-31 所示的页面类似。

![](img/d99870e80390742f93963da7be0b2e61_756_0.png)

图 21-31

# 小结

本章涵盖了大量内容。它从整体上讨论了 ASP.NET 应用程序的许多方面，以及在构建和部署这些应用程序时你所拥有的选择。凭借本章学到的技能，你应该能够构建和部署允许你显示和编辑数据库数据的简单应用程序。对许多人来说，这些技能足以解决分配给你的大部分任务。

然而，这并不意味着没有更多内容需要介绍。下一章将深入探讨使用 ASP.NET 和 WebForms 构建 Web 应用程序时可用的一些更高级的功能。

# 22

# ASP.NET 高级功能

# 本章你将学习的内容

+   - 母版页的用途和使用
+   - 快速轻松地为网站添加导航
+   - 使用成员资格和角色保护对网站的访问
+   - 为网站用户添加持久化配置文件
+   - 使用 ASP.NET 提供程序模型
+   - 使用 Microsoft Ajax 增加丰富性和交互性

ASP.NET 是一项令人兴奋的技术。它使得创建和交付远程生成的应用程序（Web 应用程序）成为可能，这些应用程序可通过一个简单的浏览器访问——而浏览器是许多人相当熟悉的容器。基于 Web 的应用程序（在这里即 ASP.NET 应用程序）的目的是通过 HTTP 仅向最终用户交付应用程序的单个实例。这意味着浏览你应用程序的最终用户始终可以使用最新版本。因此，如今许多公司都在考虑使用 ASP.NET，不仅用来交付公司网站，还用来向员工、合作伙伴和客户交付一些最新应用程序。

上一章介绍了 ASP.NET 的一些基础知识。本章将继续这一探索，向你展示一些额外且令人兴奋的技术，包括母版页、导航、个性化、AJAX 等。

# 母版页

许多 Web 应用程序在构建时，都让应用程序的每个页面具有相似的外观和感觉；并且可能包含共同的页面元素，例如页眉、导航区、广告、页脚等。大多数人希望应用程序具有统一性，以便为最终用户提供跨页面的一致体验。

ASP.NET 2.0 引入了一个名为*母版页*的功能，它使你可以创建定义一组页面共同元素的模板（或一组模板）。创建母版页后，你

