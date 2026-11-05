

- 7. 对于对数据库的简单只读访问，.NET 包含一个数据读取器类，可用于从数据库读取数据行。
- 8. OleDbDataReader 类允许从数据库只读、向前检索数据。数据不会缓存在内存中。默认情况下，实现 OleDbDataReader 类时，每次只在内存中存储一行。
- 9. 要使用数据读取器处理数据，需要声明一个 OleDbDataReader 类的对象，然后调用 OleDbCommand 类的 `ExecuteReader()` 方法来构建 OleDbDataReader 对象。
- 10. 若要将 OleDbDataReader 对象定位到检索到的第一条记录所在的行，可使用 OleDbDataReader 类的 `Read()` 方法。`Read()` 方法还用于在处理完上一条记录后前进到下一条记录。
- 11. 要理解使用 `Read()` 方法检索数据的处理过程，可以将使用数据读取器对象单次访问所检索到的内容想象成一个由该行字段组成的一维表。
- 12. 需要关闭读取器对象和连接对象以解锁数据库，以便其他人可以访问它。
- 13. ADO.NET 不要求保持与数据库的持续实时连接。这在 .NET 中是通过数据集实现的。数据集是从某个数据源检索到的记录的缓存，其中可能包含来自该数据源的一个或多个表。
- 14. 将 DataAdapter 对象与 `Fill()` 和/或 `Update()` 方法一起使用，无需再打开和关闭连接。当调用 `Fill()` 或 `Update()` 方法时，连接会自动打开和关闭。
- 15. 适配器用于在数据库源和数据集对象之间交换数据。
- 16. OleDbCommandBuilder 对象会自动生成用于更新数据库的 SQL 语句。它可用于涉及单个表的查询。
- 17. DataGrid 对象是一种划分为行和列的结构，可用于存储数据集对象。DataGrid 对象允许你更改值，或删除、插入新记录。
- 18. 要将 DataGrid 对象绑定到数据集，可使用 DataGrid 类的 SetDataBinding() 方法。
- 19. DataGridView 类提供类似 DataGrid 的控件，并增加了更多功能。自定义 DataGridView 控件的一种方法是单击其智能标记标志符号。
- 20. “数据源”窗口允许你将项（表和/或列）拖到窗体上。
- 21. 类型化数据集定义了一个架构，该架构将表及其列公开为对象属性。
- 22. DataSet 设计器使你可以设置表之间的关系，并向应用程序添加附加查询。
- 23. 若要在 Visual Studio 中创建新的 SQL Server 数据库，请使用“服务器资源管理器”窗口。若要添加表，请右键单击“表”，然后从快捷菜单中选择“添加新表”。选择“显示表数据”可预览数据。
- 24. 连接字符串可以保存到 App.config 文件中。
- 25. BindingNavigator 类通常与 BindingSource 控件配对使用，以便你能够浏览数据记录并与之交互。
- 26. TableAdapter 是设计器生成的组件，提供应用程序与数据库之间的通信链接。
- 27. DataSet 设计器用于创建和修改数据集、表适配器及其查询。若要启动该设计器，请在“解决方案资源管理器”窗口中双击数据集，或在“数据源”窗口中右键单击数据集。
- 28. 使用查询生成器编写 SQL SELECT、INSERT、DELETE 和 UPDATE 语句。
- 29. 与 SELECT 语句一起使用的 SQL INNER JOIN 子句使你可以从两个或多个表中检索结果。
- 30. 在 Access 中，使用 DataSet 设计器在表之间创建父子关系，以便能够从多个表中检索数据。
- 31. LINQ 使你可以使用语言关键字和熟悉的运算符针对强类型对象集合编写查询。
- 32. LINQ 提供查询功能，可用于关系数据源、XML 数据以及任何实现了 IEnumerable\<T\> 接口的数据类。
- 33. 大多数查询表达式以 from 子句开头，以 select 或 group 子句结尾。
- 34. 关键字 var 表示类型将由等号右侧的表达式确定。

## 习题

- 1. 数据库中多行多列数据的内存表示存储在哪类对象中？
  - a. 数据提供程序
  - b. 数据读取器
  - c. datagrid
  - d. dataset
  - e. 数据适配器

- 2. 以下各项中，哪一项不是 ADO.NET 数据提供程序的示例？
  - a. OLE DB
  - b. Oracle
  - c. ODBC
  - d. Sql Server
  - e. Access

- 3. 以下哪项是用于显示数据库数据的网格状结构的类名？
  - a. ComboBox
  - b. ListBox
  - c. DataGridView
  - d. Grid
  - e. GridData

- 4. 数据库将信息存储在记录、字段以及：
  - a. 数据提供程序
  - b. 网格
  - c. 列
  - d. 表
  - e. 命令

- 5. 每个数据提供程序附带的核心类包括以下所有类，除了：
  - a. Connection
  - b. DataAdapter
  - c. Command
  - d. DataSet
  - e. DataReader

- 6. 每个数据提供程序类按其以下内容进行分组和访问：
  - a. 命名空间
  - b. 数据库
  - c. datagrid
  - d. 提供程序
  - e. 系统

- 7. 以下哪条 SQL 语句可以从 customer 表中检索所有四列？
  - a. SELECT ALL FROM customer
  - b. SELECT * FROM customer
  - c. SELECT customer
  - d. SELECT , , , FROM customer
  - e. SELECT @ @ @ @ FROM customer

- 8. SQL Server SQL 语句的参数与 Access 数据库的参数写法略有不同。对于 SQL Server，参数使用以下方式指示：
  - a. @ 后跟标识符
  - b. @ 不带标识符
  - c. ? 后跟标识符
  - d. @ 不带标识符
  - e. params 关键字

- 9. 可以添加到 SELECT 语句中以从多个表检索数据的 SQL 子句是：
  - a. BETWEEN
  - b. INNER JOIN
  - c. CROSS CONNECTION
  - d. WHERE
  - e. UPDATE

- 10. 以下命名空间（System.Data.OleDB、System.Data.SqlClient、System.Data.Odbc、System.Data.OracleClient）包含用于不同……的类：
  - a. 数据提供程序
  - b. 文件流
  - c. ADO.NET 应用程序
  - d. 数据库
  - e. 数据读取器

- 11. 对于数据库的只读访问，使用哪个 ADO.NET 类？
  - a. DataSet
  - b. DataAdapter
  - c. CommandBuilder
  - d. Connection
  - e. DataReader

- 12. 要提供对 Access 数据库管理系统的访问，使用哪个数据提供程序？
  - a. System.Data.OleDb
  - b. System.Data.SqlClient
  - c. System.Data.Odbc
  - d. System.Data.OracleClient
  - e. Microsoft ACE.OLEDB.12.0

- 13. 哪个类与 dataset 类一起使用以方便使用断开连接的数据库？
  - a. DataAdapter
  - b. DataReader
  - c. Command
  - d. OleDbConnection
  - e. Fill

- 14. 为避免编写额外的 SQL 语句来更新实时数据库，应实例化哪个类的对象？
  - a. DataAdapter
  - b. DataReader
  - c. Connection
  - d. CommandBuilder
  - e. DataGrid

- 15. 要释放数据库以便其他应用程序可以使用它，应调用哪个方法？
  - a. ReleaseDb()
  - b. Release()
  - c. StopAccess()
  - d. Close()
  - e. 以上都不对

- 16. 要从数据库中检索特定记录，可以创建新查询并将其存储为使用 ________ 类的对象的方法。
  - a. Dataset
  - b. DataProvider
  - c. TableAdapter
  - d. Connection
  - e. Command

- 17. 哪个方法用于最初填充数据绑定控件？
  - a. Dataset Fill() 方法
  - b. Dataset Update() 方法
  - c. TableAdapter Fill() 方法
  - d. BindingNavigator Save() 方法
  - e. PageLoad() 事件处理方法

- 18. 在 Visual Studio 中，使你能够连接到数据库并使用 TableAdapter 对象自动填充 dataset 对象的工具是 ________ 向导：
  - a. 数据源配置
  - b. 数据源
  - c. 查询生成器
  - d. DataSet 设计器
  - e. TableAdapter 查询配置

- 19. 在 Visual Studio 中，哪个窗口用于显示数据集表，以便可以将它们拖放到窗体上？
  - a. 服务器资源管理器
  - b. 属性
  - c. DataSet 设计器
  - d. 数据源
  - e. 解决方案资源管理器

- 20. 连接字符串包含：
  - a. using 指令
  - b. 数据源的名称
  - c. 数据库管理系统的版本号
  - d. 数据库中的字段列表
  - e. 一条 SQL 语句

- 21. 解释 dataset、table adapter 和 datagrid 对象如何用于更新数据库。

