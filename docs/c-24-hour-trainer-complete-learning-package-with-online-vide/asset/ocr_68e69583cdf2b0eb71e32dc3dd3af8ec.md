A try-catch block must include at least one `catch` block or the `finally` block, although none of them needs to contain any code. For example, the following code catches and ignores all exceptions:

```
try
{
    ...codeToProtect...
}
catch
{
}
```

The code in the `finally` block executes whether or not an exception occurs. If an error occurs, the program executes a `catch` block (if one matches the exception) and then executes the `finally` block. If no error occurs, the program executes the `finally` block after it finishes the `codeToProtect` code.

In fact, if the code inside the `try` or `catch` section executes a `return` statement, the `finally` block still executes before the program actually leaves the method! The `finally` block executes no matter how the code leaves the `try-catch` block.

# TRYPARSE

One place where problems are likely to occur is when a program parses text entered by the user. Even if users don't enter obviously ridiculous values such as "twelve," they might enter values in a format that you don't expect. For example, you might expect the user to enter an integer dollar amount such as 1200 but the user enters $1,200.00. If you use the decimal data type's `Parse` method and don't allow the currency symbol, thousands separator, and decimal point, the `Parse` method will throw an exception.

You can use a `try-catch` block to handle the exception, but it's more efficient to detect the invalid format instead. To do that, you can use the decimal data type's `TryParse` method.

A data type's `TryParse` method attempts to parse some text and save the result in a parameter passed with the `out` keyword. The `TryParse` method returns `true` if it successfully parsed the text and `false` if it could not.

For example, the following code tries to parse a value entered by the user:

```
decimal amount;
if (!decimal.TryParse(amountTextBox.Text, out amount))
{
    MessageBox.Show("Invalid format for amount: " +
        "\r\nThe amount should be an integer such as 12.");
    return;
}
```

The code uses `decimal.TryParse` to try to parse the value in `amountTextBox`. If `TryParse` returns `false`, the code displays an error message and then uses a `return` statement to stop processing the value.