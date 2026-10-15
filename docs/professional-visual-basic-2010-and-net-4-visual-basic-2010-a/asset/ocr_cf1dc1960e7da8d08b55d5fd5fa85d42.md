In this case, you will use a Private method, so it is only providing implementation for the IPrintableObject interface. Implement the Label method by adding the following code to Employee:

```
Private Function Label(ByVal index As Integer) As String _
    Implements IPrintableObject.Label

    Return mLabels(index)
End Function
```

This is just a regular Private method that returns a String value from the pre-initialized array. The interesting part is the Implements clause on the method declaration:

```
Private Function Label(ByVal index As Integer) As String _
    Implements IPrintableObject.Label
```

By using the Implements keyword in this fashion, you are indicating that this particular method is the implementation for the Label method on the IPrintableObject interface. The actual name of the private method could be anything. It is the use of the Implements clause that makes this work. The only requirement is that the parameter data types and the return value data type must match those defined by the IPrintableObject interface method.

This is very similar to using the Handles clause to indicate which method should handle an event. In fact, like the Handles clause, the Implements clause allows you to have a comma-separated list of interface methods that should be implemented by this one function.

You can then move on to implement the other two elements defined by the IPrintableObject interface by adding this code to Employee:

```
Private Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value

    Select Case index
        Case 0
            Return CStr(EmployeeNumber)
        Case 1
            Return CStr(Age)
        Case Else
            Return Format(HireDate, "Short date")
    End Select
End Function

Private ReadOnly Property Count() As Integer _
    Implements IPrintableObject.Count
    Get
        Return UBound(mLabels)
    End Get
End Property
```

You can now run this application and click the button. The output window in the IDE will display your results, showing the ID, age, and hire-date values as appropriate.

Any object could create a similar implementation behind the IPrintableObject interface, and the PrintObject routine in your form would continue to work, regardless of the native data type of the object itself.

# Reusing a Common Implementation

Secondary interfaces provide a guarantee that all objects implementing a given interface have exactly the same methods and events, including the same parameters.