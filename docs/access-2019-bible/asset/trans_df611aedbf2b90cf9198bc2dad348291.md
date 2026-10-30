

# 图 28.1

对象浏览器提供了一个查看对象属性和方法的方式。

库下拉列表

属性

![](img/1e45673ab6eca9d20e67635ff5b9b318_947_0.png)

所选对象

方法语法

方法

对象浏览器使用起来很简单。从左上角的下拉列表中选择一个库（例如 DAO）；然后在浏览器的左侧滚动对象列表以找到感兴趣的对象。选择一个对象会在右侧列表中填充该对象的属性、方法和事件（如果适用）。单击属性、方法或事件会在列表下方区域显示该项目的语法。

尽管对象浏览器不显示具体的代码示例，但通常看到与属性、方法或事件关联的语法就足以让你开始编写 VBA 代码，或澄清对象的细节。

## 理解 DAO 对象

DAO 是默认的 Access 数据访问对象模型。DAO 自 Access 诞生之初就包含在其中，Microsoft 一直在更新 DAO 以跟上 Access 数据库引擎的变化。

DAO 对象以层次结构排列。某些对象从属于其他对象，并且在没有其父对象的实例的情况下无法存在。顶层的 DAO 对象是 DBEngine，所有其他 DAO 对象都是 DBEngine 的后代（见图 28.2）。

本节后面将描述最常用的每个 DAO 对象。

一般来说，DAO 层次结构紧密遵循 Access 数据库对象的排列方式。例如，Access 表（即 TableDef 对象）包含字段（每个字段都是一个 Field 对象）。字段有一组属性，用于指定其数据类型、默认值、验证规则等的细节。

# 图 28.2

DAO 对象模型。

![](img/1e45673ab6eca9d20e67635ff5b9b318_948_0.png)

NOTE
为了清晰起见，图 28.2 中省略了每个 DAO 对象关联的属性集。但你可以放心地假设图 28.2 中的每个对象都包含许多属性。

每个 DAO 对象还具有适合其对象类型的属性集合。TableDef 对象可能与 QueryDef 有一些共同的属性，但每个对象都有其对象类型独有的属性。虽然 QueryDef 和 TableDef 对象都有 Name 属性，但只有 QueryDef 具有 SQL 属性。方法也是如此。每个 DAO 对象都有只有它才能执行的操作。例如，由 QueryDef 定义的操作查询具有 Execute 方法，但 TableDef 没有。学习哪些属性和方法适用于每个 DAO 对象可能是 Access 开发人员面临的最大挑战。

> NOTE
> 当你阅读以下各节时，你会注意到每个数据类型访问对象的讨论中都省略了细节。由于每个 DAO 对象关联的众多属性和方法，以及这些对象在 Access 应用程序中的多种使用方式，因此在一章中不可能详细描述整个 DAO 对象模型。相反，本书在各处给出了使用 DAO（和 ADO）的具体方式的示例。请参阅索引以查找本书中讨论特定数据访问对象的章节和部分。

> NOTE
> Access 2007 引入了 ACE（Microsoft Access Engine），它是 Office 产品的新数据库引擎。ACE 是 Access 2007 至 2019 支持附件和多值字段等高级功能的原因。由于新的数据类型，ACE 需要 DAO 的更新版本（称为 ACEDAO）来支持新功能。DAO 与 ACEDAO 之间最大的区别是引入了 Recordset2 和 Field2 对象以及支持 Access 2007 引入的功能所需的新属性和方法。本章中的示例使用 ACEDAO，但为了简单起见，数据访问模型仍称为 DAO。Access 2003 MDB 格式仅支持 DAO 3.6，不支持 ACEDAO。

## DAO DBEngine 对象

DBEngine 对象，即代表 ACE 引擎的对象，位于 DAO 层次结构的顶端。它不是任何集合的成员，所有集合都是 DBEngine 的子对象。只有一个实例，并且它是少数几个你无法自行创建的数据访问对象之一。你在启动 Access 并发出 DAO 操作时打开 DBEngine 对象。它具有相对较少的属性和方法。对于属性更改要生效，必须在执行数据访问对象操作之前发出；否则，你会收到错误。由于 DBEngine 位于层次结构的顶部，你几乎总是以 DBEngine 开始 DAO 代码序列。

## DAO Workspace 对象

Workspace 对象代表每个使用 Access 的用户的一个打开的活动会话。所有数据库都在工作区中打开，要么作为默认数据库会话，要么使用 DBEngine 对象的 CreateWorkspace 方法创建的会话。

> **TIP**
> 
> 如果你选择在应用程序中使用事务跟踪（`BeginTrans`、`.EndTrans`），这些语句将包括当前工作区中打开的所有记录。如果你不想对特定记录集使用事务，请创建一个新的工作区，并在新的 Workspace 对象中打开记录集。

安全性也是从 Workspace 对象实现的（但仅适用于 MDB 文件格式）。Workspace 对象可用的安全方法允许你创建自己的安全接口和例程。如有必要，你可以使用 Workspace 对象的 CreateUser 或 CreateGroup 方法创建用户或组。

## DAO Database 对象

Database 对象代表一个打开的 Access 文件。Access 能够直接打开多种不同的数据库格式。当你直接使用 ACE 或 Jet 数据库引擎工作时，你的数据库可能是许多来源中的任何一个，例如另一个 ACCDB 或 ODBC 数据源。区别在于你如何设置数据库对象变量。

以下代码引用当前打开的 Access 数据库：

```
Dim daDb As DAO.Database
Set daDb = CurrentDb
```

CurrentDb 是 Access Application 对象的 方法，它代表整个 Access 环境及其所有对象。CurrentDb 是访问用户当前正在使用的数据库的快速、简便的方法。

也可以打开当前数据库 *之外* 的 Access 数据库：

```
Dim daDb As DAO.Database
Set daDb = OpenDatabase("C:\Northwind.mdb")
```

请注意，OpenDatabase 方法接受现有 MDB 或 ACCDB 文件的路径。OpenDatabase 方法可能会失败，具体取决于外部 Access 数据库是否可用或其当前状态是否阻止从另一个 Access 应用程序打开。

如果你在项目中混合使用 DAO 和 ADO，请确保为 DAO 对象类型声明加上 DAO 前缀，以便 Access 在设置对象时清楚使用哪个库。如果你只使用 DAO，则不需要使用库名称（在前面的示例中只需 Dim daDb As Database），但一些开发人员为清晰起见会包含它。本书中的示例通常会包含库名称前缀。

> **NOTE**
> 
> ACEDAO 对象使用 DAO 作为前缀，就像 DAO 3.6 对象一样。

## DAO TableDef 对象

DAO TableDef 对象代表 Access 数据库中的一个表。该表可能属于当前数据库，也可能链接到外部源。以下过程（包含在 Chapter28.accdb 示例数据库中）创建一个名为 MyTempTable 的新表，为其添加三个文本字段，并将该表添加到当前数据库的 TableDefs 集合中。

```
```vb
Public Sub CreateNewTableDef()

    Dim daDb As DAO.Database
    Dim taDtf As DAO.TableDef

    Const sTABLENAME As String = "MyTempTable"

    Set daDb = Application.CurrentDb

    'Delete an existing table, but ignore the error
    'if table doesn't exist
    On Error Resume Next
        daDb.TableDefs.Delete sTABLENAME
    On Error GoTo 0

    ' Create a new TableDef object:
    Set taDtf = daDb.CreateTableDef(sTABLENAME)

    With taDtf
        ' Create fields and append them to the TableDef
        .Fields.Append .CreateField("FirstName", dbText)
        .Fields.Append .CreateField("LastName", dbText)
        .Fields.Append .CreateField("Phone", dbText)
    End With

    ' Append the new TableDef object to the current database:
    daDb.TableDefs.Append taDtf

    daDb.Close
    Set daDb = Nothing

End Sub
```
```

在 Chapter28.accdb 数据库中运行此代码会创建一个名为 MyTempTable 的新表，这是数据库的永久添加。请注意，CreateNewTableDef 过程会在创建新 TableDef 之前删除此表（如果存在）。如果数据库中已存在同名表，Access 将无法将新的 TableDef 对象附加到其 TableDefs 集合中。

