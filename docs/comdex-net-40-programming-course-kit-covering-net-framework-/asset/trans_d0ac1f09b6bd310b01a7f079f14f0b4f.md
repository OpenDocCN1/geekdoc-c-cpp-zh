
在前面的代码中，我们首先声明了一个 **string** 类型的数组 **words**，并使用 **ListBox** 控件中的项初始化该数组。之后，我们在 LINQ 查询中使用 **group by** 子句，根据元素的首字母对数组元素进行分组。最后，我们向 **ListBox** 控件的 **Items** 集合中添加了一个字符串，该字符串指示每组中元素的首字母，后面跟着该组中的所有元素。

11. 按键盘上的 F5 键运行应用程序。应用程序的输出将出现，显示窗体上 ListBox1 中的单词列表（图 C#-6.22）。
12. 单击 **Group Data** 按钮（图 C#-6.22），根据单词首字母按字母顺序对单词列表进行分组，如图 C#-6.23 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_420_0.png)

通过这种方式，可以使用 group by 子句基于共同共享的属性对一组值进行分组。

## 联接运算符

LINQ 中的联接运算符用于将一个数据源中的对象与另一个数据源中共享共同属性的对象联接起来。例如，假设表中有两列，一列包含名字，另一列包含姓氏。在这种情况下，可以使用联接运算符将名字与姓氏联接起来并一起显示这些值。表 6.8 列出了 LINQ 中的所有联接运算符：

**表 6.8：LINQ 中的联接运算符**

| 运算符 | 描述 | 查询表达式语法（C#） |
| --- | --- | --- |
| Join | 基于匹配键合并来自两个数据源的元素，并返回值对 | join ...in...on...equals... |
| GroupJoin | 基于匹配键合并来自两个数据源的元素并对结果进行分组 | join ...in...on...equals...into... |

执行以下步骤，使用 join 子句联接来自两个数据源的数据：

1. *启动* **Visual Studio 2010**。
2. 从菜单栏中*选择* **文件 > 新建 > 项目**。将打开“新建项目”对话框。
3. 在“新建项目”对话框左窗格的“已安装的模板”部分中，*选择* **Visual C# > Windows**。右窗格中将显示可用于在 C# 中开发基于 Windows 的应用程序的项目模板。
4. 在右窗格中*选择* **Windows 窗体应用程序**模板，以创建 Windows 窗体应用程序。
5. 在“名称”文本框中*输入*应用程序名称 **JoinOperator**（也可在随附光盘中找到），并在“位置”组合框中输入应用程序的适当位置。
6. 单击“确定”按钮关闭“新建项目”对话框。JoinOperator 应用程序即创建完成（图 C#-6.24）。
7. 从工具箱中将 Label 控件和 ListBox 控件拖放到窗体上。
8. 使用“属性”窗口将 Label 控件的 Text 属性设置为“订单详细信息：”，如图 C#-6.24 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_421_0.png)

图 C#-6.24

9. *右键单击“解决方案资源管理器”中的 Form1.cs 文件*，然后从上下文菜单中选择 *查看代码* 选项，在代码编辑器中打开 Form1.cs 文件，如图 C#-6.25 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_421_1.png)

图 C#-6.25

10. 在 Form1.cs 文件中添加代码清单 6.16 中突出显示的代码：

### 代码清单 6.16：显示 Form1.cs 文件的代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace JoinOperator
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        public class Customer
        {
            public int Key;
            public string Name;
        }

        public class Order
        {
            public int Key;
            public string OrderNumber;
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            var customers = new List<Customer>()
            {
                new Customer {Key = 1, Name = "Priya"},
                new Customer {Key = 2, Name = "Raj"},
                new Customer {Key = 3, Name = "Rohit"},
                new Customer {Key = 4, Name = "Ram"},
                new Customer {Key = 5, Name = "Jitendra"}
            };

            var orders = new List<Order>()
            {
                new Order {Key = 1, OrderNumber = "Number 1"},
                new Order {Key = 2, OrderNumber = "Number 2"},
                new Order {Key = 3, OrderNumber = "Number 3"},
                new Order {Key = 4, OrderNumber = "Number 4"},
                new Order {Key = 5, OrderNumber = "Number 5"}
            };

            var q = from c in customers
                    join o in orders on c.Key equals o.Key
                    select new { c.Name, o.OrderNumber };

            foreach (var i in q)
            {
                listBox1.Items.Add(i.OrderNumber.ToString() + " " + i.Name);
            }
        }
    }
}
```

在代码清单 6.16 中，创建了两个列表 customers 和 orders，它们分别包含与客户和订单相关的数据。我们使用 LINQ 查询中的 join 子句联接了 customers 和 orders 这两个列表。

11. 按键盘上的 F5 键显示输出，如图 C#-6.26 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_422_0.png)

图 C#-6.26

在图 C#-6.26 中，来自两个不同数据源的数据通过 join 子句进行了联接。

## 量词运算符

量词运算符根据序列中的元素是否满足给定条件返回布尔值（True 或 False）。表 6.9 列出了 LINQ 中的所有量词运算符：

**表 6.9：LINQ 中的量词运算符**

| 运算符 | 描述 | 查询表达式语法（C#） |
| --- | --- | --- |
| All | 检查集合中的所有元素是否都满足条件 | 不可用 |
| Any | 检查集合中是否有任何元素满足条件 | 不可用 |
| Contains | 确定集合是否包含指定元素 | 不可用 |

了解量词运算符之后，现在来学习生成运算符。

## 生成运算符

生成运算符有助于创建新的值序列。这意味着已经存在按特定顺序排列的值集合；不过，你也可以从该集合中选择一个值范围或重复值，并将它们放入另一个序列中。

表 6.10 列出了 LINQ 中的所有生成运算符：

**表 6.10：LINQ 中的生成运算符**

| 运算符 | 描述 | 查询表达式语法（C#） |
| --- | --- | --- |
| DefaultIfEmpty | 检索指定集合的元素；如果指定集合为空，则返回默认值 | 不可用 |
| Empty | 检索空集合 | 不可用 |
| Range | 借助给定的值范围创建新集合 | 不可用 |
| Repeat | 通过将单个值重复指定次数来创建新集合 | 不可用 |

了解生成运算符之后，现在来学习元素运算符。

## 元素运算符

元素运算符是从序列中仅返回一个元素的运算符。这意味着，当你只想从包含 n 个值的序列中检索第 n 个值时，可以使用元素运算符。表 6.11 列出了 LINQ 中的所有元素运算符：

**表 6.11：LINQ 中的元素运算符**

| 运算符 | 描述 | 查询表达式语法（C#） |
| --- | --- | --- |
| ElementAt | 检索集合中指定索引处的元素 | 不可用 |
| ElementAtOrDefault | 检索集合中指定索引处的元素；如果指定索引超出范围，则返回默认值 | 不可用 |
| First | 检索集合中的第一个元素；或检索集合中满足给定条件的第一个元素 | 不可用 |
| FirstOrDefault | 检索集合中的第一个元素；或检索集合中满足给定条件的第一个元素；如果集合中没有元素满足给定条件，则返回默认值 | 不可用 |
| Last | 检索集合中的最后一个元素；或检索集合中满足给定条件的最后一个元素 | 不可用 |
| LastOrDefault | 检索集合中的最后一个元素；或检索集合中满足给定条件的最后一个元素；如果集合中没有元素满足给定条件，则返回默认值 | 不可用 |
| Single | 检索仅包含一个元素的集合中的该元素；或检索集合中满足给定条件的元素 | 不可用 |
| SingleOrDefault | 检索集合中的唯一元素；或检索满足给定条件的唯一元素；如果集合中没有元素满足给定条件，则返回默认值 | 不可用 |

了解元素运算符之后，现在来学习转换运算符。

## 转换运算符

转换运算符用于执行数据类型转换。它们将对象从一种类型转换为另一种类型。表 6.12 列出了 LINQ 中的所有转换运算符：

**表 6.12：LINQ 中的转换运算符**

| 运算符 | 描述 | 查询表达式语法（C#） |
| --- | --- | --- |
| AsEnumerable | 将集合的数据类型更改为 `IEnumerable<T>` | 不可用 |
| AsQueryable | 将 `IEnumerable` 或 `IEnumerable<T>` 集合转换为 `IQueryable` 或 `IQueryable<T>` 集合 | 不可用 |
| Cast | 将集合的数据类型更改为新的数据类型 | 无内置表达式；使用显式类型变量，例如 from string abc in xyz |
| OfType | 从一组值中选择可转换为指定类型的那些值 | 不可用 |
| ToArray | 将集合转换为数组 | 不可用 |
