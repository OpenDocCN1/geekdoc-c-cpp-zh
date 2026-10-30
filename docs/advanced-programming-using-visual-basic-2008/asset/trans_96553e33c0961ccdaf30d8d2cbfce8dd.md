

## 使用存储过程

在本节中，你将使用存储过程创建一个数据集。SQL Server 存储过程（SPROC）是一段 SQL 代码块，它与查询数据库一起存储，以便在需要时使用。存储过程比 TableAdapter 默认生成的查询代码更安全，而且通常运行得更快。黑客有时会通过在运行中的应用程序输入字段中输入 SQL 代码来渗透包含 SQL 查询的应用程序。这种称为 SQL 注入的技术可能使某人获得对数据库的非预期访问权限。使用存储过程则不可能发生 SQL 注入，因为代码包含在 SQL Server 环境内部，而不是应用程序代码中。

存储过程通常比程序中的查询运行得更快，因为存储过程以编译形式存储。作为源代码发送到数据库的查询每次发送时都必须编译。

## 在 VS IDE 中创建存储过程

你可以使用服务器资源管理器在 Visual Studio IDE 中直接创建 SQL Server 存储过程。服务器资源管理器通常与工具箱停靠在一起；你可以通过选择“视图 / 服务器资源管理器”来显示它。

在“数据源”窗口之外，你还可以在服务器资源管理器中查看和添加连接。服务器资源管理器显示你定义的所有连接，以及每个数据库中所有可用的对象。你不能像在“数据源”窗口中那样将表和字段从服务器资源管理器拖到窗体上。但要创建新的存储过程，你必须使用服务器资源管理器。

你可以展开服务器资源管理器中的每个连接以显示表、视图和存储过程。如果你安装了 Microsoft 的任何示例数据库，它们都有存储过程，如果你愿意，可以查看它们。Pubs 数据库已经有一些存储过程（图 3.27）；在下一节中，你将添加一个新的存储过程。

要创建新的存储过程，请右键单击数据库的“存储过程”文件夹，然后选择“添加新存储过程”。将创建一个默认名为 StoredProcedure1 的新过程，其中包含帮助你创建该过程的注释。在下一节中新过程的列表中，

### 图 3.27

服务器资源管理器显示数据库连接。你可以展开每个节点以查看数据库中已存储的表、视图和存储过程。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_154_0.png)

注释遵循 C# 格式：/* 开始注释块，*/ 结束注释块。因此，在空过程中，唯一不是注释的行是

```
CREATE PROCEDURE
AS
RETURN
```

## 空存储过程

以下是一个新的空存储过程，你将根据自己的目的对其进行修改。

```
CREATE PROCEDURE dbo.StoredProcedure1
/*
{
@parameter1 int = 5,
@parameter2 datatype OUTPUT
}
*/
AS
/* SET NOCOUNT ON */
RETURN
```

将你的 SQL 语句放在 AS 和 RETURN 之间，并按你的意愿命名过程：

```
CREATE PROCEDURE GetEmployees
AS
SELECT emp_id, fname, lname, hire_date
FROM employee
ORDER BY lname
RETURN
```

## 使用存储过程检索数据

从存储过程向窗体添加网格或详细信息视图与使用表几乎相同。在“数据源”窗口中，选择“添加新数据源”以显示“数据源配置向导”。按照与任何连接相同的步骤操作，但展开“数据库对象”下的“存储过程”项，并勾选你创建的过程。`CREATE PROCEDURE` 子句后面的名称会出现在列表中。

假设你使用名为 GetEmployees 的存储过程创建数据源，则 TableAdapter 变为 GetEmployeesTableAdapter，数据集为 PubsDataSet。在 Form_Load 事件处理程序中自动生成的 Fill 方法将是

```
Me.GetEmployeesTableAdapter.Fill(Me.PubsDataSet.GetEmployees)
```

## 反馈 3.3

- 1. 按 ZIP 码对数据库数据进行排序的两种技术是什么？
- 2. 列出创建一个组合了 City、State 和 ZIP 字段的表达式字段的步骤。

## 多层架构

既然你已经使用过 DataSet 对象、TableAdapter 和 SQL，现在是时候将项目分离为多个层了。在可能的情况下，你应该将数据库访问与用户界面分开。对于多层应用程序，我们将创建一个数据组件作为单独的层。数据组件将包含 DataSet 及其 TableAdapter，以及将数据返回给表示层的方法（图 3.28）。当你构建了良好的数据层时，你可以在具有各种用户界面的多个项目中使用该组件。

到目前为止，你一直使用 VS 可视化设计器来创建数据库访问对象。当你将对象拖到窗体上时，可视化设计器会自动创建所有必要的代码。在本节中，你将学习声明和实例化 DataSet 和 TableAdapter 对象，以及在代码中将数据库对象绑定到窗体控件。

你会发现，大多数专业应用程序在代码中执行数据库访问，而不是使用可视化设计器。当你为数据库访问创建单独的类时，你必须编写绑定控件的代码。

## 创建数据层组件

要创建数据层组件，你需要在项目中添加一个新类，并编写代码来创建和填充 DataSet。你还需要至少一个方法让窗体检索 DataSet。在后面的章节中，你将添加用于更新 DataSet 的方法。

对于 Windows 应用程序，你将启动一个新应用程序，并使用“数据源”窗口添加新的数据源。此步骤为 DataSet 和 TableAdapter 创建架构类，但不会创建实际的 DataSet 或 TableAdapter 对象。（在之前的项目中，DataSet 和 TableAdapter 对象是在你将数据拖到窗体时创建的。）

在将 DataSet 声明为数据源后，你可以在新类中编写代码来声明、实例化、填充和返回 DataSet。在查看下一节中的解释之前，先看一下代码。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_156_0.png)

### 图 3.28

> 好的应用程序通常将用户界面与数据访问分开。

## 代码

```
Public Class PubsEmployeeData
' Declare class-level variables.
Private AnEmployeeTableAdapter As PubsDataSetTableAdapters.employeeTableAdapter
```

```
Private APubsDataSet As PubsDataSet

Public Function GetEmployeeDataset() As PubsDataSet
' Fill and return the DataSet.

Try
' Instantiate the TableAdapter and DataSet.
AnEmployeeTableAdapter = _
New PubsDataSetTableAdapters.employeeTableAdapter
APubsDataSet = New PubsDataSet

' Fill the DataSet.
AnEmployeeTableAdapter.Fill(APubsDataSet.employee)
' Return the DataSet.
Return APubsDataSet
Catch ex As Exception
Throw ex
End Try
End Function
End Class
```

## 关于代码的说明

我们选择在类级别声明 TableAdapter 和 DataSet，即使它们仅在一个过程中使用，也可以声明为局部变量。在后面的章节中，你将向数据层类添加更多过程，并且需要在类级别拥有 TableAdapter 和 DataSet 对象。

如果 DataSet 和 TableAdapter 的声明令你困惑，你可能会想查看 DataSet 设计器自动生成的代码。如果你在解决方案资源管理器中选择“显示所有文件”，你可以看到并打开 PubsDataSet.xsd 文件的 PubsDataSet.Designer.vb 文件。设计器生成的文件包含多个用于处理 DataSet 的类，还有一个名为 PubsDataSetTableAdapters 的新命名空间和一个名为 employeeTableAdapter 的类。你使用以下语句实例化的正是这个类：

```
Private AnEmployeeTableAdapter _
As PubsDataSetTableAdapters.employeeTableAdapter

AnEmployeeTableAdapter = New PubsDataSetTableAdapters.employeeTableAdapter
```

`Throw ex` 语句会将任何异常传回给调用过程，以便可以在窗体中处理该异常。

## 编写窗体的数据库对象代码

在数据库应用程序的窗体中，你必须编写代码来实例化数据层组件、检索 DataSet 并绑定窗体的控件。实例化数据层组件的代码与你用来实例化第 2 章中业务类的代码类似。

```
' Create an instance of the data-tier component.
Dim APubsEmployeeData As New PubsEmployeeData
' Retrieve the dataset from the data tier.
Dim APubsDataSet As PubsDataSet
APubsDataSet = APubsEmployeeData.GetEmployeeDataset()
```

