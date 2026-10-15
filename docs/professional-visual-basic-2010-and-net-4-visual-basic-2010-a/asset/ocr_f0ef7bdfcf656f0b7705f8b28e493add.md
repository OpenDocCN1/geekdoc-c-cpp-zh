Though a Property method is a single structure, it is divided into two parts: a getter and a setter. The getter is contained within a Get...End Get block and is responsible for returning the value of the property on demand:

```
Get
    Return mName
End Get
```

Though the code in this example is very simple, it could be more complex, perhaps calculating the value to be returned, or applying other business logic to change the value as it is returned. Likewise, the code to change the value is contained within a Set...End Set block:

```
Set(ByVal Value As String)
    mName = Value
End Set
```

The Set statement accepts a single parameter value that stores the new value. The code in the block can then use this value to set the property's value as appropriate. The data type of this parameter must match the data type of the property itself. Declaring the parameter in this manner enables you to change the name of the variable used for the parameter value if needed.

By default, the parameter is named Value, but you can change the parameter name to something else, as shown here:

```
Set(ByVal NewName As String)
    mName = NewName
End Set
```

In many cases, you can apply business rules or other logic within this routine to ensure that the new value is appropriate before you actually update the data within the object. It is also possible to restrict the Get or Set block to be narrower in scope than the scope of the property itself. For instance, you may want to allow any code to retrieve the property value, but only allow other code in your project to alter the value. In this case, you can restrict the scope of the Set block to Friend, while the Property itself is scoped as Public:

```
Public Property Name() As String
    Get
        Return mName
    End Get
    Friend Set(ByVal Value As String)
        mName = Value
    End Set
End Property
```

Code snippet from Person

The new scope must be more restrictive than the scope of the property itself, and either the Get or Set block can be restricted, but not both. The one you do not restrict uses the scope of the Property method.

# Parameterized Properties

The Name property you created is an example of a single-value property. You can also create property arrays or parameterized properties. These properties reflect a range, or array, of values. For example, people often have several phone numbers. You might implement a PhoneNumber property as a parameterized property, storing not only phone numbers, but also a description of each number. To retrieve a specific phone number you would write code such as the following:

```
Dim myPerson As New Person()

Dim homePhone As String
homePhone = myPerson.Phone("home")
```

Code snippet from Person