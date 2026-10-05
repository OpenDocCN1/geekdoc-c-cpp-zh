# Chapter 3 How to code and test a Windows Forms application 73

# A method written in a readable style

```
private void btnCalculate_Click(object sender, System.EventArgs e)
{
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
    decimal discountPercent = 0m;
    if (subtotal >= 500)
    {
        discountPercent = .2m;
    }
    else if (subtotal >= 250 && subtotal < 500)
    {
        discountPercent = .15m;
    }
    else if (subtotal >= 100 && subtotal < 250)
    {
        discountPercent = .1m;
    }

    decimal discountAmount = subtotal * discountPercent;
    decimal invoiceTotal = subtotal - discountAmount;
```

```
txtDiscountPercent.Text = discountPercent.ToString("pl1");
txtDiscountAmount.Text = discountAmount.ToString("c")\ntxtTotal.Text = invoiceTotal.ToString("c")\n
txtSubtotal.Focus();
```

# A method written in a readable style

```
private void btnCalculate_Click(object sender, System.EventArgs e)
decimal subtotal=Convert.ToDecimal(txtSubtotal.Text);
decimal discountPercent=0m;
if (subtotal>=500) discountPercent=.2m;
else if (subtotal>=250&&subtotal<500) discountPercent=.15m;
else if (subtotal>=100&&subtotal<250) discountPercent=.1m;
decimal discountAmount=subtotal-discountPercent;
decimal invoiceTotal=subtotal-discountAmount;
txtDiscountPercent.Text=discountPercent.ToString("pl1")
txtDiscountAmount.Text=discountAmount.ToString("c")
txtTotal.Text=invoiceTotal.ToString("c");txtSubtotal.Focus();
```

# Coding recommendations

+   - Use indentation and spaces to align statements and blocks of code they reflect the structure of the program.
- Use spaces to separate the words, operators, and values in each statement.
- Use blank lines before and after groups of related statements.

# Note

+   - As you enter code in the Code Editor, Visual Studio automatically adjusts its formatting by default.

3-8 How to code with a readable style