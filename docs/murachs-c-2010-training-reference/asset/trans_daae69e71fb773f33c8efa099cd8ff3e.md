

## 第 10 章 Windows 表单和控件的高阶技巧 30

### 取消 Closing 事件的对话框代码

```csharp
private void frmCustomer_FormClosing(object sender, FormClosingEventArgs e)
{
    if (isDataSaved == false)
    {
        string message =
            "此表单包含未保存的数据。\n\n" + 
            "您要保存吗？";

        DialogResult button =
            MessageBox.Show(message, "客户",
            MessageBoxButtons.YesNoCancel,
            MessageBoxIcon.Warning);

        if (button == DialogResult.Yes)
        {
            if (IsValidData())
                this.SaveData();
            else
                e.Cancel = true;
        }
        if (button == DialogResult.Cancel)
        {
            e.Cancel = true;
        }
    }
}
```

### 上述代码显示的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_326_0.png)

### 说明

- 表单 FormClosing 事件的事件处理器接收一个名为 `e` 的参数，该参数由 `FormClosingEventArgs` 类创建。该参数的 `Cancel` 属性允许您指定是否取消事件。若要取消事件，请将此属性设置为 `true`。

图 10-14 如何使用 FormClosing 事件

### Payments应用程序

本章通过展示一个包含两个表单的操作、属性设置和代码来结束，这两个表单使用了本章介绍的控件和编码技术。通过学习此应用程序的代码，您将更好地了解如何在自己的应用程序中使用这些控件和技术。

### 操作

图 10-15 显示了 应用程序的工作原理。首先，此应用程序显示 Customer 表单。在此表单上，用户必须从 Customer Name 组合框中选择一个客户。然后，用户必须点击 Select Payment 按钮显示 Payment 对话框，并为选客户指定支付信息。

在 Payment 对话框中，用户可以选择扣除客户的信用卡并输入所需信息。或者，用户可以选择直接向客户账单。完成表单，用户点击 OK 按钮。然后，控制返回到 Customer 表单，支付信息将显示在该表单上。要保存支付信息，用户点击 Save 按钮。

### Customer 表单

![](img/3148667e42d4db35b3d08576aaa1fa01_328_0.png)

### Payment 对话框的两个版本

![](img/3148667e42d4db35b3d08576aaa1fa01_328_1.png)

### 说明

- Customer 表单中的 Customer Name 组合框允许用户选择客户。
- Customer 表单中的 Select Payment 按钮显示 Payment 对话框，允许用户为客户指定支付信息。
- 如果选择了 Credit Card，用户必须选择信用卡类型、输入卡号并选择月份和年份。
- 如果选择了 Bill Customer，Credit Card Type、Card Number 和 Expiration Date 控件将被禁用。
- 当用户点击 Payment 表单上的 OK 按钮时，控制返回到 Customer 表单，支付信息显示在 Payment Method 标签中。

### 注意

- 此应用程序并未实际保存输入的数据。但在生产应用程序中，数据将保存到数据库或文件中。

图 10-15 Payments 应用程序的操作

### 属性设置

图 10-16 展示了 Customer 和 Payment 表单及其控件的属性设置。在 Customer 表单中，显示支付方式的标签的 `AutoSize` 属性已设置为 `false`。这允许您使用表单设计器调整标签的大小。

在 Payment 表单中，属性已过设置，使表单看起来和运行起来像一个对话框。此外，两个组合框的 `DropDownStyle` 已设置为 `DropDownList`；用户必须从列表中选择一个项。最后，Cancel 按钮的 `DialogResult` 属性已设置为 `Cancel`，当表单的 `CancelButton` 属性设置为 Cancel 按钮时，这会自动发生。

### Customer 表单的代码

图 10-17 展示了 Customer 表单的代码。在 Visual Studio 为表单生成的代码之后，声明了一个名为 `isSaved` 的布尔变量并将其设置为 `true`。该变量表示表单中当前显示的数据是否已保存。每当 Customer Name 组合框或 Payment 标签中的数据发生变化时，它会被设置为 `false`。为了实现这一点，组合框的 `SelectedChanged` 事件和标签的 `TextChanged` 事件被连接到 `DataChanged` 方法。

当 Customer 表单加载时，Load 事件的事件处理器向 Customer Name 组合框添加了两个名称。在生产应用程序中，组合框将包含更多名称，并且将从文件或数据库加载。但对于本章而言，两个名称足够了。

当用户点击 Select Payment 按钮时，该按钮的 `Click` 事件处理器会将 Payment 表单作为对话框显示。然后，如果用户点击对话框中的 OK 按钮，支付信息将显示在 Customer 表单的 Payment Method 标签中。如您所示，这些数据存储在……

如果用户点击 Save 按钮，该按钮的 `Click` 事件处理器会调用第 2 页所示的 `IsValidData` 方法，它将 `isSaved` 设置为 `true`。在生产应用程序中，数据将保存到文件或数据库。最后一个方法如图 10-14 中所示，因此您不需要理解它是工作的。

第 10 章 Windows 表单和控件的高阶技巧 31

### Customer 表单的属性设置

| 默认名称 | 属性 | 设置 |
| --- | --- | --- |
| Form1 | Name | frmCustomer |
| Text | Customer |
| CancelButton | btn |
| comboBox1 | Name | cboNames |
| DropDownStyle | DropDownList |
| label3 | Name | lblPayment |
| BorderStyle | FixedDialog |
| AutoSize | False |
| button1 | Name | btnSave |
| button2 | Name | btnCancel |
| button3 | Name | btnSelect |

### Payment 表单的属性设置

| 默认名称 | 属性 | 设置 |
| --- | --- | --- |
| Form2 | Name | frmPayment |
| Text | Payment |
| AcceptButton | btnOK |
| CancelButton | btnCancel |
| ControlBox | False |
| MaximizeBox | False |
| BorderBorderStyle | FixedDialog |
| groupBox1 | Text | Billing |
| radioButton1 | Name | rdoCreditCard |
| Checked | True |
| radioButton2 | Name | rdoBillCustomer |
| listBox1 | Name | lstCardType |
| textBox1 | Name | txtCardNumber |
| comboBox1 | Name | cboExpirationMonth |
| DropDownStyle | DropDownList |
| comboBox2 | Name | cboExpirationYear |
| DropDownStyle | DropDownList |
| checkBox1 | Name | chkDefault |
| Checked | True |
| button1 | Name | btnOK |
| button2 | Name | btnCancel |

### 说明

- 除了上述属性外，您可能希望设置文本和对齐属性，以表单看起来像图 10-15 中的表单。

### Customer 表单的代码

```csharp
public partial class frmCustomer : Form
{
    public frmCustomer()
    {
        InitializeComponent();
    }
    bool isSaved = true;
    private void frmCustomer_Load(object sender, System.EventArgs e)
    {
        cboNames.Items.Add("Mike Smith");
        cboNames.Items.Add("Nancy Jones");
    }
    private void DataChanged(object sender, System.EventArgs e)
    {
        isSaved = false;
    }
    private void btnSelectPayment_Click(object sender, System.EventArgs e)
    {
        Form paymentForm = new frmPayment();
        DialogResult selectedButton = paymentForm.ShowDialog();
        if (selectedButton == DialogResult.OK)
        {
            lblPayment.Text = (string)paymentForm.Tag;
        }
    }
    private void btnSave_Click(object sender, System.EventArgs e)
    {
        if (IsValidData())
        {
            SaveData();
        }
    }
}
```

图 10-17 Customer 表单的代码（第 1/2 部分）

