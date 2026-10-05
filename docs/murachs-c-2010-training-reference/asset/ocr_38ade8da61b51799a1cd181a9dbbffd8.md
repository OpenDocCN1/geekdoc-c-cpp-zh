# A method that checks if a string contains a decimal value

public bool IsDecimal(TextBox textBox, string name)

```
{
    string s = TextBox.Text;
    int decimalCount = 0;
    bool validDecimal = true;
    foreach (char c in s)
    {
        if (1(
            c == '0' || c == '1' || c == '2' // numeric chars
            c == '3' || c == '4' || c == '5'
            c == '6' || c == '7' || c == '8'
            c == '9' || c == '-' || c == '%' || c == ',' // formatting chars
            c == '_'
        ))
        {
            validDecimal = false;
            break;
        }
        if (c == '.')
        {
            decimalCount++;
        }
    }
    if (validDecimal && decimalCount <= 1)
    {
        return true;
    }
    else
    {
        MessageBox.Show(name + " must be a decimal value.",
        "Entry Error");
        textBox.Focus();
        return false;
    }
}
```

# A method that strips formatting characters from a numeric string

public string Strip(string s)

```
{
    foreach (char c in s)
    {
        if (c == '$' || c == '%' || c == ',' || c == ' ')
        {
            int i = s.IndexOf(c);
            s = s.Remove(i, 1);
        }
    }
    return s;
}
```

# Code that calls the methods shown above

```
decimal monthlyInvestment = 0;
if (IsDecimal(txtMonthlyInvestment, "Monthly Investment")
{
    monthlyInvestment = Convert.ToDecimal(
    Strip(txtMonthlyInvestment.Text));
}
```

Figure 9-8 Two methods for validating user entries