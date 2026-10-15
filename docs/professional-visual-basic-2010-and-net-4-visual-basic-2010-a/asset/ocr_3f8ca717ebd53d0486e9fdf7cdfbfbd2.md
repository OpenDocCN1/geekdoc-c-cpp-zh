Or, to add or change a specific phone number, you’d write the following code:

```
myPerson.Phone("work") = "555-9876"
```

Not only are you retrieving and updating a phone number property, you are also updating a specific phone number. This implies a couple of things. First, you can no longer use a simple variable to hold the phone number, as you are now storing a list of numbers and their associated names. Second, you have effectively added a parameter to your property. You are actually passing the name of the phone number as a parameter on each property call.

To store the list of phone numbers, you can use the Hashtable class. The Hashtable is very similar to the standard VB Collection object, but it is more powerful — allowing you to test for the existence of a specific element. Add the following declaration to the Person class:

```
Public Class Person
    Public Property Name As String
    Public Property BirthDate As Date
    Public Property TotalDistance As Integer
    Public Property Phones As New Hashtable
```

You can implement the Phone property by adding the following code to the Person class:

```
Public Property Phone(ByVal location As String) As String
    Get
        Return CStr(Phones.Item(Location))
    End Get
    Set(ByVal Value As String)
        If Phones.ContainsKey(location) Then
            Phones.Item(location) = Value
        Else
            Phones.Add(location, Value)
        End If
    End Set
End Property
```

The declaration of the Property method itself is a bit different from what you have seen:

```
Public Property Phone(ByVal location As String) As String
```

In particular, you have added a parameter, location, to the property itself. This parameter will act as the index into the list of phone numbers, and must be provided when either setting or retrieving the phone number values.

Because the location parameter is declared at the Property level, it is available to all code within the property, including both the Get and Set blocks. Within your Get block, you use the location parameter to select the appropriate phone number to return from the Hashtable:

```
Get
    Return Phones.Item(location)
End Get
```

With this code, if no value is stored matching the location, then you get a trappable runtime error.

Similarly, in the Set block, you use the location to update or add the appropriate element in the Hashtable. In this case, you are using the ContainsKey method of Hashtable to determine whether the phone number already exists in the list. If it does, then you simply update the value in the list; otherwise, you add a new element to the list for the value:

```
Set(ByVal Value As String)
    If Phones.ContainsKey(location) Then
        Phones.Item(location) = Value
    Else
```