# The enhanced Invoice Total form

![](bbox=[0.056, 0.101, 0.513, 0.259])

# The code for the class variables and two event handlers

```
int numberOfInvoices = 0;
decimal totalOfInvoices = 0m;
decimal invoiceAverage = 0m;

private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal subtotal = Convert.ToDecimal(txtEnterSubtotal.Text);
    decimal discountPercent = .25m;
    decimal discountAmount = Math.Round(subtotal * discountPercent, 2);
    decimal invoiceTotal = subtotal - discountAmount;
    txtSubtotal.Text = subtotal.ToString("c");
    txtDiscountPercent.Text = discountPercent.ToString("pl");
    txtDiscountAmount.Text = discountAmount.ToString("c");
    txtTotal.Text = invoiceTotal.ToString("c");

    numberOfInvoices += invoiceTotal;
    invoiceAverage = totalOfInvoices / numberOfInvoices;

    txtNumberOfInvoices.Text = numberOfInvoices.ToString();
totalOfInvoices.Text = totalOfInvoices.ToString("c");
txtInvoiceAverage.Text = invoiceAverage.ToString("c");

    txtEnterSubtotal.Text = "";
    txtEnterSubtotal.Focus();
}

private void btnCalculateTotals_Click(object sender, System.EventArgs e)
{
    numberOfInvoices = 0;
totalOfInvoices = 0m;
invoiceAverage = 0m;

    txtNumberOfInvoices.Text = "";
totalOfInvoices.Text = "";
txtInvoiceAverage.Text = "";

    txtEnterSubtotal.Focus();
}

```

Figure 4-17  The enhanced Invoice Total application