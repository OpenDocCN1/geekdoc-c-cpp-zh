# The code for the Payment form

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