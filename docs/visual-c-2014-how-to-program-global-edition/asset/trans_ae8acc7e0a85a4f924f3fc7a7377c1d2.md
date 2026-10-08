
# 第 22 章 数据库与 LINQ

用于对结果排序。在这种情况下，我们传递了一个 lambda 表达式，它定义了一个匿名方法，其中：

- 参数 `author`（`Author` 实体数据模型类的对象）被传递给方法，并且
- lambda 表达式的返回值（=>）——在此情况下为作者的 `LastName`——由方法隐式返回。

Lambda 表达式从 `dbcontent.Authors`（包含 `Author` 对象）推断出 `author` 的类型，并从 `author.LastName` 推断出作者的返回类型（`string`）。当有多个同名的作者时，我们希望他们也能按名字升序列出。`ThenBy` 扩展方法

```csharp
.ThenBy(author => author.FirstName)
```

允许你根据额外的列进行排序。这应用于已经按姓排序的 `Author` 对象。与 `OrderBy` 一样，`ThenBy` 也接收一个用于对结果排序的 `Func` 委托。

最后，30 行调用了 `Load` 扩展方法（定义在 `System.Data` 命名空间下的 `DbExtensions` 类中）。该方法执行查询并将结果加载到内存中。这些数据由本地内存中的 `BookEntities DbContext` 跟踪，以便可以将数据的任何更改最终保存到数据库。27–30 行等同于使用以下语句：

```csharp
from author in dbcontent.Authors
orderby author.LastName,author.FirstName
select author.Load();
```

33 行将 `BindingSource` 的 `DataSource` 属性设置为 `DbContext` `Authors` 对象的 `Local` 属性。在这种情况下，`Local` 属性是一个 `ObservableCollection<Author>`——它返回由 27–30 行加载到内存中的查询结果。当 `BindingSource` 的 `DataSource` 属性被分配 `ObservableCollection<T>` 时，绑定到该 `BindingSource` 的 GUI 将被通知，用户对 GUI 进行的任何更改都将由 `DbContext` 跟踪，并最终可以将这些更改保存到数据库。

authorBindingNavigatorItem_Click 事件处理程序：将修改保存到数据库
如果用户修改了 `DataGridView` 中的数据，我们也希望将修改保存到数据库中。默认情况下，`BindingNavigator` 的 `Data` 按钮是禁用的。要启用它，点击 `BindingNavigator` 中的此按钮图标并选择 `Enabled`。然后，双击图标以创建其 `Click` 事件处理程序，并在方法体中添加代码（第 41–53 行）。

将 `DataGridView` 中输入的数据写回数据库是一个三步过程。首先，通过调用继承的方法对表单控件进行验证（第 41 行）——如果任何控件具有 `Validating` 事件的事件处理程序，它就会执行。你通常处理此事件以判断控件的内容是否有效。接下来，第

# 22.6 动态绑定查询结果

42 行在 `authorBindingSource` 上调用了 `EndEdit`，这会强制它将任何待处理的更改保存到内存中的 `BooksEntity` 模型中。最后，47 行在 `BooksEntity` 上下文中调用 `SaveChanges` 以将任何更改存储到数据库中。我们将此调用放置在 `try` 语句中，因为 `Authors` 表不允许名字和姓氏为空值——这些规则是在我们最初创建数据库时配置的。当调用 `SaveChanges` 时，存储到 `Authors` 表中的任何更改必须满足表的规则。如果不符合，则会发生 `DBEntityValidationException`。

# 22.6 动态绑定查询结果

接下来我们展示如何执行多个不同的查询并在 `DataGridView` 中显示结果。此应用程序仅从实体模型中读取数据，因此我们禁用了 `BindingNavigator` 中的按钮，以便使用户添加和删除记录——只需选择每个按钮并在属性窗口中将其 `Enabled` 属性设置为 `False`。稍后，我们将解释为什么我们在这个示例中不支持修改数据库。

`Display Query Results` 应用程序（图 22.23–22.25）允许用户从窗口底部的 `ComboBox` 进行查询，该框显示查询结果。

![](img/57baed2319be0bb1b5f98674846f2711_955_0.png)

图 22.23 | `Display Query Results` 应用程序 `All` 查询的结果，显示了按书名排序的 `Titles` 表的内容。

![](img/57baed2319be0bb1b5f98674846f2711_955_1.png)

图 22.24 | `Display Query Results` 应用程序 `Titles` 带 `2016 copyright` 查询的结果。

# 第 22 章 数据库与 LINQ

![](img/57baed2319be0bb1b5f98674846f2711_956_0.png)

图 22.25 | `Display Query Results` 应用程序以 "How to query" 结尾的 `Titles` 查询结果。

# 22.6.1 创建 Display Query Results GUI

执行以下步骤构建 `Display Query Results` 应用程序的 GUI。

### 步骤 1：创建项目
按照 22.5.2 节中的步骤操作，在与 `DisplayTable` 相同的解决方案创建一个名为 `DisplayQueryResult` 的新 Windows Forms 项目。将 `Form1.cs` 源文件重命名为 `TitleQueries.cs`。将 Form的 `Text` 属性设置为 `Display Query Results`。确保添加对 `BooksExample` 和 `EntityFramework` 库的引用，向 `App.Config` 文件添加连接字符串，并将 `DisplayQueryResult` 设置为启动项目。

### 步骤 2：创建用于显示标题的 DataGridView
按照 22.5.3 节中的步骤 1 和 2 创建数据源和 `DataGridView`。对于此示例，选择 `Title` 类（而不是 `Author`）作为数据源，并从 `DataGridView` 删除列，因为它将在使用。

### 步骤 3：在表单上添加 ComboBox
在设计视图中，在 `DataGridView` 下方添加 `ComboBox`。将 `ComboBox` 的 `Dock` 属性设置为 `Bottom`，将 `DataGridView` 的 `Dock` 属性设置为 `Fill`。接下来，向 `ComboBox` 添加所有查询名称。

智能标签允许你快速访问可能设置控件的常用属性（例如 `TextBox` 的 `Multiline` 属性），因此你可以在设计视图中直接设置这些属性，而不是在属性窗口中。当选中控件时，会出现控件右上角的智能标签菜单。在字符串集合编辑器中，为 `queryComboBox` 添加以下三项，对应我们要的每个查询：

# 动态查询结果

1. 所有标题
2. 2016 版权的标题
3. 以 "How to Program" 结尾的标题

# 22.6.2 编写 Display Query Results 应用程序

接下来你将为此编写代码（图 22.26）。

```csharp
// 图 22.26: TitleQueries.cs
// 在 DataGridView 中显示用户选择的查询结果。
using System;
using System.Data.Entity;
using System.Linq;
using System.Windows.Forms;

namespace DisplayQueryResult{
    public partial class TitleQueries : Form
    {
        public TitleQueries()
        {
            InitializeComponent();
        }
        // 实体 DbContext
        private BooksExample.BooksEntities dbcontext = new BooksExample.BooksEntities();

        // 从数据库加载数据到 DataGridView
        private void TitleQueries.Load(object sender, EventArgs e)
        {
            dbContext.Titles.Load(); // 加表到内存

        // 设置 ComboBox 显示从 Titles 表选择
        // 所有书籍的默认查询
        queriesComboBox.SelectedIndex = 0;

        // 根据用户选择将数据加载到 titleBindingSource
        private void queriesComboBox.SelectedIndexChanged(object sender, EventArgs e)
        {
            // 设置显示的数据为所选内容
            switch (queriesComboBox.SelectedIndex)
            {
                case 0: // 所有标题
                // 使用 LINQ 按标题排序书籍
                titleBindingSource.DataSource = dbContext.Titles.Local.OrderBy(book => book.Title);break;
            }
        }
    }
}
```

**图 22.26** | 在 DataGridView 中显示用户选择的查询。（第 I 部分，共 2 部分）。

