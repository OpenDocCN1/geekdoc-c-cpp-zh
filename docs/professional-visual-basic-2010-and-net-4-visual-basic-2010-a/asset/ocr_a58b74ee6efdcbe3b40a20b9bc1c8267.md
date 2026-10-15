```
Property Name As Object
Property Salary As Object
Property HireDate As Object
End Class
```

Code snippet from Person

Notice that the three properties have all been created as Objects, and the parameters to the constructor — while correct — do not have very descriptive names. Therefore, the code for the class can be cleaned up a little: Give the parameters to the constructor more useful names, and apply the correct data types to the three properties. While you’re in there, you might as well add a bit of validation to the Salary property, prohibiting negative values. After editing the Employee class, it should look as follows:

```
Public Class Employee
    Private _name As String
    Private _salary As Decimal
    Private _hireDate As Date

    Sub New(ByVal name As String,
            ByVal salary As Decimal,
            ByVal hireDate As Date)
        Me.Name = name
        Me.Salary = salary
        Me.HireDate = hireDate
    End Sub
    Sub New()
        Me.Name = String.Empty
        Me.Salary = Decimal.Zero
        Me.HireDate = DateTime.MinValue
    End Sub
    Property Name As String
        Get
            Return _name
        End Get
        Set(ByVal value As String)
            _name = value
        End Set
    End Property
    Property Salary As Decimal
        Get
            Return _salary
        End Get
        Set(ByVal value As Decimal)
            If value < 0 Then
                Throw New ArgumentOutOfRangeException("Salary cannot be negative")
            End If
            _salary = value
        End Set
    End Property
    Property HireDate As Date
        Get
            Return _hireDate
        End Get
        Set(ByVal value As Date)
            _hireDate = value
        End Set
    End Property
End Class
```

Code snippet from Person

The short version of the properties for Name and HireDate could be left as is, because you don’t perform any validation in them. Notice that rather than write directly to the private member variables, the