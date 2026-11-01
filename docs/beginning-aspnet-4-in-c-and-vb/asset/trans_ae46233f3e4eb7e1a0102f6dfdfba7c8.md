

![](img/d7d2ffa0a76feaab821930e95daace93_1190_0.png)

## 图 39-2

这个简单的应用程序从 Northwind 数据库的 Customer 表中选择所有记录，并在 DataGridView 控件中将这些记录显示给用户。以下代码片段展示了此示例的代码（不包括窗体和控件定义代码）：

```
using System;
using System.Configuration;
using System.Data;
using System.Data.Common;
using System.Data.SqlClient;
using System.Windows.Forms;

namespace DisplayTabularData
{
    partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void getData_Click(object sender, EventArgs e)
        {
            string customers = "SELECT * FROM Customers";

            using (SqlConnection con =
                   new SqlConnection(ConfigurationManager.
                       ConnectionStrings["northwind"].ConnectionString))
            {
                DataSet ds = new DataSet();

                SqlDataAdapter da = new SqlDataAdapter(customers, con);

                da.Fill(ds, "Customers");

                dataGridView.AutoGenerateColumns = true;
                dataGridView.DataSource = ds;
                dataGridView.DataMember = "Customers";
            }
        }
    }
}
```

窗体由一个 getData 按钮组成，单击该按钮时会调用示例代码中显示的 getData_Click() 方法。

该方法使用 ConfigurationManager 类的 ConnectionStrings 属性构造一个 SqlConnection 对象。随后，使用 DataAdapter 对象构造一个数据集，并从数据库表中填充该数据集。然后，通过设置 DataSource 和 DataMember 属性，DataGridView 控件将数据显示出来。请注意，AutoGenerateColumns 属性也被设置为 true，因为这可以确保向用户显示内容。如果未指定此标志，则需要自行创建所有列。

## 数据源

DataGridView 控件提供了一种灵活的数据显示方式；除了将 DataSource 设置为 DataSet，并将 DataMember 设置为要显示的表名之外，DataSource 属性还可以设置为以下任意来源：

- 数组（网格可以绑定到任何一维数组）
- DataTable
- DataView
- DataSet 或 DataViewManager
- 实现 IListSource 接口的组件
- 实现 IList 接口的组件
- 任何泛型集合类或从泛型集合类派生的对象

以下各节将给出每种数据源的示例。

## 显示数组中的数据

乍一看，从数组中显示数据似乎很简单。创建一个数组，用一些数据填充它，然后设置 DataGridView 控件的 DataSource 属性。以下是一些示例代码：

```
string[] stuff = new string[] {"One", "Two", "Three"};
dataGridView.DataSource = stuff;
```

如果数据源包含多个可能的候选表（例如使用 DataSet 或 DataViewManager 时），则还需要设置 DataMember 属性。

你可以将前面示例的 getData_Click 事件处理程序中的代码替换为前面的数组代码。这段代码的问题在于最终显示的结果（参见图 39-3）。

![](img/d7d2ffa0a76feaab821930e95daace93_1191_0.png)

网格显示的并不是数组中定义的字符串，而是这些字符串的长度。这是因为当使用数组作为 DataGridView 控件的数据源时，网格会查找数组中对象的第一个公共属性，并显示该值，而不是字符串值。字符串的第一个（也是唯一的）公共属性是它的长度，因此显示的是长度。任何类的属性列表都可以通过 TypeDescriptor 类的 GetProperties 方法获取。该方法返回一个 PropertyDescriptor 对象的集合，之后可在显示数据时使用这些对象。.NET 的 PropertyGrid 控件在显示任意对象时就会使用此方法。

解决在 DataGridView 中显示字符串问题的一种方法是创建一个包装类：

```
protected class Item
{
    public Item(string text)
    {
        _text = text;
    }

    public string Text
    {
        get {return _text;}
    }
    private string _text;
}
```

图 39-4 显示了将 Item 类的数组（对于它所执行的处理而言，使用结构体也同样可以）添加到数据源数组代码中后的输出结果。

![](img/d7d2ffa0a76feaab821930e95daace93_1192_0.png)

## DataTable

可以通过两种方式在 DataGridView 控件中显示 DataTable：

- 如果有一个独立的 DataTable，只需将控件的 DataSource 属性设置为该表即可。
- 如果 DataTable 包含在 DataSet 中，则需要将 DataSource 设置为该数据集，并将 DataMember 属性设置为该数据集中 DataTable 的名称。

![](img/d7d2ffa0a76feaab821930e95daace93_1192_1.png)

图 39-5 显示了运行 DataSourceDataTable 示例代码后的结果。

最后一列显示的是复选框，而不是更常见的编辑控件。在没有任何其他信息的情况下，DataGridView 控件会从数据源（此处为 Products 表）读取架构，并根据列类型推断出要显示的控件。与原始的 DataGrid 控件不同，DataGridView 控件内置了对图像列、按钮和组合框的支持。

当数据网格中的字段被修改时，数据库中的数据不会改变，因为数据仅存储在客户端的本地计算机上——没有与数据库的活动连接。更新数据库中的数据将在本章后面讨论。

## 显示 DataView 中的数据

DataView 提供了一种在 DataTable 中筛选和排序数据的方法。从数据库中选择数据后，通常允许用户对该数据进行排序，例如通过单击列标题来排序。此外，用户可能希望过滤数据以仅显示某些行，例如所有已更改的行。可以对 DataView 进行过滤，以便仅向用户显示选定的行；但是，不能从 DataTable 中过滤列。

> DataView 不允许过滤列，只允许过滤行。

若要基于现有 DataTable 创建 DataView，请使用以下代码：

```
DataView dv = new DataView(dataTable);
```

一旦创建了 DataView，就可以对其进一步设置，这些设置会影响数据以及在数据网格中显示该数据时所允许的操作。例如：

- 设置 AllowEdit = false 将禁用所有行的列编辑功能。
- 设置 AllowNew = false 将禁用新行功能。
- 设置 `AllowDelete = false` 将禁用删除行功能。
- 设置 `RowStateFilter` 仅显示给定状态的行。
- 设置 `RowFilter` 可以对行进行筛选。

下一节将解释如何使用 `RowStateFilter` 设置；其他选项的含义不言自明。

## 按数据过滤行

创建 `DataView` 后，可以通过设置 `RowFilter` 属性来更改该视图显示的数据。此属性的类型为字符串，用于根据字符串值定义的某些条件进行过滤。其语法类似于普通 SQL 中的 `WHERE` 子句，但它是针对已经从数据库中选出的数据执行的。

下表显示了一些筛选子句的示例。

| 子句 | 说明 |
|---|---|
| `UnitsInStock > 50` | 仅显示 `UnitsInStock` 列中的值大于 50 的行。 |
| `Client = 'Smith'` | 仅返回指定客户的记录。 |
| `County LIKE 'C*'` | 返回 `County` 字段以 C 开头的所有记录——在本示例中，将返回 Cornwall、Cumbria、Cheshire 和 Cambridgeshire 的行。`%` 字符可用作单字符通配符，而 `*` 表示通用通配符，可匹配零个或多个字符。 |

运行时将尽最大努力将筛选表达式中使用的数据类型强制转换为源列的适当类型。例如，在前面的示例中，即使列是整数，编写“`UnitsInStock > '50'`”也完全合法。如果提供了无效的筛选字符串，将引发 `EvaluateException` 异常。

## 按状态过滤行

`DataView` 中的每一行都有一个已定义的行状态，其值如下表所示。此状态也可用于过滤用户查看的行。

| DATAVIEWROWSTATE | 说明 |
|---|---|
| `Added` | 列出所有新创建的行。 |
| `CurrentRows` | 列出除已删除行之外的所有行。 |
| `Deleted` | 列出最初选中且已被删除的所有行；不显示已删除的新创建行。 |
| `ModifiedCurrent` | 列出所有已修改的行，并显示每列的当前值。 |
| `ModifiedOriginal` | 列出所有已修改的行，但显示列的原始值，而非当前值。 |
| `OriginalRows` | 列出最初从数据源中选出的所有行。不包括新行。显示列的原始值（即，如果进行了更改，则不显示当前值）。 |
| `Unchanged` | 列出所有未以任何方式更改的行。 |

图 39-6 显示了一个可以添加、删除或修改行的网格，以及第二个网格，该网格列出处于上述某种状态的行。

