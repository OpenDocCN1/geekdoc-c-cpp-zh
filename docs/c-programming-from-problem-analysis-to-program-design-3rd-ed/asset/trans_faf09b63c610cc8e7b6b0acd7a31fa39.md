
窗体上的内容可以绑定到 BindingSource 对象，而不是实际数据源。

工具条中已自动编入许多功能。首次实例化 BindingNavigator 控件时，导航的“移到第一项”“移到最后一项”“向前”和“向后”箭头均可正常工作。这段代码也是在将 DataGridView 控件拖放到窗体上时自动生成的。

### 示例 14-23

```csharp
private void studentBindingNavigatorSaveItem_Click(object sender, EventArgs e)
{
    this.Validate();
    this.studentBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll(this.studentDataBaseDataSet.Student);
}
```

## TableAdapterManager

示例 14-23 所示方法中的最后一条语句调用了 TableAdapterManager 类的 UpdateAll() 方法。你在本章前面已经了解到，数据适配器如何与数据集一起使用，通过断开式架构更新数据库。数据集与实际数据库之间的交互通过数据适配器或表适配器对象的方法来控制。请注意，图 14-20 所示组件栏中的五个对象之一是 TableAdapterManager。在 Visual Studio 2010 中，在项目中创建数据集时会生成一个 TableAdapterManager 对象。当应用程序从两个或多个表中拉取数据时，TableAdapterManager 非常有用。它使用外键关系来检索和保存相关数据表中的数据。

数据适配器或表适配器从数据源（数据库）填充数据集，然后使用其更新方法将更改发送回数据库。数据适配器和表适配器将数据从数据库读入数据集，然后将数据集中的已更改数据写回数据库。它们使用 SELECT、INSERT、DELETE 和 UPDATE SQL 语句完成此操作。

## TableAdapters

在前面关于编写程序语句以使用数据集和数据适配器更新数据库的讨论中，我们提到，在设置 DataAdapter 类的 SelectCommand 属性后，可以使用 CommandBuilder 类生成用于更新的 SQL 语句。另一种方法是使用 TableAdapter 的 SelectCommand、InsertCommand、UpdateCommand 和 DeleteCommand 属性。每个属性的 CommandText 都可以设置为一个 SQL 查询。为使 TableAdapter.Update() 方法正常工作，它必须具有可用的 SQL INSERT、DELETE 和 UPDATE 命令。根据与用户的交互，会执行其中一个或多个命令。如果数据被修改，则使用 UPDATE SQL 命令。当记录被删除时，则使用 DELETE SQL 命令。TableAdapter 的 Update() 方法在被调用时确定要使用哪个（些）命令。

当你将 DataGridView 控件拖放到窗体上时，放置在组件栏中的五个对象之一是 studentTableAdapter。TableAdapter 是由设计器生成的组件，从技术上讲并不属于 ADO.NET，但与数据适配器一样，它们在应用程序和数据库之间提供通信链接。它们提供数据适配器的全部功能。它们还具有内置的连接对象，并允许你在“属性”窗口中手动配置 InsertCommand、UpdateCommand 和 DeleteCommand SQL 查询。

![](img/e33ae760e23d89eac66541252ad65de8_909_0.png)

如果在组件栏中选择 TableAdapter 对象并查看其属性，将看不到 SelectCommand、InsertCommand、UpdateCommand 和 DeleteCommand 属性。需要使用数据集设计器查看和修改这些属性的 CommandText。

## 数据集设计器

Visual Studio 中提供了数据集设计器工具，可用于处理 DataSet 对象。数据集设计器可用于扩展数据集的功能。它还用于创建和修改数据适配器、表适配器及其查询。要启动设计器，请在解决方案资源管理器窗口中双击某个数据集，或者在数据源窗口中右键单击该数据集。将呈现数据集和表适配器的可视化表示，如图 14-21 所示。

![](img/e33ae760e23d89eac66541252ad65de8_910_0.png)

图 14-21 已打开的数据集设计器

在 **解决方案资源管理器** 窗口中双击 **StudentDatabaseDataSet.xsd** 文件即可打开数据集设计器。图 14-21 所示的 **属性** 窗口显示了 **StudentTableAdapter** 对象。**StudentTableAdapter** 对象已在数据集设计器中被选中。请注意，其中有名为 **InsertCommand**、**DeleteCommand**、**UpdateCommand** 和 **SelectCommand** 的属性。当 **DataGridView** 对象被拖放到窗体上时，SQL 命令已与这些属性中的每一个相关联。

## 查看 TableAdapter 的命令属性

**StudentTableAdapter** 对象已经有与用于检索和更新数据集表的 SQL 命令相关联的值。展开四个 SQL 命令（**SelectCommand**、**InsertCommand**、**DeleteCommand** 和 **UpdateCommand**）的每个属性时，会显示另外三行，如图 14-22 所示。将显示 **CommandText**、**CommandType** 和 **Parameters** 选项。你可以使用 **查询生成器** 为每个 **CommandText** 编辑或编写新的 SQL 语句。

![](img/e33ae760e23d89eac66541252ad65de8_911_0.png)

图 14-22 更新 SelectCommand

如图 14-22 所示，第一个属性 **CommandText** 保存 SQL 语句。SQL 语句可以直接在此框中键入，也可以使用 **查询生成器** 生成。要打开 **查询生成器**，请单击 **CommandText** 值框。此时将出现一个省略号。单击该省略号即可启动生成器。

## 查询生成器

单击任意命令属性旁的值框，会打开一个下拉列表，其中包含 **Current**、**New** 和 **None** 选项。可以从 **Current** 和 **New** 启动查询生成器。如果选择 **New**，然后单击 **CommandText** 框中的省略号，系统会首先提示你选择要从中检索数据的表。如图 14-23 所示。

![](img/e33ae760e23d89eac66541252ad65de8_912_0.png)

图 14-23 确定要更新的表

添加 Student 表并关闭图 14-23 所示的对话框后，即可生成查询。你可以将 SQL 语句键入 SQL 窗格，或使用关系图窗格选择要更新的列。通常，会为更新选择所有列。中间的网格窗格用于筛选和输入参数化表达式。

## 参数

若要指示在运行时通过输入值来设置该列，可以创建参数化查询。对于在显示窗体时可能在运行时提供的值，对于 SQL Server 数据源，会在标识符前放置一个“at”符号（@）。对于 Access，使用问号（?）代替 @ 符号。在 Access 中，? 后不能跟标识符。

图 14-24 显示了使用查询生成器创建的 SELECT 语句。仅检索了 major_ID = 'CS' 的记录。

![](img/e33ae760e23d89eac66541252ad65de8_913_0.png)

图 14-24 SelectCommand 的 CommandText 属性值

SelectCommand 的 CommandText 如示例 14-24 所示。此 SQL 语句没有使用关系图窗格或网格窗格，而是直接键入到 SQL 窗格中。

### 示例 14-24

```sql
SELECT  student_ID, student_FirstName, student_LastName, major_ID,
        student_Phone
FROM Student
WHERE (major_ID = 'CS')
```

在查询生成器中，你可以通过选择“执行查询”按钮来测试 SQL 语句。如果有参数化值，将显示一个对话框，要求提供参数值。查询结果将显示回 **查询生成器** 窗口中的 **结果** 窗格。

你可以插入新行、修改现有数据，以及删除一行或多行。图 14-25 显示了应用程序运行期间用户界面的一些快照。

![](img/e33ae760e23d89eac66541252ad65de8_914_0.png)

**图 14-25** 使用配置工具的示例最终输出

如图 14-25 所示，Joshua Binkley 的姓名被更改。两条记录（Adam Jones 和 Brenda Shepherd）被删除，但插入了 Francisco 和 Manuel Alberto。单击 **保存** 按钮会调用 `tableAdapterManager.UpdateAll()` 方法，该方法使用表适配器的 `InsertCommand`、`DeleteCommand` 和 `UpdateCommand` 的 `CommandText` SQL 语句将更改写回数据库。图 14-26 显示了更新后的 Access 表。

![](img/e33ae760e23d89eac66541252ad65de8_914_1.png)

代码生成器通常会添加超出必要的代码。**UpdateCommand** 的 **CommandText** 被缩短为 `UPDATE Student SET student_ID = ?, student_FirstName = ?, student_LastName = ?, major_ID = ?, student_Phone = ? WHERE (student_ID = ?)`。对于最终的 ConfigToolsExample 解决方案，其他 **CommandText** 属性均未修改。

