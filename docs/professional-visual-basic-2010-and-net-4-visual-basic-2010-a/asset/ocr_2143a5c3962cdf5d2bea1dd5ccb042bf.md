You can implement an AmbientAllergens property as follows:

```
Public WriteOnly Property AmbientAllergens() As Integer
    Set(ByVal Value As Integer)
        mAllergens = Value
    End Set
End Property
```

To create a write-only property, use the WriteOnly keyword and only implement a Set block in the code. Because the property is write-only, you will get a syntax error if you try to implement a Get block.

# The Default Property

Objects can implement a default property, which can be used to simplify the use of an object at times by making it appear as if the object has a native value. A good example of this behavior is the Collection object, which has a default property called Item that returns the value of a specific item, allowing you to write the following:

```
Dim mData As New HashTable()

Return mData(index)
```

Default properties must be parameterized properties. A property without a parameter cannot be marked as the default. This is a change from previous versions of Visual Basic, in which any property could be marked as the default.

Our Person class has a parameterized property — the Phone property you built earlier. You can make this the default property by using the Default keyword:

```
Default Public Property Phone(ByVal location As String) As String
    Get
        Return CStr(mPhones.Item(location))
    End Get
    Set(ByVal Value As String)
        If mPhones.ContainsKey(location) Then
            mPhones.Item(location) = Value
        Else
            mPhones.Add(location, Value)
        End If
    End Set
End Property
```

Prior to this change, you would have needed code such as the following to use the Phone property:

```
Dim myPerson As New Person()

MyPerson.Phone("home") = "555-1234"

Now, with the property marked as Default, you can simplify the code:

myPerson("home") = "555-1234"
```

As you can see, the reference to the property name Phone is not needed. By picking appropriate default properties, you can potentially make the use of objects more intuitive.

# Events

Both methods and properties enable you to write code that interacts with your objects by invoking specific functionality as needed. It is often useful for objects to provide notification as certain activities occur during processing. You see examples of this all the time with controls, where a button indicates that it was clicked via a Click event, or a text box indicates that its contents have been changed via the TextChanged event.