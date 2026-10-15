```
Set(ByVal value As String)
    mName = value
End Set
End Property
```

Code snippet from Person

With that done, the Name method can now be overridden by any derived class. In the Employee class, you can now override the Name method, replacing the functionality provided by the Person class. First, add a Normal option to the Enum that controls the types of Name value you can store:

```
Public Enum NameTypes
    Informal = 1
    Formal = 2
    Normal = 3
End Enum
```

Now you can add code to the Employee class to implement a new Name property. This is in addition to the existing Name property already implemented in the Employee class:

```
Public Overloads Overrides Property Name() As String
    Get
        Return mNames(NameTypes.Normal)
    End Get
    Set(ByVal value As String)
        mNames(NameTypes.Normal) = value
    End Set
End Property
```

Code snippet from Person

Note that you are using both the Overrides keyword (to indicate that you are overriding the Name method from the base class) and the Overloads keyword (to indicate that you are overloading this method in the subclass).

This new Name property merely delegates the call to the existing version of the Name property that handles the parameter-based names. To complete the linkage between this implementation of the Name property and the parameter-based version, you need to make one more change to that original overloaded version:

```
Public Overloads Property Name(ByVal type As NameTypes) As String
    Get
        Return mNames(Type)
    End Get
    Set(ByVal value As String)
        If mNames.ContainsKey(type) Then
            mNames.Item(type) = value
        Else
            mNames.Add(type, value)
        End If

        If type = NameTypes.Normal Then
            MyBase.Name = value
        End If
    End Set
End Property
```

Code snippet from Person

This way, if the client code sets the Name property by providing the Normal index, you are still updating the name in the base class as well as in the Dictionary object maintained by the Employee class.

# Shadowing

Overloading enables you to add new versions of existing methods as long as their parameter lists are different. Overriding enables your subclass to entirely replace the implementation of a base-class method