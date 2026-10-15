# TABLE 6-8: Common Debug Object Methods

| METHOD | DESCRIPTION |
| --- | --- |
| Assert | Checks a condition and displays a message if False |
| Close | Executes a flush on the output buffer and closes all listeners |
| Fail | Emits an error message in the form of an Abort/Retry/Ignore message box |
| Flush | Flushes the output buffer and writes it to the listeners |
| Write | Writes bytes to the output buffer |
| WriteLine | Writes characters followed by a line terminator to the output buffer |
| WriteIf | Writes bytes to the output buffer if a specific condition is True |
| WriteLineIf | Writes characters followed by a line terminator to the output buffer if a specific condition is True |

The following example shows how you can open an existing file (called mytext.txt) for output and assign it to the Listeners object of the Debug object so that it can catch your Debug.WriteLine statements:

```
Sub LoggingExample2()
    Dim objWriter As New _
        IO.StreamWriter("C:\mytext.txt", True)
    Debug.Listeners.Add(New TextWriterTraceListener(objWriter))
    Try
        Throw (New EntryPointNotFoundException())
    Catch objA As System.EntryPointNotFoundException
        Debug.WriteLine(objA.Message)
        objWriter.Flush()
        objWriter.Close()
        objWriter = Nothing
    End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

Looking in detail at this code, you first create a StreamWriter that is assigned to a file in your local file system:

```
Dim objWriter As New _
    IO.StreamWriter("C:\mytext.txt", True)
```

You then assign your StreamWriter to a debug listener by using the Add method:

```
Debug.Listeners.Add(New TextWriterTraceListener (objWriter))
```

This example forces an exception and catches it, writing the Message property of the Exception object (which is "Entry point was not found") to the debug buffer through the WriteLine method:

```
Debug.WriteLine(objA.Message)
```

Finally, you flush the listener buffer to the output file and free your resources:

```
objWriter.Flush()
objWriter.Close()
objWriter = Nothing
```

After running this code, you can examine the c:\mytext.txt file to see the trace output.

# SUMMARY

This chapter reviewed the Exception object and the syntax available to work with exceptions. You have looked at the various properties of exceptions and learned how to use the exposed information. You have also seen how to promote exceptions to consuming code using the Throw statement, and how structured exception