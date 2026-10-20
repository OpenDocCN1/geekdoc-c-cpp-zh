# A method that executes a single statement

```
private void DisplayErrorMessage(string message, string caption)
{
    MessageBox.Show(message, caption);
}
```

# The same method with an expression body

```
private void DisplayErrorMessage(string message, string caption) =>
    MessageBox.Show(message, caption);
```

# A method that returns the value of an expression

```
private decimal GetDiscountPercent(string customerType)
{
    return customerType switch
    {
        "R" => .1m,
        "C" => .2m,
        "T" => .4m,
        _ => .0m
    };
}
```

# The same method with an expression body

```
private decimal GetDiscountPercent(string customerType) =>
    customerType switch
    {
        "R" => .1m,
        "C" => .2m,
        "T" => .4m,
        _ => .0m
    };
```

# Description

+   - With C# 6.0 and later, you can code a method that executes a single statement or returns an expression as an expression-bodied method.
+   - To code an expression-bodied method, you code the method signature, followed by the lambda operator (=>) and an expression or executable statement.
+   - Although you can code expression-bodied methods within a form class, you’re more likely to code them within user-defined classes. You can learn more about that in chapter 12.