# 674 | CHAPTER 18 EXCEPTION HANDLING, DEBUGGING, TRACING

+   - Sending e-mail—The server may be down, or you may not have the permissions to access it.
- Accessing a database—The server may be down, you may not have permission to access it, you may get an error due to foreign constraint violations as you saw in Chapter 15, and so on.
- Trying to write an uploaded file to disk—The disk may be full, you may not have the necessary permissions to write to disk, or you are providing an invalid filename.

Although Try blocks are great to avoid exceptions from bubbling up to the user interface, you should use them with care, because they come at a cost. A Try Catch block is generally slower than code without, so you shouldn't use a Try Catch for errors you can avoid otherwise. Consider the following two examples:

# VB.NET

```
Dim value1 As Integer = Convert.ToInt32(ValueBox1.Text)
Dim value2 As Integer = Convert.ToInt32(ValueBox2.Text)
Try
    result = value1 / value2
    ResultLabel.Text = result.ToString()
Catch Ex As DivideByZeroException
    ResultLabel.Text = "Sorry, division by zero is not possible."
End Try
```

# C#

```
int value1 = Convert.ToInt32(ValueBox1.Text);
int value2 = Convert.ToInt32(ValueBox2.Text);
t{
    result = value1 / value2;
    ResultLabel.Text = result.ToString();
}
catch (DivideByZeroException ex) {
    ResultLabel.Text = "Sorry, division by zero is not possible.";
}
```

In this example, the code is set up to expect a DivideByZeroException. This exception is thrown when value2 contains the value 0. Although at first it seems like a good idea to implement exception handling, it is much better to use code that checks for this value before the division is carried out, instead of letting an exception occur.

# VB.NET

```
If value2 <> 0 Then
    result = value1 / value2
    ResultLabel.Text = result.ToString()
Else
    ResultLabel.Text = "Sorry, division by zero is not possible."
End If
```