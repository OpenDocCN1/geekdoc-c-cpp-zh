# The code for the Payment form

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