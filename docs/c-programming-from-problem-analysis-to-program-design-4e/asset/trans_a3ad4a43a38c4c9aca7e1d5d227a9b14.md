
```csharp
namespace PizzaApp
{
    public partial class PizzaForm : Form
    {
        private string order;
        private double totalCost;

        public PizzaForm()
        {
            InitializeComponent();
        }

        private void PizzaForm_Load(object sender, EventArgs e)
        {
            this.cmboSize.SelectedIndex = 1;
            this.cmboCrust.SelectedIndex = 0;
            this.cmboSpeciality.SelectedIndex = 0;
            this.txtBxSodaQty.Text = "0";
            this.txtBxWaterQty.Text = "0";
            order = "";
            totalCost = 0;
        }

        private void btnPlaceOrder_Click(object sender,
                                         EventArgs e)
        {
            double drinkCost,
                   pizzaCost,
                   specialtyCost;
            order = "";
            order += cmboCrust.SelectedItem.ToString() + " - ";
            order += cmboSize.SelectedItem.ToString() + "\n";
            if (ckBxItems.CheckedItems.Count > 0)
            {
                order += "Toppings:";
                foreach (string s in ckBxItems.CheckedItems)
                {
                    order += "\n" + s;
                }
            }

            pizzaCost = DeterminePizzaCost();
            if (pizzaCost != 0)
                order += "\nPizza Total: " +
                         pizzaCost.ToString("C");

            drinkCost = DetermineDrinkCost();

            if (drinkCost != 0)
                order += "\nDrink Total: " + drinkCost;

            specialtyCost = DetermineSpecialtyCost();
            if (specialtyCost != 0)
            {
                order += "\r\n\nSpecialty Items:\n" +
                    cmboSpeciality.SelectedItem.ToString();
            }

            order += "\r\n\nAmount Due: " +
                (pizzaCost + drinkCost +
                 specialtyCost).ToString("C");
            MessageBox.Show(order,
                "B & D Pizza Express Order\n");
        }

        private double DetermineDrinkCost()
        {
            double sodaCnt,
                   waterCnt;
            totalCost = 0;

            if (txtBxSodaQty.Text != "")
            {
                while (double.TryParse(txtBxSodaQty.Text,
                                       out sodaCnt) == false)
                {
                    lblErrorMsg.Text =
                        "Quantity must be numeric";
                    txtBxSodaQty.Text = "0";
                }
                order += "\r\n\nDrink Selections:\n" +
                    sodaCnt + " soda(s)";
                totalCost = sodaCnt * 1.75;
            }

            if (txtBxWaterQty.Text != "")
            {
                while (double.TryParse(txtBxWaterQty.Text,
                                       out waterCnt) == false)
                {
                    lblErrorMsg.Text =
                        "Quantity must be numeric";
                    txtBxWaterQty.Text = "0";
                }
                order += "\r\n" + waterCnt + " water(s)";
            }

            return totalCost;
        }

        public double DeterminePizzaCost()
        {
            double cost;
            if (cmboSize.SelectedIndex == 0)
                cost = 9.95;
            else
                if (cmboSize.SelectedIndex == 1)
                    cost = 12.95;
                else
                    cost = 15.95;
            return cost +
                (ckBxItems.CheckedItems.Count * 1.50);
        }

        public double DetermineSpecialtyCost()
        {
            double cost;

            if (cmboSpeciality.SelectedIndex == 1)
            {
                cost = 5.00;
            }
            else
                if (cmboSpeciality.SelectedIndex == 2)
                {
                    cost = 4.00;
                }
                else
                    if (cmboSpeciality.SelectedIndex == 3)
                    {
                        cost = 3.00;
                    }
                    else
                        cost = 0;
            return cost;
        }
    }
}
```

在查看示例 10-24 时，请注意两个标识符 `order` 和 `totalCost` 都定义为 `private` 数据成员，而不是在事件处理程序方法内部定义为局部变量。这样做是为了让类中的所有方法都能访问它们。`Form_Load()` 事件处理程序初始化并设置窗体上每个控件的默认值。应用程序的功能由 `btnPlaceOrder_Click()` 事件处理程序控制。应付总额在此方法中根据窗体上所做的选择来确定。

为节省篇幅，这里未显示 `PizzaApp.Designer.cs` 文件中自动生成的代码。不过，此应用程序与书中所有其他示例一样，可作为功能完整的 Visual Studio 项目使用。本示例新增了一个控件 CheckedListBox。该控件显示一个项目列表，每个项目左侧都有一个复选框。因此，它把所有复选框项目放在一个组中，提供了 GroupBox 的附加功能，但没有添加 GroupBox。CheckedListBox 控件使用了两个新属性：Count 和 CheckedItems。CheckedItems 属性返回已选中项的集合；Count 返回已选中项的数量。

另一个控件 PictureBox 也被拖放到 PizzaForm 的顶部选项卡上。要将图像与 PictureBox 控件关联，需选择 Image 属性。这样便可以浏览到图像存储的位置。你可以为图像创建单独的文件夹，或者像本应用程序一样，将图像放在 `bin\debug` 目录中。选择 Image 属性并单击三个点（省略号）后，将显示 **选择资源** 对话框。使用 **本地资源** 选项导入图像。

在查看工具箱时，请注意 **工具箱** 中有 100 多个不同的控件。本书仅详细介绍了其中一小部分。鼓励你探索、发现并试验其他控件及其属性。IntelliSense 会为你提供简短说明。更多详细信息可通过 Visual Studio 帮助系统和在线资源找到。

## 编程示例：DinerGUI 应用程序

本示例演示包含图形用户界面设计与实现的事件驱动应用程序。构造两个类，以将业务逻辑与表示细节分离。第一个类定义食品订单对象的模板。它包含处理订单的行为，订单中包括主菜、饮料和特殊请求的选择。该类为每个选中项分配价格，并确定订单总价。另一个类实例化 Order 类的对象，并实例化一个 Windows Form 对象来表示图形用户界面。使用 .NET 预定义的 Control 类，将 Label、ComboBox、ListBox、RadioButton、CheckBox 和 Menu 对象添加到 Form 对象中。DinerGUI 应用程序的问题说明如图 10-24 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_686_0.png)

Valley 校区熟食店旁 Diner 的经理计划在校园中心放置一台计算机，供学生进入时下单。他们提供有限菜单选择，包括三明治和饮料。经理希望计算机屏幕能让学生从可用的三明治和饮料选项列表中进行选择。计算机所在位置的墙上挂着一块大公告板，显示可用项目菜单并列出每项价格。

需要一个用户友好的界面。每份订单可免费获得水，但必须点单。除了白面包，他们还有全麦面包和黑麦面包。不同面包类型不额外收费；不过，他们确实将这种选择视为特殊请求。界面应允许选择面包类型等特殊请求。学生应能够输入其他特殊请求，例如“不要洋葱”或“不要蛋黄酱”。

设计一个 GUI，接受食品和饮料选择作为输入。经理希望提供以下选项：显示订单总费用、显示当前订单选择，或允许学生改变对每个选择的想法。

**图 10-24** DinerGUI 示例的问题说明

### 分析问题

你应该查看图 10-24 中的问题说明，并确保理解问题定义。将从 GUI 控件中选择若干值，以表示主菜和饮料选择，以及水和特殊请求的偏好。使用两个类将业务逻辑与用户界面分离。Order 类的数据成员如表 10-6 所示。
