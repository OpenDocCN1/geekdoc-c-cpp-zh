
摘要 977

- LINQ to Entities 通过 `IQuery<T>` 接口实现，该接口继承自 `IEnumerable<T>`。当针对 `IQuery<T>` 对象执行 LINQ 查询以访问数据库时，结果将加载到相应的实体模型类对象中，以便在您的代码中方便使用。
- 与 LINQ to Entities 使用的扩展方法定义为 `Queryable<>`（命名空间 System.Linq）的静态方法，并适用于任何实现 `IQuery<T>`的接口的对象——包括实体数据模型对象和 LINQ to Entities 查询的结果。

## 第 22.5 节 使用 LINQ 查询数据库

- IDE 提供了可视化编程工具和向导，简化了项目中的数据访问。这些工具建立了数据库连接并创建了对象，以便通过 GUI 方便地查看和操作数据——这种技术被称为绑定（binding）。
- GridView（命名空间 System.windows.Forms）以表格格式显示来自数据源的数据。
- BindingNavigator 是一个控件集合，允许你在 GUI 中的的记录之间进行导航。BindingNavigator 还允许你添加记录、删除记录并将更改保存到数据库中。

### 第 22.5.1 节 创建 ADO.NET 实体数据模型类库

- 实体数据模型描述了你将操作的 C# 类。
- 要与数据库交互，请向项目添加 ADO.NET 实体数据模型（通常是一个用于复用的类库）。这还将配置到数据库的连接。
- ADO.NET 实体数据模型的 `.edmx` 文件包含有关实体模型的信息。
- 在配置模型时，你会创建到数据库的连接并从数据库中选择模型的内容。
- 实体连接字符串包含了 ADO.NET Entity Framework运行时连接数据库所需的信息。
- 实体数据模型包含选定的数据库对象，并显示了它们之间的关系。

### 第 22.5.2 节 创建 Windows Forms 项目并将其配置为实体数据模型

- 要使用类库中的实体数据模型类进行数据绑定，你必须先向项目添加该类库的引用。你还需要添加对 `EntityFramework` 库的引用。
- 每个使用实体数据模型的应用程序都需要 Framework 库。
- 每个使用实体数据模型的应用程序还需要连接字符串，用于告诉 Framework 如何连接到数据库。连接字符串存储在定义该实体数据模型的 `App.Config` 文件中，必须复制到任何使用该实体数据模型的项目的 `App.Config` 文件中。

### 第 22.5.3 节控件与实体数据模型之间的数据绑定

- 你必须编写代码使自动生成的 GUI 与实体数据模型交互。
- 要使用实体数据模型类进行数据绑定，首先通过 Visual Studio 的“数据源”（Data sources）将它们作为数据源添加。实体数据模型类用于创建表示数据库中表的对象，因此请使用 Object 数据源。

- 表格的默认 GUI 是 `DataGridView`，其列名代表数据源对象的所有属性。IDE 还会创建一个 `BindingNavigator`，其中包含用于在条目之间移动、添加条目、删除条目以及保存更改到数据库的按钮。IDE 还会生成 `BindingSource`，它处理数据源与 Form 上数据绑定控件之间的数据传输。

- 非视觉化组件（如 `BindingSource` 和导航器的非平凡部分）会显示在组件树中——设计视图中 Form 下方的灰色区域。

- IDE 根据数据源的名称命名 `BindingNavigator` 和 `BindingSource`。

- 要编辑在 `DataGridView` 中显示的列，右键单击它，然后选择“编辑列...”（Edit Columns...）来删除。

- 要完成数据绑定，你必须创建一个实体模型 `DbContext` 对象并使用它来获取数据。

- `OrderBy` 扩展方法接收一个 `Func` 委托，并根据委托返回的值升序排列行。

- `ThenBy` 扩展方法接收一个 `Func` 委托，并允许你通过额外的列对结果进行排序。

- `Load` 扩展方法（定义在命名空间 System.Data.Entity 的 `DBExtensions` 中）将数据加载到内存中。这些数据在本地内存内存中被跟踪，以便任何数据的更改最终都能保存到数据库。

- `DbContext` 属性的本地属性是一个 `ObservableCollection<T>`，代表内存中的数据。

- 当 `BindingSource` 的 `DataProperty` 被赋值为 `ObservableCollection<T>`（命名空间 System.Collections.ObjectModel）时，绑定到 `BindingSource` 的 GUI 会收到数据更改通知，以便准确更新 GUI。此外，用户对 GUI 中数据所做的更改将由 `DbContext` 跟踪，最终可以将这些更改保存到数据库。

- 在 `BindingSource` 上调用 `EndEdit` 会强制将其任何更改保存到 `DbContext` 模型中。

- 在 `DbContext` 对象上调用 `SaveChanges` 将更改保存到数据库。

## 第 26.2 节 动态绑定查询结果

- IDE 创建的数据绑定在每次 `BindingSource` 的 `DataSource` 变化时都会自动更新 `DataGridView`。

- `BindingSource` 的 `MoveFirst` 方法将 `Position` 属性设置为 0，移动到数据源的第一行。

- 在 `ObservableCollection<T>` 上调用 `OrderBy` 返回一个 `IOrderedEnumerable<T>`。

- `where` 扩展方法必须返回一个 `bool` 值的 `Func` 委托，指示委托的参数是否符合指定标准。

## 第 22.7 节 使用 LINQ 从多个表中检索数据

- 要连接多个表，你可以使用实体模型中包含的数据库表之间外键关系的属性。这些属性允许你轻松访问其他表中的相关结果。

- 大多数查询返回以关系型行和列排列的结果。通过 LINQ to Entities，你可以创建返回层次结构结果的查询，结果中的每个项都包含其他项目的集合。

## 术语 979

- 匿名类型的所有属性都是公共且只读的。
- 你通过隐式类型局部变量引用匿名类型。
- 匿名类型自动生成的 `Equals` 方法比较调用方法的匿名对象和它接收的匿名对象的属性。

## 第 22.8 节 创建主/详细视图应用程序

- 在主/详细视图中，GUI 的一部分（主视图）允许你选择条目，另一部分（详情）显示该条目的详细信息。

- IDE 允许你指定从“数据源”窗口将对象拖放到 Form 上时它将创建的控件类型。要执行操作，请点击“数据源”窗口中的数据源对象节点——它将变为一个下拉列表，你可以从中选择在 GUI 上使用的控件。“详情”（Details）选项表示 IDE 将生成代表数据源对象每个列的标签-文本框。

- 从“数据源”窗口向数据源对象拖动属性将创建一个 `BindingSource` 以及其在另一个表中的 GUI，并且它们与该数据源对象关联。此 `BindingSource` 中的项会根据当前选择的主对象自动更新。

## 第 22.9 节 电话录案例研究

- 你不能直接将 LINQ to Entities 查询的结果绑定到 `BindingSource` 的 `DataSource`。
- 当你将查询转换为 `List` 时，只有对 `DbContext` 记录的更改会被跟踪——你在 `List` 中查看过滤数据时添加或删除任何内容都将被跟踪。

## 术语

Func 委托 数据库表的标识列 IQueryable<T> 接口 数据库表连接 LINQ to Entities 扩展方法类 Extensions 多对多关系 主/详细视图 SQL Server Express MoveFirst 方法类类 BindingSource 导航属性 对象数据 ObservableCollection<T> 类 一对多关系 OrderBy 扩展方法类 Queryable 主键 Queryable 关系型数据库 行 数据库行 SaveChanges 方法类 Db 智能标签菜单

