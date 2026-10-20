# The syntax for creating a DateTime value

```
DateTime variableName = new DateTime(year, month, day
    [, hour, minute, second[, millisecond]]);
```

# How to create a DateTime value using the Parse() method

```
DateTime variableName = DateTime.Parse(string);
```

# How to create a DateTime value using the TryParse() method

```
DateTime.TryParse(string, out DateTime variableName);
```

# Statements that create DateTime values

```
DateTime startDate = new DateTime(2020, 01, 30);      // 1/30/2020 12:00 AM
DateTime startDateAndTime =
    new DateTime(2020, 1, 30, 14, 15, 0);      // 1/30/2020 2:15 PM

DateTime startDate = DateTime.Parse("01/30/20");      // 1/30/2020 12:00 AM
DateTime startDateAndTime
    = DateTime.Parse("Jan 30, 2020 2:15 PM");      // 1/30/2020 2:15 PM
DateTime invoiceDate = DateTime.Parse(txtInvoiceDate.Text);

DateTime.TryParse(txtInvoiceDate.Text, out DateTime invoiceDate);
```

# Valid date formats

+   - 01/30/2020
+   - 1/30/20
+   - 01-01-2020
+   - 1-1-20
+   - 2020-01-01
+   - Jan 30 2020
+   - January 30, 2020

# Valid time formats

+   - 2:15 PM
+   - 14:15
+   - 02:15:30 AM

# Description

+   - You can use the DateTime structure of .NET to create and work with dates and times.
+   - To create a DateTime value, you can use the new keyword and then specify the date and time values you want to use to create the date.
+   - You can also use the static Parse() or TryParse() method of the DateTime structure to create a DateTime value from a string.
+   - If you omit the time specification when you create a DateTime value, the time is set to 12:00 AM. You can also omit the date specification when you create a DateTime value using the Parse() or TryParse() method. Then, the date is set to the current date.
+   - A date is stored as a 64-bit signed integer that represents the number of ticks (100 nanosecond units) that have elapsed since 12:00 AM, January 1, 0001.