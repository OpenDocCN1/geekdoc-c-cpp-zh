

# 使用 Visual C#.NET 进行数据选择查询

BindingSource 组件。所有与数据的后续交互（包括导航、排序、过滤和更新）都是通过调用 BindingSource 组件完成的。

其次，BindingSource 组件可以作为强类型数据源。使用 `Add` 方法向 BindingSource 组件添加类型可以创建该类型的列表。

第三，BindingSource 控件充当桥梁的作用，将你的数据（`DataSet`）连接到 Visual C# 表单上的数据控件上。BindingSource 也可以被视为一个容器对象，并包含来自该源的所有映射数据。随着数据驱动过程的运行，BindingSource 将使用 `TableAdapter` 来自 `DataSet` 的数据。此外，BindingSource 控件将创建一组映射到 `DataSet` 中填充数据的数据。BindingSource 可以持有这组映射数据，并在 `DataSet` 和 `BindingSource` 之间建立一对一的连接。当你于 Visual C# 表单上的控件与 `DataSet` 中的数据之间执行数据绑定时，这种连接非常有用。事实上，当你需要将数据反映在关联控件上时，你设置了一个连接，即向 BindingSource 发出请求，由 BindingSource 控件来控制对数据源（`DataSet`）的访问以及这些控件中的数据更新。例如，当执行列排序操作时，`DataGridView` 会向 BindingSource 控件发送请求，后者将与数据源通信以完成此排序。

在 Visual Studio 中执行数据绑定时，你需要将 `BindingSource` 控件引用的数据绑定到控件的属性上。

## 5.1.1.4 BindingNavigator

BindingNavigator 允许用户按顺序选择和浏览在数据源（`DataSet`）中存储的所有记录。BindingNavigator 组件提供了一个带有按钮的标准 UI，并允许用户导航到数据中的第一条、上一条记录，以及下一条和最后一条记录。它还提供了文本框来显示当前数据表中存在多少记录以及当前记录的索引。

如图 5.2 所示，BindingNavigator 也绑定到 BindingSource 组件。当用户点击 BindingNavigator UI 上的“上一个”（Previous）或“下一个”（Next）按钮时，会向 BindingSource 发送获取上一个或下一条记录的请求，随后请求将发送到数据源以获取该数据。

## 5.1.1.5 TableAdapter

从图 5.2 可以发现，`TableAdapter` 等同于适配器（adapter），它仅作为数据库与 `DataSet` 之间的连接方法，以及 `BindingSource` 与 `DataSet` 之间的连接方法。这意味着 `TableAdapter` 在为不同目的担任不同角色时具有双重功能。例如，当你在使用 `TableAdapter` 的 `Fill` 方法使用 `DataSet` 开发数据驱动应用时；当 Visual C# 表单中的数据控件需要填充或更新时，`TableAdapter` 也作为适配器来协调 `BindingSource` 和 `DataSet` 之间的数据操作。

在 Visual Studio 2005 之前，Data Adapter 是 `DataSet` 及其与数据库之间的唯一纽带。如果需要对数据进行更改，你需要为 `DataSet` 中的每个表使用不同的 `TableAdapter`，并调用每个 Data Adapter 的 `Update` 方法。

`TableAdapter` 引入自 Visual Studio 2005，你无法在工具窗口（Tool Window）中找到它。`TableAdapter` 属于设计器生成的组件，用于连接你的 `DataSet` 对象与其底层数据库，当你添加和配置数据源（如 `DataSet` 配置向导）时，它会自动创建。

`TableAdapter` 与 Adapter 类似，因为这两个组件都可以处理 `DataSet` 和数据库之间的数据操作，但 `TableAdapter` 可以包含多个查询以支持数据库中的多个表，允许一个 `TableAdapter` 对你的 `DataSet` 执行多次查询。另一个点是，每个 `TableAdapter` 都是一个唯一的类，由 Visual Studio 自动生成，仅针对你为特定数据库选择的字段工作。

`TableAdapter` 类包含用于从你的数据库中选择数据的查询。此外，它还包含不同的方法，允许使用项目中的动态参数从数据库填充 `DataSet`。你还可以使用 `TableAdapter` 在不同的数据操作上构建如 `Insert`、`Update` 和 `Delete` 等不同的 SQL 语句。后续章节将通过真实示例提供 `TableAdapter` 的更详细探索和实现。

## 5.1.2 数据源窗口中的数据设计向导

从 Visual Studio 2005 开始，增加了两个集成开发环境（IDE）功能：数据源窗口（Data Sources Window）和数据源配置向导（Data Source Configuration Wizard），帮助使用新类（如 `DataConnector` 和 `DataAdapter`）设置数据访问。

数据源窗口用于显示项目中的数据源或可用数据库。你可以通过将数据源窗口中的项拖到项目中的 Visual C# 表单上，来创建用户界面（由数据绑定的控件组成）。数据源窗口中的每个项都有一个下拉控件列表，你可以通过将其拖到表单上来选择要创建的控件类型。你还可以使用额外的控件（例如你创建的控件）对控件进行自定义。

关于如何使用数据源窗口开发数据驱动项目的详细描述，请参阅第 5.4 节。

### 5.1.2.1 添加新数据源

在 Visual C# 2022 环境中首次创建新的数据驱动应用时，项目中尚未添加任何数据源，因此数据源窗口是空白的，没有数据源可显示。例如，你可以通过选择 `File | New | Project` 菜单项创建一个新的 Visual C# 2022 Windows ，并选择 `DataSource` 作为项目名称。项目创建并打开后，你可以通过点击菜单栏上的 `View | Other | Data Sources` 菜单找到并打开数据源窗口，如图所示。

