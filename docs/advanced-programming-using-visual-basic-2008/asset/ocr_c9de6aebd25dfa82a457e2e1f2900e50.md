# Writing a Filter

The rules for creating a filter are the same as for a WHERE clause of a SQL statement. Specify the field, a comparison operator (usually the equal sign), and the value to match.

```
"LastName = Jones"
"SalesAmount = 1000"
"Quantity > 0"
```

The tricky part comes when you want to filter on a string that may contain spaces. The value to match must be enclosed in single quotes.

```
"Title = 'A Great Book'"
```

If you are matching a value stored in a variable, you must concatenate the elements to create a filter string in the correct format. For string data, you must concatenate the single quotes around the data values:

```
"Title = '" & TitleString & "'"
"Title = '" & TitleComboBox.SelectedValue.ToString & "'"
```

In the second statement, assume that TitleComboBox.SelectedValue = "Great Expectations". After the concatenation, the entire string would be "Title = 'Great Expectations'", which is exactly what is needed for the filter.

For numeric values, you create a filter string without the quotes:

```
"SalesAmount = " & AmountDecimal.ToString
"Quantity > " & QuantityTextBox.Text
```

Here is a list of the most useful operators. You can find a complete listing of operators on the "Comparison Operators" page in MSDN.

| Operator | Meaning | Examples |
|---|---|---|
| = | equal to | "Subject = 'Business'"
"Subject = '" & SubjectTextBox.Text & "'" |
| > | greater than | "Sales > 1000"
"Sales > " & SalesTextBox.Text |
| < | less than | "Sales < 1000"
"Sales < " & SalesTextBox.Text |
| Like | pattern match | "Subject Like ('B%')" (For SQL Server databases)
"Subject Like 'B*' (For Access databases) |

# Binding a List at Run Time

When you display filtered data in a list, usually you want the list to appear empty until a selection is made. In that case, you must bind the control in code, rather than at design time.