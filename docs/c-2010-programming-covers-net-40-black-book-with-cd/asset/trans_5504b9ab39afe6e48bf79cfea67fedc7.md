

在前面的代码片段中，我们创建了一个 `XsltCompiledTransform` 类的对象。然后，通过调用 `XsltCompiledTransform` 对象的 `Load()` 方法加载 XSL 文件 `authors.xslt`。随后，将位于项目 `bin` 文件夹内 `debug` 文件夹中的 XML 文件 `authors.xml`（这是默认路径）转换生成 HTML 文件 `authors.html`，位置相同。最后，在 Web 浏览器中打开该 HTML 文件。

8. 按 F5 键运行 TransformingXML 应用程序。在输出中，点击 Generate HTML 按钮后，HTML 文件会在 Web 浏览器中打开，如图 30.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1479_0.png)

图 30.8：显示 TransformingXML 应用程序的输出

## 转换 ADO.NET 和 XML 数据

你已经了解到 ADO.NET 提供了一些强大的功能，用于读写 XML 文档。你可以通过先使用 ADO.NET 数据源填充 `DataSet` 对象，然后调用 `DataSet` 对象的 `WriteXml()` 方法来创建包含 ADO.NET 数据源数据的 XML 文件。`WriteXml()` 方法有两个重载形式，其中一个接受包含文件路径和名称的字符串，另一个多一个参数用于指定模式，该模式的值来自 `XmlWriteMode` 枚举。`XmlWriteMode` 枚举的一个值是 `DiffGram`，它指定包含编辑会话前后相关数据的 XML 文档。

在本节中，你将学习 ADO.NET 数据与 XML 数据之间的转换。请注意，在下一节中，我们使用 Northwind 数据库来显示和访问 SQL 数据。让我们开始将 ADO.NET 数据转换为 XML 数据。

## 将 ADO.NET 数据转换为 XML 数据

在本节中，我们创建 ConvertingADO.NETDataIntoXMLData 应用程序（也可在 CD 上获得）以将 ADO.NET 数据转换为 XML 数据。

执行以下步骤将数据从 ADO.NET 数据源转换为 XML 文件格式：

- 1. 创建一个名为 ConvertingADO.NETDataIntoXMLData 的 Windows 窗体应用程序。
- 2. 从工具箱拖放一个 Web 浏览器、DataGridView 和按钮控件。
- 3. 将 button1 的 Text 属性设置为 Generate XML Data。
- 4. 将 Listing 30.7 中的代码添加到 Form1.cs 文件：

### Listing 30.7: Showing the Code of the Form1.cs File of the Converting ADO.NET Data Into XML Data Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.SqlClient;
using System.Xml;

namespace ConvertingADO.NETDataIntoXMLData
{
    public partial class Form1 : Form
    {
        DataSet ds;
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string str1 = "Data Source=.;Initial Catalog=Northwind;Integrated Security=True";
            SqlConnection con = new SqlConnection(str1);
            string str2 = "Select EmployeeID,FirstName,Title,HireDate from Employees";
            SqlDataAdapter da = new SqlDataAdapter(str2, con);
            ds = new DataSet("employeeslist");
            da.Fill(ds, "Employees");
            dataGridView1.DataSource = ds.Tables["Employees"];
        }

        private void button1_Click(object sender, EventArgs e)
        {
            ds.WriteXml("employees.xml");
            webBrowser1.Url = new Uri(AppDomain.CurrentDomain.BaseDirectory + "employees.xml");
        }
    }
```

在 Listing 30.7 中，添加了 `System.Data.SqlClient` 和 `System.Xml` 命名空间。在类级别声明了 `DataSet` 的对象。我们取了一个字符串变量并为其分配了连接 Northwind 数据库的连接字符串。之后，我们通过传递 `str1` 字符串变量创建了 `SqlConnection` 类的对象；然后取另一个字符串变量 `str2` 用于分配 SQL 命令。接下来，通过传递包含 SQL 命令的字符串变量和 `SqlConnection` 类的对象创建 `SqlDataAdapter` 类的对象。

接下来，使用名称 `employeeslist` 创建 `DataSet` 类的对象并将其分配给 `DataSet` 变量。通过传递 `DataSet` 对象作为一个参数、数据表的名称作为第二个参数调用 `SqlDataAdapter` 对象的 `Fill()` 方法。最后，将 Employees 表设置为 DataGridView 的 `DataSource` 属性。

在 button1 的 Click 事件中，我们通过调用 `DataSet` 对象的 `WriteXml()` 方法将数据从 `DataSet` 对象写入 XML 文件。XML 文件创建在项目的 `bin` 文件夹内的 `debug` 文件夹中。然后我们在 Web 浏览器中显示该 XML 文件的数据。

5. 按 F5 键运行 ConvertingADO.NETDataIntoXMLData 应用程序。在输出中，你可以点击 Generate XML Data 按钮生成 XML 文件并在 Web 浏览器中显示该文件的数据，如图 30.9 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1481_0.png)

图 30.9：显示 ConvertingADO.NETDataIntoXMLData 应用程序的输出

## 写入 DiffGram 数据

在本节中，我们创建 WritingDataToDiffGram 应用程序（也可在 CD 上获得）以使用 DiffGram 在编辑会话前后存储数据。这可以通过执行以下步骤完成：

- 1. 创建一个名为 WritingDataToDiffGram 的 Windows 窗体应用程序。
- 2. 从工具箱拖放一个 Web 浏览器和一个按钮控件。
- 3. 将按钮的 Text 属性设置为 Show Data。
- 4. 将 Listing 30.8 中的代码添加到 Form1.cs 文件：

### Listing 30.8: Showing the Code of the Form1.cs File of the WritingDataToDiffGram Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.SqlClient;
using System.Xml;
namespace WritingDataToDiffGram
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            string str1 = "Data Source=.;Initial Catalog=Northwind;Integrated Security=True";
            SqlConnection con = new SqlConnection(str1);
            string str2 = "Select EmployeeID,FirstName,Title,HireDate from Employees";
            SqlDataAdapter da = new SqlDataAdapter(str2, con);
            DataSet ds = new DataSet("employeeslist");
            da.Fill(ds, "Employees");
            DataRow dr = ds.Tables[0].NewRow();
            dr["EmployeeID"] = 7;
            dr["FirstName"] = "King";
            dr["Title"] = "Sales Representative";
            ds.Tables[0].Rows.Add(dr);
            ds.WriteXmlSchema("employees.xdr");
            ds.WriteXml("employeesdiff.xml", XmlWriteMode.DiffGram);
            ds.AcceptChanges();
            webBrowser1.Url = new Uri(AppDomain.CurrentDomain.BaseDirectory + "employeesdiff.xml");
        }
    }
```

在 Listing 30.8 中，添加了 `System.Data.SqlClient` 和 `System.Xml` 命名空间。我们将连接字符串分配给一个字符串变量以连接到 Northwind 数据库。之后，我们通过传递一个字符串变量创建了 `SqlConnection` 类的对象，并将 SQL 命令分配给另一个字符串变量。我们还通过传递包含 SQL 命令的字符串变量和 `SqlConnection` 类的对象创建了 `SqlDataAdapter` 类的对象。然后，我们使用名称 `employeeslist` 创建了 `DataSet` 类的对象。

接下来，通过传递 `DataSet` 对象作为一个参数、数据表的名称作为第二个参数调用 `SqlDataAdapter` 对象的 `Fill()` 方法。然后，我们为 Employees 数据表创建新行并向其中添加数据。向 Employees 数据表的 Rows 集合添加新行。通过调用 `DataSet` 对象的 `WriteXmlSchema()` 方法写入架构文件 `employees.xdr`。该架构文件用于读取 DiffGram 中的数据。

接下来，通过调用 `DataSet` 对象的 `WriteXml()` 方法并将 `XmlWriteMode.DiffGram` 作为模式参数传递，创建 DiffGram `employeesdiff.xml`。然后，通过调用 `DataSet` 对象的 `AcceptChanges()` 方法接受所做的更改。最后，在 Web 浏览器上显示 DiffGram 的数据。

- 5. 按 F5 键运行 WritingDataToDiffGram 应用程序。在输出中，点击 Show Data 按钮后，会创建 DiffGram 并在 Web 浏览器中显示 DiffGram 的数据，如图 30.10 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1482_0.png)

图 30.10：显示 WritingDataToDiffGram 应用程序的输出

