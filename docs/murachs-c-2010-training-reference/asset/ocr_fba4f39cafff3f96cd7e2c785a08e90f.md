# Common methods for data conversion

| Method | Description |
| --- | --- |
| ToString([format]) | A method that converts the value to its equivalent string representation using the specified format. If the format is omitted, the value isn't formatted. |
| Parse(string) | A static method that converts the specified string to an equivalent value. |

# Some of the static methods of the Convert class

| Method | Description |
| --- | --- |
| ToDecimal(value) | Converts the value to the decimal data type. |
| ToDouble(value) | Converts the value to the double data type. |
| ToInt32(value) | Converts the value to the int data type. |
| ToChar(value) | Converts the value to the char data type. |
| ToBool(value) | Converts the value to the bool data type. |
| ToString(value) | Converts the value to a string object. |

# Conversion statements that use the ToString and Parse methods

```
decimal sales = 2574.98m;
string salesString = sales.ToString(); // decimal to string
sales = Decimal.Parse(salesString); // string to decimal
```

# An implicit call of the ToString method

```
double price = 49.50;
string priceString = "Price: $" + price; // automatic ToString call
```

# Conversion statements that use the Convert class

```
decimal subtotal = Convert.ToSubtotal(txtSubtotal.Text); // string to decimal
int years = Convert.ToInt32(txtYears.Text); // string to int
txtSubtotal.Text = Convert.ToString(subtotal); // decimal to string
int subtotalInt = Convert.ToInt32(subtotal); // decimal to int
```

# Description

+   - The ToString and Parse methods are included in all of the data structures.
- In some situations where a string is expected, the compiler will automatically call the ToString method.
- The Convert class contains static methods for converting all of the built-in types. By all of this class, you can use Visual Studio's help to look up the Convert class.

![](bbox=[0.061, 0.943, 0.558, 0.963])