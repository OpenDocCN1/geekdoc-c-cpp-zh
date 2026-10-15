

```vb
Catch excGeneric As Exception
' You'll get here when any exception is thrown and not caught in
' a previous Catch block.
    MessageBox.Show("Calculation failed - generic exception caught")
    Throw excGeneric
Finally
' Code in the Finally block will always run, even if
' an exception was thrown in a Catch block.
    MessageBox.Show("You always get here, with or without an error")
End Try
End Function
```

Code snippet from ExceptionHandlingSampleCodeForm

此代码可以从一个按钮调用，其调用 GetAverage3 的代码类似。只需将调用的函数名称更改为 GetAverage4 即可。

这种技术特别适用于处理属性过程中检测到的问题。Property Set 逻辑通常包括检查属性是否即将被赋予有效值。如果不是，则抛出新的 ArgumentException（而不是分配属性值）是告知调用代码问题的良好方法。

## The Exit Try Statement

Exit Try 语句将在给定情况下，跳出 Try 或 Catch 块并继续执行 Finally 块。在下面的示例中，如果 iItems 的值为 0，则会退出 Catch 块，因为你知道错误是由该问题引起的：

```vb
Private Function GetAverage5(iItems As Integer, iTotal As Integer) As Single
    ' Code that might throw an exception is wrapped in a Try block.
    Try
        Dim sngAverage As Single
        ' This will cause an exception to be thrown.
        sngAverage = CSng(iTotal \ iItems)
        ' This only executes if the line above generated no error.
        MessageBox.Show("Calculation successful")
        Return sngAverage
    Catch excDivideByZero As DivideByZeroException
        ' You'll get here with a DivideByZeroException in the Try block.
        If iItems = 0 Then
            Exit Try
        Else
            MessageBox.Show("Error not caused by iItems")
        End If
        Throw excDivideByZero
        MessageBox.Show("More logic after the thrown - never executed")
    Catch excGeneric As Exception
        ' You'll get here when any exception is thrown and not caught in
        ' a previous Catch block.
        MessageBox.Show("Calculation failed - generic exception caught")
        Throw excGeneric
    Finally
        ' Code in the Finally block will always run, even if
        ' an exception was thrown in a Catch block.
        MessageBox.Show("You always get here, with or without an error")
    End Try
End Function
```

Code snippet from ExceptionHandlingSampleCodeForm

在第一个 Catch 块中，你插入了一个 If 块，以便在特定条件下退出该块（在本例中，如果溢出异常是因为 iItems 的值为 0 导致）。Exit Try 会立即转到 Finally 块并在那里完成处理：

```vb
If iItems = 0 Then
    Exit Try
Else
    MessageBox.Show("Error not caused by iItems")
End If
```

现在，如果溢出异常是由除零以外的其他原因引起，你将得到一个消息框，显示“Error not caused by iItems”。

## Nested Try Structures

有时 Try 块中的特定行可能需要特殊的异常处理。此外，错误也可能在 Try 结构的 Catch 部分中发生并导致进一步的异常抛出。对于这两种情况，都可以使用嵌套的 Try 结构。你可以修改“Throw 关键字”部分下的示例来演示以下代码：

```vb
Private Function GetAverage6(iItems As Integer, iTotal As Integer) As Single
    ' Code that might throw an exception is wrapped in a Try block.
    Try
        Dim sngAverage As Single
        ' Do something for performance testing...
        Try
            LogEvent("GetAverage6")
        Catch exc As Exception
            MessageBox.Show("Logging function unavailable")
        End Try
        ' This will cause an exception to be thrown.
        sngAverage = CSng(iTotal \ iItems)
        ' This only executes if the line above generated no error.
        MessageBox.Show("Calculation successful")
        Return sngAverage
    Catch excDivideByZero As DivideByZeroException
        ' You'll get here with a DivideByZeroException in the Try block.
        MessageBox.Show("Error not divide by 0")
        Throw excDivideByZero
        MessageBox.Show("More logic after the thrown - never executed")
    Catch excGeneric As Exception
        ' You'll get here when any exception is thrown and not caught in
        ' a previous Catch block.
        MessageBox.Show("Calculation failed - generic exception caught")
        Throw excGeneric
    Finally
        ' Code in the Finally block will always run, even if
        ' an exception was thrown in a Catch block.
        MessageBox.Show("You always get here, with or without an error")
    End Try
End Function
```

Code snippet from ExceptionHandlingSampleCodeForm

在前面的示例中，你假设存在一个用于记录事件的函数。该函数通常位于公共库中，并可能以各种方式记录事件。你将在本章后面详细了解记录异常，但一个简单的 LogEvent 函数可能如下所示：

```vb
Public Sub LogEvent(ByVal sEvent As String)
FileOpen(1, "logfile.txt", OpenMode.Append)
Print(1, DateTime.Now & " -" & sEvent & vbCrLf)
FileClose(1)
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

在这种情况下，你不希望记录事件时出现问题，例如“磁盘已满”错误导致例程崩溃。GetAverage6 函数的代码会触发一个消息框以指示日志函数出现问题。

Catch 块可以为空。在这种情况下，异常将被忽略。但是，执行不会从导致错误的下一行继续，而是从 Finally 块继续，或者如果没有 Finally 块，则从 End Try 之后的下一行继续。

## Using Exception Properties

之前的示例在消息框中显示了硬编码的消息，这显然不是生产应用程序的良好技术。相反，描述异常的消息框或日志条目应尽可能提供有关问题的详细信息。为此，可以使用异常的各种属性。

获取有关异常信息的最粗暴的方法是使用异常的 ToString 方法。假设你修改了 GetAverage2 的早期示例，以更改显示的异常信息，如下所示：

```vb
Private Function GetAverage2(ByVal iItems As Integer, ByVal iTotal As Integer) _
    As Single
' Code that might throw an exception is wrapped in a Try block.
Try
    Dim sngAverage As Single
    ' This will cause an exception to be thrown.
    sngAverage = CSng(iTotal \ iItems)
    ' This only executes if the line above generated no error.
    MessageBox.Show("Calculation successful")
    Return sngAverage
Catch excDivideByZero As DivideByZeroException
    ' You'll get here with a DivideByZeroException in the Try block.
    MessageBox.Show(excDivideByZero.ToString)
    Throw excDivideByZero
    MessageBox.Show("More logic after the thrown - never executed")
Catch excGeneric As Exception
    ' You'll get here when any exception is thrown and not caught in
    ' a previous Catch block.
    MessageBox.Show("Calculation failed - generic exception caught")
    Throw excGeneric
Finally
    ' Code in the Finally block will always run, even if
    ' an exception was thrown in a Catch block.
    MessageBox.Show("You always get here, with or without an error")
End Try
End Function
```

Code snippet from ExceptionHandlingSampleCodeForm

当函数以 iItems = 0 访问时，将显示类似于图 6-1 的消息框。

### The Message Property

图 6-1 中显示的消息对开发人员很有帮助，因为它包含大量信息，但这通常不是你希望用户看到的内容。相反，用户通常需要看到问题的简短描述，这由 Message 属性提供。

如果将之前的代码更改为使用 Message 属性而不是 ToString，则消息框将提供类似于图 6-2 所示的内容。

![](img/d99870e80390742f93963da7be0b2e61_294_0.png)

FIGURE 6-1

![](img/d99870e80390742f93963da7be0b2e61_294_1.png)

FIGURE 6-2

### The InnerException and TargetSite Properties

InnerException 属性用于存储异常跟踪。当发生多个异常时，这非常有用。异常发生时设置导致进一步异常产生的条件的情况很常见。随着异常按顺序发生，你可以选择使用 Exception 对象的 InnerException 属性将它们堆叠起来以供以后参考。随着每个异常加入堆栈，先前的 Exception 对象成为堆栈中的内部异常。

为了简单起见，你将启动一个新的代码示例，其中只包含一个生成自身异常的子例程。你将包含代码以将对 InnerException 对象的引用添加到你使用 Throw 方法生成的异常中。

此示例还包含一个消息框来显示异常的 TargetSite 属性中存储的内容。如结果所示，TargetSite 将包含生成异常的例程的名称——在本例中为 HandlerExample。以下是代码：

```vb
Sub HandlerExample()
    Dim intX As Integer
    Dim intY As Integer
    Dim intZ As Integer
    intY = 0
    intX = 5
    ' First Required Error Statement.
    Try
        ' Cause a "Divide by Zero"
        intZ = CType((intX \ intY), Integer)
        ' Catch the error.
    Catch objA As System.DivideByZeroException
        Try
            Throw (New Exception("0 as divisor", objA))
        Catch objB As Exception
            Dim sError As String
            sError = "My Message: " & objB.Message & vbCrLf & vbCrLf
            sError &= "Inner Exception Message: " & _
            objB.InnerException.Message & vbCrLf & vbCrLf
            sError &= "Method Error Occurred: " & objB.TargetSite.Name
            MessageBox.Show(sError)
        End Try
    Catch
```

