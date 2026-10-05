# Chapter 10 More skills for working with Windows forms and controls 313

# The code for the Customer Page 2

```
private bool IsValidData()\{
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
      ""This form contains unsaved data.\n\n" +
      ""Do you want to save it?";
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

Figure 10-17 The code for the Customer form (part 2 of 2)