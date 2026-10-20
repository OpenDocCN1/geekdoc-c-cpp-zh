# The syntax for a try-catch statement that accesses the exception

```
try { statements }
catch(ExceptionClass exceptionName) { statements }
```

# Two common properties for all exceptions

| Property | Description |
|---|---|
| Message | Gets a message that briefly describes the current exception. |
| StackTrace | Gets a string that lists the methods that were called before the exception occurred. |

# A common method for all exceptions

| Method | Description) |
|---|---|
| GetType() | Gets the type of the current exception. |

# A try-catch statement that accesses the exception

```
try
{
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
}
catch(Exception ex)
{
    MessageBox.Show(ex.Message + "\n\n" + ex.GetType().ToString() + "\n" + ex.StackTrace, "Exception");
}
```

# The dialog box that’s displayed if an exception occurs

![](bbox=[0.155, 0.529, 0.522, 0.715])

# Description

+   - If you want to use the properties or methods of the exception in the catch block, you must supply a name for the exception.
+   - The stack trace is a list of the methods that were called before the exception occurred. The list appears in reverse order, from the last method called to the first method called.

# Note

+   - If you’re coding the try-catch statement within an event handler, you can’t use e for the name of the exception because it’s used as the name of a parameter for the handler.