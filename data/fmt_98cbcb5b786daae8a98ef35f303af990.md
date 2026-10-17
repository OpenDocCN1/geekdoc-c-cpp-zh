
- 如果选择了 Credit Card，用户必须选择信用卡类型、输入卡号并选择月份和年份。

- 如果选择了 Bill Customer，`Credit Card Type`、`Card Number` 和 `Expiration Date` 控件将被禁用。

- 当用户点击 Payment 表单上的 OK 按钮时，控制返回到 Customer 表单，支付信息显示在 Payment Method 标签中。

# 注意

- 此应用程序并未实际保存输入的数据。但在生产应用程序中，数据将保存到数据库或文件中。

图 10-15 Payments 应用程序的操作

### 属性设置

图 10-16 展示了 Customer 和 Payment 表单及其控件的属性设置。在 Customer 表单中，显示支付方式的标签的 `AutoSize` 属性已设置为 `false`。这允许您使用表单设计器调整标签的大小。

在 Payment 表单中，属性已过设置，使表单看起来和运行起来像一个对话框。此外，两个组合框的 `DropDownStyle` 已设置为 `DropDownList`；用户必须从列表中选择一个项。最后，Cancel 按钮的 `DialogResult` 属性已设置为 `Cancel`，当表单的 `CancelButton` 属性设置为 Cancel 按钮时，这会自动发生。

### Customer 表单的代码

图 10-17 展示了 Customer 表单的代码。在 Visual Studio 为表单生成的代码之后，声明了一个名为 `isSaved` 的布尔变量并将其设置为 `true`。该变量表示表单中当前显示的数据是否已保存。每当 Customer Name 组合框或 Payment 标签中的数据发生变化时，它会被设置为 `false`。为了实现这一点，组合框的 `SelectedChanged` 事件和标签的 `TextChanged` 事件被连接到 `DataChanged` 方法。

当 Customer 表单加载时，`Load` 事件的事件处理器向 Customer Name 组合框添加了两个名称。在生产应用程序中，组合框将包含更多名称，并且将从文件或数据库加载。但对于本章而言，两个名称足够了。

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

## 说明

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

# 第 10 章 用于 Windows 表单和控件的更多技巧 313

## Customer 页面第 2 部分代码

```csharp
private bool IsValidData()
{
  if (cboNames.SelectedIndex == -1)
  {
    MessageBox.Show("You must select a customer.", "Entry Error");
    cboNames.Focus();
    return false;
  }
  if (lblPayment.Text == "")
  {
    MessageBox.Show("You must enter a payment.", "Entry Error");
    return false;
  }
}
private void btnExit_Click(object sender, System.EventArgs e)
{
  this.Close();
}
private void frmCustomer_Form_Closing(object sender,
FormClosingEventArgs e)
{
  if (isDataSaved == false)
  {
    string message =
      "This form contains unsaved data.\n\n" +
      "Do you want to save it?";
    DialogResult button =
      MessageBox.Show(message, "Customer",
      MessageBoxButtons.YesNoCancel,
      MessageBoxIcon.Warning);
  }
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
```

图 10-17 Customer 表单代码（2 部分中的 2 部分）

## Payment 表单代码

图 10-18 显示了 Payment 表单的代码。在 Visual Studio 为表单生成的代码之后，`Load` 事件的事件处理程序向列表框和表单上的两个组合框添加了适当的项目。此外，此方法设置了这些控件的 `SelectedIndex`，以便选中第一个项目。

当用户点击表单上的 OK 按钮时，事件处理程序首先调用此列表第 2 页所示的 `IsValidData` 方法。如果选择了信用卡（Credit Card）单选按钮，该方法将检查用户是否选择了信用卡类型并输入了信用卡号。它还会检查用户是否从两个组合框中选择了第一个项目以外的项。这是必要的，因为这些组合框的第一项包含用户指令（“Select a month...”和“Select a year...”）。

如果数据有效，OK 按钮的事件处理程序将继续调用此列表第 3 页所示的 `SaveData` 方法。此方法创建了一个包含支付信息的字符串。然后，将该字符串存储在此属性的 `Tag` 属性中以显示支付信息。正如你已经看到的，Customer 表单使用此属性显示支付信息。最后，`SaveData` 方法将表单的 `DialogResult` 属性设置为 `DialogResult` 枚举中的 `OK` 成员。这对于关闭 Payment 表单并允许程序执行到 Customer 表单是必要的。

当用户选择此表单上的单选按钮之一时，会发生 `CheckedChanged` 事件。对于两个单选按钮，此事件都连接到 `Billing_CheckChanged` 事件处理程序。如果当执行此事件处理程序时选择了信用卡单选按钮，它将调用 `EnableControls` 方法来启用表单上的其他控件，以便用户输入所需信息。然而，如果信用卡按钮未被选中，则意味着选择了账单（Bill）按钮。此时，该事件处理程序将调用 `DisableControls` 方法禁用其他控件。

## Payment 表单代码

```csharp
public partial class frmPayment : Form
{
    public frmPayment()
    {
        InitializeComponent();
    }
    private void Payment_Load(object sender, EventArgs e)
    {
        1stCreditCardType.Items.Add("Visa");
        1stCreditCardType.Items.Add("Mastercard");
        1stCreditCardType.Items.Add("American Express");
        1stCreditCardType.SelectedIndex = 0;

        string[] months = {"Select a month...",
        "January", "February", "March", "April",
        "May", "June", "July", "August",
        "September", "October", "November", "December"};
        foreach (string month in months)
            cboExpirationMonth.Items.Add(month);
        cboExpirationMonth.SelectedIndex = 0;

        int year = DateTime.Today.Year;
        int endYear = year + 8;
        cboExpirationYear.Items.Add("Select a year...");
        while (year < endYear)
        {
            cboExpirationYear.Items.Add(year);
            year++;
        }
        cboExpirationYear.SelectedIndex = 0;
    }

    private void btnOK_Click(object sender, System.EventArgs e)
    {
        if (IsValidData())
        {
            this.SaveData();
        }
    }
}
```

图 10-18 Payment 表单代码（3 部分中的 1 部分）

## Payment 表单代码

```csharp
private bool IsValidData()
{
    if (rdoCreditCard.Checked)
    {
        if (lstCardType.SelectedIndex == -1)
        {
            MessageBox.Show("You must select a credit card type.", "Entry Error");
            lstCardType.Focus();
            return false;
        }
        if (txtCardNumber.Text == "")
        {
            MessageBox.Show("You must enter a credit card number.", "Entry Error");
            txtCardNumber.Focus();
            return false;
        }
        if (cboExpirationMonth.SelectedIndex == 0)
        {
            MessageBox.Show("You must select a month.", "Entry Error");
            cboExpirationMonth.Focus();
            return false;
        }
        if (cboExpirationYear.SelectedIndex == 0)
        {
            MessageBox.Show("You must select a year.", "Entry Error");
            cboExpirationYear.Focus();
            return false;
        }
    }
    return true;
}
```

图 10-18 Payment 表单代码（3 部分中的 2 部分）

## Payment 表单代码
