One second later, the main thread communicates a request for cancellation for both tasks through the `CancellationTokenSource` instance’s `Cancel` method:

```
cts.Cancel()
```

The cancellation token is evaluated in the two delegates launched by the Task instances, as previously explained.

Adding a few lines, it is indeed easy to cancel asynchronous actions. However, it is very important to add the necessary clean-up code.

A `Try...Catch...End Try` block encloses the call to `Task.WaitAll`. Because there was a request for cancellation for both tasks, there will be two benign exceptions of type `OperationCanceledException`.

The `IsCanceled` property for both tasks is going to be True. Checking this property, you can add code whenever a task was cancelled.

# Handling Exceptions Thrown by Tasks

As many tasks run in parallel, many exceptions can occur in parallel. Task instances also work with a set of exceptions, handled by the previously explained `System.AggregateException` class.

Listing 33-15 shows the highlighted lines that add an unhandled exception in the GenerateAESKeysCancel subroutine.

Comment the code that requested cancellation for both tasks:

```
' cts.Cancel()
```

**LISTING 33-15: An unhandled exception in the subroutine called by an asynchronous delegate**

```vb
Sub GenerateAESKeysCancel(ByVal ct As System.Threading.CancellationToken)
    ct.ThrowIfCancellationRequested()
    Dim sw = Stopwatch.StartNew()
    Dim aesM As New AesManaged()
    Dim result() As Byte
    Dim hexString As String
    For i As Integer = 1 To NUM_AES_KEYS
        aesM.GenerateKey()
        result = aesM.Key
        hexString = ConvertToHexString(result)
        ' Console.WriteLine("AES: " + hexString)
        If (sw.Elapsed.Seconds > 0.5) Then
            Throw New TimeoutException("GenerateAESKeysCancel is taking more than 0.5 seconds to complete.")
        End If
        If ct.IsCancellationRequested Then
            ct.ThrowIfCancellationRequested()
        End If
    Next
    Debug.WriteLine("AES: " + sw.Elapsed.ToString())
End Sub
```

Add the following lines to the Main subroutine:

```
If t1.IsFaulted Then
    For Each innerEx As Exception In t1.Exception.InnerExceptions
        Debug.WriteLine(innerEx.ToString())
        ' Do something else considering the innerEx Exception
    Next
End If
```