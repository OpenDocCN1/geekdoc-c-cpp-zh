```
```vb
' and override Finalize() below.
' TODO: set large fields to null.
End If
Me.disposedValue = True
End Sub

' TODO: override Finalize() only if Dispose(ByVal disposing As Boolean) above
'       has code to free unmanaged resources.
Protected Overrides Sub Finalize()
    ' Do not change this code.  Put cleanup code in
    '     Dispose(ByVal disposing As Boolean) above.
    Dispose(False)
    MyBase.Finalize()
End Sub

' This code added by Visual Basic to correctly implement the disposable pattern.
Public Sub Dispose() Implements IDisposable.Dispose
    ' Do not change this code.  Put cleanup code in
    '     Dispose(ByVal disposing As Boolean) above.
    Dispose(True)
    GC.SuppressFinalize(Me)
End Sub
#End Region
```
```

Notice the use of the `Overridable` and `Overrides` keywords. The automatically inserted code is following a best-practice design pattern for implementation of the `IDisposable` interface and the `Finalize` method. The idea is to centralize all cleanup code into a single method that is called by either the `Dispose` method or the `Finalize` method as appropriate.

Accordingly, you can add the cleanup code as noted by the TODO: comments in the inserted code. As mentioned in Chapter 1, the TODO: keyword is recognized by Visual Studio’s text parser, which triggers an entry in the task list to remind you to complete this code before the project is complete. Because this code frees a managed object (the `Hashtable`), it appears as shown here:

```
```vb
Protected Overridable Sub Dispose(ByVal disposing As Boolean)
    If Not Me.disposedValue Then
        If disposing Then
            ' TODO: dispose managed state (managed objects).
        End If
        ' TODO: free unmanaged resources (unmanaged objects)
        ' and override Finalize() below.
        ' TODO: set large fields to null.
    End If
    Me.disposedValue = True
End Sub
```
```

In this case, we’re using this method to release a reference to the object to which the `mPhones` variable points. While not strictly necessary, this illustrates how code can release other objects when the `Dispose` method is called. Generally, it is up to your client code to call this method at the appropriate time to ensure that cleanup occurs. Typically, this should be done as soon as the code is done using the object.

This is not always as easy as it might sound. In particular, an object may be referenced by more than one variable, and just because code in one class is dereferencing the object from one variable doesn’t mean that it has been dereferenced by all the other variables. If the `Dispose` method is called while other references remain, then the object may become unusable and cause errors when invoked via those other references. There is no easy solution to this problem, so careful design is required if you choose to use the `IDisposable` interface.

![](bbox=[0.613, 0.406, 0.932, 0.423])

![](bbox=[0.613, 0.733, 0.932, 0.75])