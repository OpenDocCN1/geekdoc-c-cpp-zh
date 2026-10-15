```
TextBox1.Text &= "Time to concatenate strings: " &
(Now().Subtract(start)).TotalMilliseconds().ToString() &
" String length: " & strRedo.Length.ToString()
TextBox1.Text &= line & Environment.NewLine
```

Code snippet from Form1

This code does not perform well. For each assignment operation on the strMyString variable, the system allocates a new memory buffer based on the size of the new string, and copies both the current value of strMyString and the new text that is to be appended. The system then frees the previous memory that must be reclaimed by the garbage collector. As this loop continues, the new memory allocation requires a larger chunk of memory. Therefore, operations such as this can take a long time.

To illustrate this, you'll note that the code captures the start time before doing the 10,000 concatenations, and then within the print statement uses the DateTime.Subtract method to get the difference. That difference is returned as an object of type Timespan, between the start time and the print time. This difference is then expressed in milliseconds (refer to Figure 2-8).

However, .NET offers an alternative in the System.Text.StringBuilder object, shown in the following snippet:

```
start = Now()
Dim strBuilder = New System.Text.StringBuilder("A simple string")
For index = 1 To 1000000 '1 million times....
    strBuilder.Append("Making a much larger string")
Next
TextBox1.Text &= "Time to concatenate strings: " &
(Now().Subtract(start)).TotalMilliseconds().ToString() &
" String length: " & strBuilder.ToString().Length.ToString()
TextBox1.Text &= line & Environment.NewLine
End Sub
```

Code snippet from Form1

The preceding code works with strings but does not use the String class. The .NET class library contains the System.Text.StringBuilder class, which performs better when strings will be edited repeatedly. This class does not store strings in the conventional manner; it stores them as individual characters, with code in place to manage the ordering of those characters. Thus, editing or appending more characters does not involve allocating new memory for the entire string. Because the preceding code snippet does not need to reallocate the memory used for the entire string, each time another set of characters is appended it performs significantly faster.

Note that the same timing code is used in this snippet. However, for the StringBuilder, the loop executes one million times (versus ten thousand). Note the increase in the number of iterations was made in order to cause enough of a delay to actually show it requiring more than just one or two milliseconds to complete. Even with 100 times the number of iterations, Figure 2-8 still illustrates that this is a much more efficient use of system resources.

Ultimately, an instance of the String class is never explicitly needed, because the StringBuilder class implements the ToString method to roll up all of the characters into a string. While the concept of the StringBuilder class isn't new, because it is available as part of the Visual Basic implementation, developers no longer need to create their own string memory managers.

# String Constants

If you ever have to produce output based on a string you'll quickly find yourself needing to embed certain constant values. For example, it's always useful to be able to add a carriage-return linefeed combination to trigger a new line in a message box. One way to do this is to learn the underlying ASCII codes and then embed these control characters directly into your String or StringBuilder object.

Visual Basic provides an easier solution for working with these: the Microsoft.VisualBasic.Constants class. The Constants class, which you can tell by its namespace is specific to Visual Basic, contains definitions for several standard string values that you might want to embed. The most common, of course,