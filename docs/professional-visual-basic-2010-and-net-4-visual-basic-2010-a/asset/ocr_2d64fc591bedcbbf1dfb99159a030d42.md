```
Private Sub OnNameChanged(ByVal newName As String)
    MsgBox("New name: " & newName)
End Sub
```

Note that you are not using the Handles clause here. In this case, for simplicity, you use the AddHandler method to dynamically link the event to this method. However, you could have also chosen to use the WithEvents and Handles keywords, as described in Chapter 2 — either way works.

With the handler built, you can use the AddHandler method to link this method to the event on the object:

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click

    Dim person As Employee = New OfficeEmployee("Mary")

    AddHandler person.NameChanged, AddressOf OnNameChanged
    With person
        .Name = "Fred"

```

Code snippet from Form1

Also note that you are uncommenting the line that changes the Name property. With this change, you know that the event should fire when the name is changed.

When you run the application now, you will see a message box, indicating that the name has changed and proving that the NameChanged event really is exposed and available, even though your object is of type OfficeEmployee, rather than Person.

# Raising Events from Subclasses

One caveat you should keep in mind is that while a subclass exposes the events of its base class, the code in the subclass cannot raise the event. In other words, you cannot use the RaiseEvent method in Employee or OfficeEmployee to raise the NameChanged event. Only code directly in the Person class can raise the event.

To see this in action, let’s add another event to the Person class, an event that can indicate the change of other arbitrary data values:

```
Public Class Person
    Private mName As String
    Private mBirthDate As String
    Private mID As String

    Public Event NameChanged(ByVal newName As String)
    Public Event DataChanged(ByVal field As String, ByVal newValue As Object)
```

You can then raise this event when the BirthDate is changed:

```
Public Overridable Property BirthDate() As Date
    Get
        Return mBirthDate
    End Get
    Set(ByVal value As Date)
        mBirthDate = value
        RaiseEvent DataChanged("BirthDate", value)
    End Set
End Property
```

Code snippet from Person