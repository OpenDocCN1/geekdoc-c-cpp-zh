

22.9 地址簿案例研究 973

```csharp
// 当表单加载时，用数据库中的数据填充
private void Contacts_Load(object sender, EventArgs e)
{
    RefreshContacts(); // 用数据库中的数据填充绑定源
}
```

**图 22.42** | 在应用程序加载时调用 RefreshContacts 来填充 TextBox。

## 方法 addressBindingNavigatorSaveItem_Click

方法 addressBindingNavigatorSaveItem_Click（图 22.43）在点击 BindingNavigator 的“保存数据”（Save Data）按钮时，将更改保存到数据库。（记得启用此功能。）地址数据库需要名字、姓氏、电话号码和电子邮件的值。当你尝试保存时，如果某个字段为空，则会发生 DbEntityValidation 异常。我们在保存后调用了 RefreshContacts（第 72 行），以重新排序数据并返回到第一个元素。

```csharp
// BindingNavigator 中保存按钮的点击事件处理程序
// 将更改保存到数据源中
private void addressBindingNavigatorSaveItem_Click(
    object sender, EventArgs e)
{
    Validate(); // 验证输入字段
    addressBindingSource.EndEdit(); // 完成当前编辑（如果有）
    // 尝试保存
    try {
        dbcontext.SaveChanges(); // 将更改写入数据库文件
    } catch (DbEntityValidationException) {
        MessageBox.Show("列不能为空",
        "实体验证异常");
    }
    RefreshContacts(); // 切换回更新后的未过滤数据
}
```

**图 22.43** | 当用户点击“保存数据”时将更改保存到数据库。

## 方法 FindButton_Click

方法 FindButton_Click（图 22.44）使用 LINQ 查询语法（第 81–85 行）仅选择姓氏以 TextBox 中的字符开头的个人。该查询按姓、名字对结果进行排序。在 LINQ to Entities 中，你不能直接将 LINQ 查询绑定到 BindingSource.DataSource。因此，第 88 行获取了对象的 ToList 以获取过滤后数据的 List 表示，并将该 List 赋值给 BindingSource.DataSource。当你将查询转换为 List 时，DbContext 中现有记录的任何更改都将由 DbContext 跟踪——你在查看过滤数据时添加或删除的任何记录都将丢失。出于此原因，当数据被过滤时禁用了“添加”和“删除”按钮。当你输入姓氏并点击“查找”时，BindingNavigator 允许用户浏览包含匹配名称的行。这是因为绑定到 Form 控件上的数据（LINQ 查询的结果）已经发生变化，现在只有有限的行。

```csharp
// 使用 LINQ 创建一个数据源，其中仅包含
// 以指定文本开头的姓氏
private void findButton_Click(object sender, EventArgs e)
{
    // 使用 LINQ 过滤姓氏以 findTextBox 内容
    // 开头的联系人
    var lastName =
        from address in dbcontext.Addresses
        where address.LastName.StartsWith(findTextBox.Text)
        orderby address.LastName, address.FirstName
        select address;

    // 显示匹配的联系人
    addressBindingSource.DataSource = lastQuery.ToList();
    addressBindingSource.MoveFirst(); // 转到第一个结果
    // 联系人过滤时不添加/删除
    bindingNavigatorAddNewItem.Enabled = false;
    bindingNavigatorDeleteItem.Enabled = false;
}
```

图 22.44 查找姓氏指定字符串开头的联系人。

方法 browseAllButton_Click
方法 browseAllButton_Click（图 22.45）允许用户在搜索特定行后返回浏览所有行。双击 browseButton 以创建 Click 事件处理程序。该事件处理程序处理添加和删除按钮，然后调用 RefreshContacts 将数据源恢复为完整人员列表（按排序顺序）并清除 findTextBox。

```csharp
// 使用所有行重新加载 addressBindingSource
private void browseAllButton_Click(object sender, EventArgs e)
{
    // 联系人未过滤时允许添加/删除
    bindingNavigatorAddNewItem.Enabled = true;
    bindingNavigatorDeleteItem.Enabled = true;
    RefreshContacts(); // 切换回初始的未过滤数据
}
```

图 22.45 允许用户浏览所有联系人。

## 22.10 工具和网络资源

我们在 www.deitel.com/LINQ 上的 LINQ 中心包含许多指向附加信息的链接，包括 Microsoft LINQ 团队成员的博客、示例章节、教程、视频、下载、常见问题、论坛、网络研讨会和其他资源网站。

学习 LINQ 的一个工具工具是 LINQCPad

```
http://www.linq.net
```

它允许你执行并查看任何 C# 或 Visual Basic 表达式的结果，包括 LINQ 查询。它还支持 ADO.NET Entity Framework 和 LINQ to Entities。

本章旨在介绍数据库、ADO.NET Entity Framework 和 LINQ to Entities。Microsoft 的 Entity Framework 网站

```
https://msdn.microsoft.com/en-us/data/aa937723
```

提供了关于使用 ADO.NET Entity Framework 和 LINQ to Entities 的大量信息，包括教程、视频等。

## 22.11结

本章介绍了关系数据库模型、ADO.NET Entity Framework、LINQ to Entities 以及用于处理数据库的 Visual Studio Visual编程工具。你检查了示例数据库的内容并学习了数据库中表之间的关系。你使用了 LINQ to Entities 和 IDE 生成的实体数据类来检索数据。

## 总结

### 22.1 引言

-   数据库是组织良好的数据集合。
-   数据库管理系统（DBMS）提供了存储、组织和修改数据的机制。
-   SQL Server 提供了许多功能，但也有某些限制。
-   ADO.NET Entity Framework 允许对 SQL Server 数据库进行操作。

### 22.2 关系数据库

-   关系数据库通过表来组织数据。
-   表由行和列（也称为字段）组成。
-   行的主键（或列的组合）可以唯一标识它。
-   由两个或多个列组成的主称为复合键。
-   每个列代表一个数据属性。
-   行在表中通过主键是唯一的。

### 22.3 关于数据库

-   数据库表、字段及其之间的关系统称为数据库模式。
-   外键是一个表中的列，匹配另一个表的主键。
-   在创建数据库表时指定的的外键连接了多个表的数据。
-   每个外键值必须出现在另一个主键中，以确保外键有效。
-   外键还允许从这些表中选择数据——这被称为连接（joining）。
-   主键与相应的外键之间存在一对多的关系——外键在自己的表中可以出现多次，但在另一个表中仅出现一次。
-   实体关系（ER）图显示了数据库中的表及其关系。
-   每行必须在主列有一个值，且键的值在表中是唯一的。

### 22.4 LINQ to Entities 和 ADO.NET Framework

-   通过 ADO.NET Entity Framework，你通过 IDE 在添加 ADO.NET Entity Model 时生成的类与数据库交互。
-   IDE 为表创建两个类。第一个类表示表的一行以及每个表列的属性。该类的对象称为行，存储单行数据。IDE 使用表复数名的单数形式作为行类的名称。第二个类表示表本身。该类的对象存储行的集合。
-   实体数据模型在 IDE 中具有完整的 IntelliSense 支持。
-   行类中的导航属性表示表之间的关系。
-   DbContext（命名空间 System.Data.Entity）管理程序和数据库之间的数据流。当 IDE 生成实体模型的行和表类时，它还会创建一个特定于所操作数据库的 DbContext 派生类。该类包含表的属性。
-   DbContext 管理的数据更改可以使用 DbContext 的 Changes 方法保存到数据库。

