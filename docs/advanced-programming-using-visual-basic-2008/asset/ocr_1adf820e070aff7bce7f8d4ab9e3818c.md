Remember, the private module-level variable holds the value of the property. The Property Get and Set retrieve the current value and assign a new value to the property.

# Read-Only and Write-Only Properties

In some instances, you may wish to set a value for a property that can only be retrieved by an object but not changed. To create a read-only property, use the **ReadOnly** modifier and write only the Get portion of the property procedure. Security recommendations are to not include a Set procedure unless one is needed for your application or for class inheritance.

```
Private PayDecimal As Decimal    ' Declared at the module level.

Public ReadOnly Property Pay() As Decimal    ' Make the property read-only.
    Get
        Return PayDecimal
    End Get
End Property
```

A write-only property is one that can be set but not returned. Use the **WriteOnly** modifier and write only the Set portion of the property procedure:

```
Private PasswordString As String    ' Declared at the module level.

Public WriteOnly Property Password() As String    ' Make it write-only.
    Set(ByVal Value As String)
        PasswordString = Value
    End Set
End Property
```

# Constructors and Destructors

A constructor is a method that automatically executes when a class is instantiated. A destructor is a method that automatically executes when an object is destroyed. In VB, the constructor must be a procedure named **New**. The destructor must be named **Dispose** and must override the Dispose method of the base class. You will generally write constructors for your classes, but usually not destructors. Most of the time the Dispose method of the base class handles the class destruction very well.

You create a constructor for your class by writing a Sub New procedure. The constructor executes automatically when you instantiate an object of the class. Because the constructor method executes before any other code in the class, the constructor is an ideal location for any initialization tasks that you need to do, such as opening a database connection.

The Sub New procedure must be Public or Protected because the objects that you create must execute this method. Remember that the default is Public.

```
Sub New()
    ' Constructor for class.

    ' Initialization statements.
End Sub
```