This simply adds a property to the class that indicates the global retirement age for all people. To use this value, you can simply access it directly from the class:

```
```vb
MessageBox.Show(Person.RetirementAge)
```
```

Alternately, you can access it from any Person object:

```
```vb
Dim myPerson As New Person()

MessageBox.Show(myPerson.RetirementAge)
```
```

Either way, you are invoking the same shared property.

# Shared Events

As with other interface elements, events can also be marked as Shared. For instance, you could declare a shared event in the Person class:

```
```vb
Public Shared Event NewPerson()
```
```

Shared events can be raised from both instance methods and shared methods. Regular events cannot be raised by shared methods. Because shared events can be raised by regular methods, you can raise this one from the constructors in the Person class:

```
```vb
Public Sub New()
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
    mCounter += 1
    RaiseEvent NewPerson()
End Sub

Public Sub New(ByVal name As String, ByVal birthDate As Date)
    mName = Name
    mBirthDate = BirthDate

    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
    mCounter += 1
    RaiseEvent NewPerson()
End Sub
```
```

![](bbox=[0.766, 0.599, 0.938, 0.638])

The interesting thing about receiving shared events is that you can get them from either an object, such as a normal event, or from the class itself. For instance, you can use the AddHandler method in the form’s code to catch this event directly from the Person class.

First, add a method to the form to handle the event:

```
```vb
Private Sub OnNewPerson()
    MessageBox.Show("new person " & Person.PersonCount)
End Sub
```
```

Then, in the form’s Load event, add a statement to link the event to this method:

```
```vb
Private Sub Form1_Load(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles MyBase.Load

    AddHandler Person.NewPerson, AddressOf OnNewPerson

    mPerson = New Person()
    If Microsoft.VisualBasic.Command = "nodisplay" Then
        AddHandler mPerson.Walked, AddressOf LogOnWalk
    Else
```
```