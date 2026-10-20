```
```vb
End Property
Public Property name As String
Set(byval value As String)
Studentname = value
End Set
Get
Return studentname
End Get
End Property
Public Function percentage(byval i As Integer) As Single
Totalmarks = i
Return totalmarks / 4
End Function
End Class
```
```

# Form.vb

```
```vb
Public Class Form1
Private i As Short
```
```