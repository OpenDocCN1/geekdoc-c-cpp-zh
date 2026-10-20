
## The property settings

Figure 10-16 presents the property settings for the Customer and Payment forms and their controls. In the Customer form, the AutoSize property of the label that displays the payment information has been set to false. This allows you to use the Form Designer to size the label. In addition, the DropDownStyle property for the combo box has been set to DropDownList so the user must select an item from the list.

In the Payment form, the properties have been set so the form looks and acts like a dialog box. In addition, the CancelButton property of the form has been set to the Cancel button, which causes the DialogResult property of that button to be set to Cancel. Finally, like the combo box on the Customer form, the DropDownStyle properties of the combo boxes on this form have been set to DropDownList so the user must select an item from the lists.

## The code for the Customer form

Figure 10-17 presents the code for the Customer form. After the code that Visual Studio has generated for the form, a Boolean variable named isDataSaved is declared and set to true. This variable indicates whether the data that’s currently displayed in the form has been saved. It’s set to false in the event handler for the TextChanged event of the Payment label and in the event handler for the SelectedIndexChanged event of the Customer Name combo box. Notice that the event handler for the Customer Name combo box also clears the Payment label so it doesn’t contain information that’s been entered for another customer.

When the Customer form is loaded, the event handler for the Load event adds two names to the Customer Name combo box. In a production application, of course, the combo box would include many more names, and they would be loaded from a file or database. But for the purposes of this chapter, two names are sufficient.

When the user clicks the Select Payment button, the Click event handler for that button displays the Payment form as a dialog box. Then, if the user clicks the OK button in that dialog box, the payment data is displayed in the Payment Method label on the Customer form. As you can see, this data is stored in the Tag property of the Payment form.

If the user clicks the Save button, the Click event handler for that button calls the IsValidData() method shown on page 2 of this listing. This method checks that the user has selected a customer and entered a payment. If so, the event handler for the Click event of the Save button calls the SaveData() method. This method sets the SelectedIndex property of the Customer Name combo box to -1 so that no customer is selected, and it clears the Payment Method label. Then, it sets the isDataSaved variable to true and moves the focus to the combo box. In a production application, this data would be saved to a file or database.

The last method is executed when the user tries to close the Customer form. This is the same method you saw in figure 10-14, so you shouldn’t have any trouble understanding how it works.

## The property settings for the Customer form

| Default name | Property | Setting |
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

## The property settings for the Payment form

| Default name | Property | Setting |
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

## Description

- In addition to the properties shown above, you’ll want to set the text and alignment properties so the forms look like the forms shown in figure 10-15.

## The code for the Customer form

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

## The code for the Payment form

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

## The code for the Payment form

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

## The code for the Payment form

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

Figure 10-18    The code for the Payment form (part 3 of 3)
