The compiler will generate the following code:

```
Public Sub New()
Me.CustomerName = "Unknown"
Me.OrderDate = DateTime.Now.Date
Dim temp_var = New List(Of OrderItem)
Me.Items = temp_var
End Sub
```

```
Public Sub New(ByVal initialID As Integer)
Me.CustomerName = "Unknown"
Me.OrderDate = DateTime.Now.Date
Dim temp_var = New List(Of OrderItem)
Me.Items = temp_var
Me.ID = initialID
End Sub
```

Following are a few restrictions concerning default values for auto-implemented properties:

+   - You cannot initialize an auto-implemented property that is a member of an Interface or one that is marked Override.

+   - When you declare an auto-implemented property as a member of a Structure, you can only initialize the auto-implemented property if it is marked as Shared.

+   - When you declare an auto-implemented property as an array, you cannot specify explicit array bounds. However, you can supply a value by using an array initializer, and the array bounds are inferred from this initializer.

You cannot use auto-implemented properties in every case. Following are the cases when you must use the standard property syntax:

+   - You want the Get and Set procedures to have different accessibilities.

+   - You need ReadOnly or WriteOnly or parameterized properties.

+   - You want to add code for the Get or Set procedures.

+   - You need to extend the backing field with attributes or comments.

# Collection Initializers

Visual Basic provides you with a syntax to set the initial values of arrays:

```
Dim PrimesUnder50() As Integer = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43}
Dim SeaCreatures() As String = {"Stingray","Potato cod","Surgeon fish","Anemone fish","Grey shark","stonefish"}, \_
```

However, if PrimesUnder50 and SeaCreatures were not arrays, but collections (for example, lists), with Visual Basic 2008, you must initialize them with longer procedural code:

```
Dim PrimesUnder50 As New List(Of Integer)
PrimesUnder50.Add(2)
PrimesUnder50.Add(3)
```