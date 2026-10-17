
```csharp
this.ClientSize = new System.Drawing.Size(342, 253);
this.Controls.Add(this.checkBoxWater);
this.Controls.Add(this.label2);
this.Controls.Add(this.comboBoxSpecial);
this.Controls.Add(this.group2);
this.Controls.Add(this.label1);
this.Controls.Add(this.listBoxEntree);
this.Controls.Add(this.menuStrip1);
this.Font = new System.Drawing.Font("Arial", 9.75F,
System.FontStyle.Regular,
System.Drawing.GraphicsUnit.Point, ((byte)0));
this.ForeColor = System.Drawing.Color.Navy;
this.Icon = ((System.Drawing.Icon)(resources.GetObject(
"$thisIcon"));
this.MainMenuStrip = this.menuStrip1;
this.Name = "OrderGUI";
this.Text = "Student Union - Diner by the Valley";nthis.Load += new System.EventHandler(this.Form1_Load);
this.groupBox2.ResumeLayout(false);
this.menuStrip1.ResumeLayout(false);
this.menuStrip1.PerformLayout();
this.ResumeLayout(false);
this.PerformLayout( );

#endregion // Windows 窗单设计器生成的代码结束
}
// OrderGUI.designer.cs 文件结束
```

```csharp
// OrderGUI.cs 作者：Doyle
// 此文件包含事件处理方法。
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
```

```csharp
namespace Diner
{
    public partial class OrderGUI : Form
    {
        public OrderGUI()
        {
            InitializeComponent();
        }
    }
```

```csharp
// 当表单首次加载加载时，
// 实例化 Order 类对象。
private void Form1_Load(object sender,
    System.Events e)
{
    newOrder = new Order ( );
    for(int i = 0;
        i < newOrder.menuEntree.Length; i++)
        {
            this.lstBoxEntree.Items.Add(
                (newOrder.menuEntree[i]);
        }

}
```

```csharp
// 事件处理程序，从 ListBox
// 获取主菜 (entrée) 并设置主菜价格。
private void lstBoxEntree_SelectedIndexChanged
    (object sender,System.Events e)
{
    newOrder.Entree = this.lstBoxEntree.Text;
}
```

```csharp
// 事件处理程序，获取特殊要求 -
// 如果它是从预定义列表中选中的。
private void cmboBox_Special_SelectedIndexChanged
    (object sender,System.Events e)
{
    newOrder.SpecialRequest =
        this.comboBoxSpecial.Text;
}
```

```csharp
// 显示订单的菜单项。
private void menuDisplayOrder_Click(object sender,
    System.Events e)
{
    MessageBox.Show(
        newOrder.Entree + "\n"
        + newOrder.SpecialRequest
        + "\n"
        + newOrder.DrinkSelection
        + "\n" +
        newOrder.GetWaterSelection(),
        "当前订单");
}
```

```csharp
// 事件处理程序，获取选中的单选按钮
// 并设置饮料选择。
private void Drink_CheckedChanged(object sender,
    System.EventArgs e)
{
    if (this.radTea.Checked)
        newOrder.DrinkSelection =
            radTea.Text;
    else
        if (this.radCoffee.Checked)
            newOrder.DrinkSelection =
                radCoffee.Text;
    else
        if (this.radSoda.Checked)
            newOrder.DrinkSelection =
                radSoda.Text;
    else
        if (this.radLemon.Checked)
            newOrder.DrinkSelection =
                radLemon.Text;
    else
        if (this.radJuice.Checked)
            newOrder.DrinkSelection =
                radJuice.Text;
    else
        if (this.radMilk.Checked)
            newOrder.DrinkSelection =
                radMilk.Text;
}
```

```csharp
// 事件处理程序，当水复选框
// 被选中时触发。
private void ckWater_CheckedChanged
    (object sender, System.EventArgs e)
{
    if (this.checkBoxWater.Checked)
        Order..SelectionSelection =;

    

        newOrder.Selection = =;

```

```csharp
//// 事件程序当当在组合框的//////区域输入内容时触发。
private void cmboBoxSpecial_KeyPress
    (object sender,
    System.Windows.Forms.KeyPress e)
{
    newOrder.SpecialRequest =
        this.comboBoxSpecial.Text;
}
```

```csharp
// 事件处理程序，当点击编辑菜单以// 更改主菜 (entrée) 时触发。
private void menuEditEntree_Click(object sender, System.EventArgs e)
{
    MessageBox.Show("请选择新的主菜");
    newOrder.Entree = "";
    this.lstBoxEntree.Clear();
}
```

```csharp
// 事件处理程序，当点击编辑菜单以// 更改饮料时触发。
private void menuEdit_Click(object sender, System.EventArgs e)
{
    MessageBox.Show("请选择新的饮料");
    newOrder.DrinkSelection = "";
    ClearDrinks();
}
```

```csharp
// 清空所有饮料按钮的选择。
public void ClearDrinks()
{
    this.radMilk.Checked = false;
    this.radJuice.Checked = false;
    this.radSoda.Checked = false;
    this.radLemon.Checked = false;
    this.radTea.Checked = false;
    this.radCoffee.Checked = false;
}
```

```csharp
// 清空所有选择以便可以//
// 新订单。重置 Order 对象
// 为默认值。
private void menuClearOrder_Click(object sender, System.EventArgs e)
{
    this.lstBoxEntree.Clear();
    this.checkBoxWater.Checked = false;
    this.comboBoxSpecial.SelectedIndex = -1;
    this.comboBoxSpecial.Text = "";
    ClearDrinks();
    newOrder.DrinkSelection = "";
    newOrder.Entree = "";
    newOrder.SpecialRequest = "";
    newOrder.WaterSelection = false;
}
```

```csharp
// 显示 Order 实例的// 成员值。
private void menuPlaceOrder_Click(object sender, System.EventArgs e)
{
    MessageBox.Show(newOrder.Entree + "\n" +
    newOrder.SpecialRequest + "\n" +
    newOrder.DrinkSelection + "\n" +
    newOrder.GetWaterSelection() +
    "\n\n\n" + "总计: " +
    newOrder.DetermineTotalCharges().ToString("C", "已下单订单"));
}
```

```csharp
// 事件处理程序，当点击编辑菜单以
// 更改特殊要求时触发。
private void menuEditSpecial_Click(object sender, System.EventArgs e)
{
    MessageBox.Show("特殊要求已清除");
    newOrder.SpecialRequest = "";
    this.comboBoxSpecial.SelectedIndex = -1;
    this.comboBoxSpecial.Text = "";
}
```

```csharp
// 事件处理程序，当点击帮助
// 菜单以显示关于信息时触发。
private void menuAbout_Click(object sender, System.EventArgs e)
{
    MessageBox.Show("学生会 = " +
    "Diner by the Valley" +
    "\n\n\n版本 1.0");
}
```

```csharp
// 事件处理程序，当点击
// 退出时触发。
private void menuExit_Click(object sender, System.EventArgs e)
{
    Application.Exit( );
}
```

图 10-31 显示了带有“文件”菜单选项的原始用户界面。注意标题栏中使用了一个新图标。该图标是通过设置 `OrderGUI` 表单的 `Icon` 属性添加的。

![](img/45e6f245af31396d967c3186f196d331_661_0.png)

图 10-31 显示新菜单选项的界面

> 注意：可以使用任何以 `.ico` 扩展名结尾的文件。互联网上的许多资源提供免费图形。它们可以轻松地添加到你的 Windows 应用程序中。

要在表单上添加图片，只需要实例化 `PictureBox` 类的对象。如果你正在使用 Visual Studio，请将 `PictureBox` 控件对象拖到表单上。将 `Image` 属性设置为所需的图片。

> 注意：你可以为 `Image` 属性选择如 `*.bmp`、`*.gif`、`*.jpeg`、`*.jpg`、`*.png` 和 `*.ico` 的图形文件类型，或者选择如 `*.emf` 或 `*.wmf` 的元文件类型。将图像存储在当前项目的 `bin\debug` 子目录下。

`Form` 对象还有一个 `BackgroundImage` 属性，可以设置为在背景上显示图片。若要在背景中显示图片，在使用 Visual Studio 时选择表单，然后使用属性窗口选择 `BackgroundImage` 属性。浏览到包含位图或元文件的位置。

当表单被加载时，会触发 `Form_Load` 事件。此时，会实例化 `Order` 类的对象。使用 `Order` 类的 `entrée` 数组填充列表框。在表单上每次点击都会触发一个不同的事件。图 10-32 显示了在选择多个选项（包括“下单”菜单选项）后显示的消息。

# 编程示例：DinerGui 应用程序 629

![](img/45e6f245af31396d967c3186f196d331_662_0.png)

图 10-32 从“下单”菜单选项中显示出的的消息

`ComboBox` 对象允许输入特殊请求。任何新选择都会为 `Order` 类的实例设置新值。当用户在 `ComboBox` 对象的文本区域中输入值时，会触发 `KeyPress()`。图 10-33 阐了 `ComboBox` 对象的输入项。`MessageBox.Show()` 方法用于显示菜单选项的消息。图 10-33 是从“文件”->“显示订单”选项显示的。

![](img/45e6f245af31396d967c3186f196d331_662_1.png)

图 10-33 从“当前订单”菜单选项中显示的消息

当从“编辑”菜单触发事件时，事件处理方法会显示一条指示正在清除选择的消息。然后，返回表单 GUI 的控件被清除，`Order` 实例数据成员被设置为其默认值。图 10-34 显示了选择“编辑->“特殊请求”菜单选项的结果。

![](img/45e6f245af31396d967c3186f196d331_663_0.png)

触发 **清除订单** 菜单选项（如图 10-35 所示）将取消选择表单上的所有条目，并将 `Order` 实例数据成员重置为默认值。

Windows 应用程序将处于运行状态，直到触发 **退出** 菜单选项或点击 **关闭** 按钮。

![](img/45e6f245af31396d967c3186f196d331_664_0.png)

**图 10-35** 触发清除订单点击事件

此应用程序有许多事件处理方法连接到对象上。表 10-8 列出了事件处理方法及其关联对象。这些方法在 `OrderGUI` 类中都被实例化。

**表 10-8** DinerGUI 事件

| 事件处理方法 | 类 | 对象 |
| --- | --- | --- |
| ckBoxWater_CheckedChanged | CheckBox | ckBoxWater |
| cmboBoxSpecial_KeyPress | ComboBox | cmboBoxSpecial |
| cmboBoxSpecial_SelectedIndexChanged | ComboBox | cmboBoxSpecial |
| Drink_CheckedChanged | RadioButton | radTea, radSoda, radLemon, radMilk, radCoffee, radJuice |
| Forml1_Load | OrderGUI | this |
| 1stBoxEntree_SelectedIndexChanged | ListBox | 1stBoxEntree |

**表 10-8** DinerGUI 事件（续）

| 事件处理方法 | 类 | 对象 |
| --- | --- | --- |
| menuAbout_Click | ToolStripMenuItem | menuAbout |
| menuClearOrder_Click | ToolStripMenuItem | menuClearOrder |
| menuDisplayOrder_Click | ToolStripMenuItem | menuDisplayOrder |
| menuEditDrink_Click | ToolStripMenuItem | menuEditDrink |
