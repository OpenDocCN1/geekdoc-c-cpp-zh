# Chapter 4 How to work with numeric and string data 121

# Standard numeric formatting codes

| Code | Format | Description |
|---|---|---|
| C c | Currency | Formats the number as currency with the specified number of decimal places. |
| P p | Percent | Formats the number as a percent with the specified number of decimal places. |
| N o n | Number | Formats the number with thousands separators and the specified number of decimal places. |
| F o r | Float | Formats the number as a decimal with the specified number of decimal places. |
| D o r d | Digits | Formats an integer with the specified number of digits. |
| E o r e | Exponential | Formats the number in scientific (exponential) notation with the specified number of decimal places. |
| G o r g | General | Formats the number as a decimal or in scientific notation depending on which is more compact |

# How to use the ToString method to format a number

| Statement | Example |
|---|---|
| string monthlyAmount = amount.ToString("c"); | $1,547.20 |
| string interestRate = interest.ToString("f1"); | 2.3% |
| string quantityString = quantity.ToString("n0"); | 15,000 |
| string paymentString = payment.ToString("f3"); | 432.818 |

# How to use the Format class to string a number

| Statement | Result |
|---|---|
| string monthlyAmount = String.Format("{0:c}", 1547.2m); | $1,547.20 |
| string interestRate = String.Format("{0:p1}", .023m); | 2.3% |
| string quantityString = String.Format("{0:n0}", 15000); | 15,000 |
| string paymentString = String.Format("{0:f3}", 432.8175); | 432.818 |

# The syntax of the format specification using the Format method

```
{index:formatCode}
```

# Description

+   - You can include a number after some of the numeric formatting codes to specify the number of decimal places in the result. If the numeric value contains more decimal places than are specified, the result will be rounded using standard rounding. If you don't specify the number of decimal places, the default is 2.
- You can include a number after the D or d formatting code to specify the minimum number of digits shown. If the integer has fewer digits than specified, zeros are added to the beginning of the integer.
- You can use the Format method of the String class to format two or more values. For more information, see chapter 9.

Figure 4-12 How to convert numbers to formatted strings