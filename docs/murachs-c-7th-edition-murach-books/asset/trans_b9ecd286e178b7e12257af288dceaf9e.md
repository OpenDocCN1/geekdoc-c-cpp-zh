

## 属性设置

图 10-16 展示了 Customer 表单和 Payment 表单及其控件的属性设置。在 Customer 表单中，显示付款信息的标签的 AutoSize 属性已设置为 false。这允许你使用 Form Designer 来调整标签大小。此外，组合框的 DropDownStyle 属性已设置为 DropDownList，因此用户必须从列表中选择一个项目。

在 Payment 表单中，属性已设置使表单看起来并像对话框一样工作。此外，表单的 CancelButton 属性已设置为 Cancel 按钮，这会导致该按钮的 DialogResult 属性被设置为 Cancel。最后，与 Customer 表单上的组合框一样，此表单上组合框的 DropDownStyle 属性也已设置为 DropDownList，因此用户必须从列表中选择一个项目。

## Customer 表单的代码

图 10-17 展示了 Customer 表单的代码。在 Visual Studio 为表单生成的代码之后，声明了一个名为 isDataSaved 的布尔变量并将其设置为 true。该变量指示当前在表单中显示的数据是否已保存。它在 Payment 标签的 TextChanged 事件的处理程序中设置为 false，并在 Customer Name 组合框的 SelectedIndexChanged 事件的处理程序中设置为 false。请注意，Customer Name 组合框的事件处理程序还清空了 Payment 标签，以便它不包含为另一位客户输入的信息。

当 Customer 表单加载时，Load 事件的处理程序向 Customer Name 组合框添加了两个名称。在生产应用程序中，当然组合框将包含更多名称，并且它们将从文件或数据库加载。但就本章而言，两个名称已足够。

当用户单击 Select Payment 按钮时，该按钮的 Click 事件处理程序将 Payment 表单作为对话框显示。然后，如果用户在该对话框中单击 OK 按钮，则付款数据将显示在 Customer 表单的 Payment Method 标签中。如你所见，此数据存储在 Payment 表单的 Tag 属性中。

如果用户单击 Save 按钮，则该按钮的 Click 事件处理程序将调用本列表第 2 页所示的 IsValidData() 方法。此方法检查用户是否已选择客户并输入了付款。如果是，则 Save 按钮的 Click 事件处理程序将调用 SaveData() 方法。此方法将 Customer Name 组合框的 SelectedIndex 属性设置为 -1，以便没有客户被选中，并清空 Payment Method 标签。然后，它将 isDataSaved 变量设置为 true 并将焦点移至组合框。在生产应用程序中，此数据将保存到文件或数据库中。

最后一个方法在用户尝试关闭 Customer 表单时执行。这就是你在图 10-14 中看到的相同方法，因此你不应该有任何理解上的困难。

## Customer 表单的属性设置

| 默认名称 | 属性 | 设置 |
|---|---|---|
| Form1 | Name | frmCustomer |
|  | Text | Customer |
|  | CancelButton | btnExit |
|  | StartPosition | CenterScreen |
| comboBox1 | Name | cboNames |
|  | DropDownStyle | DropDownList |
| label3 | Name | lblPayment |
|  | BorderStyle | Fixed3D |
|  | AutoSize | False |
|  | Text | "" |
| button1 | Name | btnSave |
| button2 | Name | btnExit |
| button3 | Name | btnSelectPayment |

## Payment 表单的属性设置

| 默认名称 | 属性 | 设置 |
|---|---|---|
| Form2 | Name | frmPayment |
|  | Text | Payment |
|  | AcceptButton | btnOK |
|  | CancelButton | btnCancel |
|  | StartPosition | CenterScreen |
|  | ControlBox | False |
|  | MaximizeBox | False |
|  | FormBorderStyle | FixedDialog |
| groupBox1 | Text | Billing |
| radioButton1 | Name | rdoCreditCard |
|  | Checked | True |
| radioButton2 | Name | rdoBillCustomer |
| listBox1 | Name | lstCreditCardType |
| textBox1 | Name | txtCardNumber |
| comboBox1 | Name | cboExpirationMonth |
|  | DropDownStyle | DropDownList |
| comboBox2 | Name | cboExpirationYear |
|  | DropDownStyle | DropDownList |
| checkBox1 | Name | chkDefault |
|  | Checked | True |
| button1 | Name | btnOK |
| button2 | Name | btnCancel |
|  | DialogResult | Cancel |

## 描述

- 除了上面显示的属性外，你还希望设置文本和对齐属性，以便表单看起来像图 10-15 中显示的表单。

## Customer 表单的代码

```
public partial class frmCustomer : Form
{
    public frmCustomer()
    {
        InitializeComponent();
    }

    bool isDataSaved = true;

    private void frmCustomer_Load(object sender, EventArgs e)
    {
        cboNames.Items.Add("Mike Smith");
        cboNames.Items.Add("Nancy Jones");
    }

    private void lblPayment_TextChanged(object sender, EventArgs e)
    {
        isDataSaved = false;
    }

    private void cboNames_SelectedIndexChanged(object sender, EventArgs e)
    {
        isDataSaved = false;
        lblPayment.Text = "";
    }

    private void btnSelectPayment_Click(object sender, EventArgs e)
    {
        Form paymentForm = new frmPayment();
        DialogResult selectedButton = paymentForm.ShowDialog();
        if (selectedButton == DialogResult.OK)
        {
            lblPayment.Text = (string) paymentForm.Tag;
        }
    }

    private void btnSave_Click(object sender, EventArgs e)
    {
        if (IsValidData())
        {
            SaveData();
        }
    }

    private void SaveData()
    {
        cboNames.SelectedIndex = -1;
        lblPayment.Text = "";
        isDataSaved = true;
        cboNames.Focus();
    }
}
```

## Payment 表单的代码

```
public partial class frmPayment : Form
{
public frmPayment()
{
InitializeComponent();
}

private void frmPayment_Load(object sender, EventArgs e)
{
lstCreditCardType.Items.Add("Visa");
lstCreditCardType.Items.Add("Mastercard");
lstCreditCardType.Items.Add("American Express");
lstCreditCardType.SelectedIndex = 0;

string[] months = {"Select a month...",
"January", "February", "March", "April",
"May", "June", "July", "August",
"September", "October", "November", "December"};
foreach (string month in months)
{
cboExpirationMonth.Items.Add(month);
}
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

private void btnOK_Click(object sender, EventArgs e)
{
if (IsValidData())
{
this.SaveData();
}
}
}
```

## Payment 表单的代码

```
private bool IsValidData()
{
    if (rdoCreditCard.Checked)
    {
        if (lstCreditCardType.SelectedIndex == -1)
        {
            MessageBox.Show("You must select a credit card type.",
                "Entry Error");
            lstCreditCardType.Focus();
            return false;
        }
        if (txtCardNumber.Text == "")
        {
            MessageBox.Show("You must enter a credit card number.",
                "Entry Error");
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

## Payment 表单的代码

```csharp
private void SaveData()
{
    string msg = null;
    if (rdoCreditCard.Checked == true)
    {
        msg += "Charge to credit card. " + "\n\n";
        msg += "Card type: " + lstCreditCardType.Text + "\n";
        msg += "Card number: " + txtCardNumber.Text + "\n";
        msg += "Expiration date: "
             + cboExpirationMonth.Text + "/"
             + cboExpirationYear.Text + "\n";
    }
    else
    {
        msg += "Send bill to customer." + "\n\n";
    }

    bool isDefaultBilling = chkDefault.Checked;
    msg += "Default billing: " + isDefaultBilling;

    this.Tag = msg;
    this.DialogResult = DialogResult.OK;
}

private void Billing_CheckedChanged(object sender, EventArgs e)
{
    if (rdoCreditCard.Checked)
        EnableControls();
    else
        DisableControls();
}

private void EnableControls()
{
    lstCreditCardType.Enabled = true;
    txtCardNumber.Enabled = true;
    cboExpirationMonth.Enabled = true;
    cboExpirationYear.Enabled = true;
}

private void DisableControls()
{
    lstCreditCardType.Enabled = false;
    txtCardNumber.Enabled = false;
    cboExpirationMonth.Enabled = false;
    cboExpirationYear.Enabled = false;
}
```

图 10-18    Payment 表单的代码（第 3 部分，共 3 部分）

