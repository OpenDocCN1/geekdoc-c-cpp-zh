# The syntax of the Parse() and TryParse() methods for validating decimal values

```
Parse(string, style1[ | style2]...)
TryParse(string, style1[ | style2]..., formatProvider, result)
```

# Common members of the NumberStyles enumeration for decimal values

| Member | Characters allowed |
|---|---|
| AllowCurrencySymbol | Digits and a $ sign |
| AllowDecimalPoint | Digits and a decimal point |
| AllowLeadingWhiteSpace | Digits and leading whitespace |
| AllowTrailingWhiteSpace | Digits and trailing whitespace |
| AllowLeadingSign | Digits and a leading sign |
| AllowTrailingSign | Digits and a trailing sign |
| AllowParentheses | Parentheses around the digits to indicate a negative value |
| AllowThousands | Digits and commas used as thousands separators |
| Currency | Digits and all of the characters listed above |
| Number | Digits and all of the characters listed above except for a $ sign and parentheses |
| None | Digits only |

# A Parse() method that allows entries with any of the content above

```
decimal invoiceTotal = Decimal.Parse(txtTotal.Text, NumberStyles.Currency);
```

# A TryParse() method that allows entries with a $ sign and a decimal point

```
Decimal.TryParse(txtTotal.Text,
    NumberStyles.AllowCurrencySymbol | NumberStyles.AllowDecimalPoint,
    CultureInfo.CurrentCulture, out decimal invoiceTotal);
```

# Description

+   - By default, commas, a decimal point, and leading and trailing spaces are allowed in a decimal value when you use the Parse() or TryParse() method.
+   - If you want to restrict the characters that can be entered or if you want to allow additional characters, you can use the second argument of the Parse() or TryParse() method. Then, if any other characters are entered, an exception will occur.
+   - To indicate the characters that are allowed, you use the members of the NumberStyles enumeration. You can combine two or more members of this enumeration by coding a pipe character (|) between them as shown in the second example above.
+   - The Parse() and TryParse() methods remove any of the specified characters from the string that aren’t allowed by the numeric data type before the value is assigned to that data type.
+   - When you use this syntax of the TryParse() method, you also have to include a format provider that specifies culture-specific parsing information. In most cases, you’ll code this argument as shown above.
+   - The NumberStyles enumeration is in the System.Globalization namespace.