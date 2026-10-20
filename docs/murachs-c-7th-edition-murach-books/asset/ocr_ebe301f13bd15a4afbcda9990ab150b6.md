# The code for the Future Value application

```
private void btnCalculate_Click(object sender, EventArgs e)
{
    try
    {
        if (IsValidData())
        {
            decimal monthlyInvestment =
                Convert.ToDecimal(txtMonthlyInvestment.Text);
            decimal yearlyInterestRate =
                Convert.ToDecimal(txtInterestRate.Text);
            int years = Convert.ToInt32(txtYears.Text);

            int months = years * 12;
            decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;
            decimal futureValue = CalculateFutureValue(
                monthlyInvestment, monthlyInterestRate, months);

            txtFutureValue.Text = futureValue.ToString("c");
            txtMonthlyInvestment.Focus();
        }
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message + "\n\n" +
            ex.GetType().ToString() + "\n" +
            ex.StackTrace, "Exception");
    }
}

private bool IsValidData()
{
    bool success = true;
    string errorMessage = "";

    errorMessage += IsDecimal(txtMonthlyInvestment.Text,
        txtMonthlyInvestment.Tag.ToString());
    errorMessage += IsWithinRange(txtMonthlyInvestment.Text,
        txtMonthlyInvestment.Tag.ToString(),
        1, 1000);

    errorMessage += IsDecimal(txtInterestRate.Text,
        txtInterestRate.Tag.ToString());
    errorMessage += IsWithinRange(txtInterestRate.Text,
        txtInterestRate.Tag.ToString(), 1, 20);

    errorMessage += IsInt32(txtYears.Text, txtYears.Tag.ToString());
    errorMessage += IsWithinRange(txtYears.Text, txtYears.Tag.ToString(),
        1, 40);

    if (errorMessage != "")
    {
        success = false;
        MessageBox.Show(errorMessage, "Entry Error");
    }
    return success;
}
```

Figure 7-12    The code for the Future Value application (part 1 of 2)