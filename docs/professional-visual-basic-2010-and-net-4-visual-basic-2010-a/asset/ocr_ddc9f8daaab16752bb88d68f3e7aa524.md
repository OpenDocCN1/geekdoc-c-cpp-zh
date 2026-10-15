interface, but also overrides the implementation for the interface. For instance, you could declare the Value method in the interface as follows:

```
Public Overridable Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value, IValues.GetValue
```

Now it is Public, so it is available on your native interface, and it is part of both the IPrintableObject and IValues interfaces. This means that you can access the property three ways in client code:

```
Dim emp As New Employee()
Dim printable As IPrintableObject = emp
Dim values As IValues = emp

Debug.WriteLine(emp.Value(0))
Debug.WriteLine(printable.Value(0))
Debug.WriteLine(values.GetValue(0))
```

Note that you are also now using the Overrides keyword in the declaration. This means that a subclass of Employee, such as OfficeEmployee, can override the Value method. The overridden method will be the one invoked, regardless of whether you call the object directly or via an interface.

Combining the implementation of an interface in a base class with overridable methods can provide a very flexible object design.

# ABSTRACTION

Abstraction is the process by which you can think about specific properties or behaviors without thinking about a particular object that has those properties or behaviors. Abstraction is merely the ability of a language to create “black box” code, to take a concept and create an abstract representation of that concept within a program.

A Customer object, for example, is an abstract representation of a real-world customer. A DataSet object is an abstract representation of a set of data.

Abstraction enables you to recognize how things are similar and to ignore differences, to think in general terms and not in specifics. A TextBox control is an abstraction because you can place it on a form and then tailor it to your needs by setting properties. Visual Basic enables you to define abstractions using classes.

Any language that enables a developer to create a class from which objects can be instantiated meets this criterion, and Visual Basic is no exception. You can easily create a class to represent a customer, essentially providing an abstraction. You can then create instances of that class, whereby each object can have its own attributes, representing a specific customer.

In Visual Basic, you implement abstraction by creating a class using the Class keyword. To see this in action, bring up Visual Studio and create a new Visual Basic Windows Forms Application project named “OOExample.” Once the project is open, add a new class to the project using the Project ⇨ Add Class menu option. Name the new class Customer.vb, and add some code to make this class represent a real-world customer in an abstract sense:

```
Public Class Customer
    Private mID As Guid = Guid.NewGuid
    Private mName As String
    Private mPhone As String

    Public Property ID() As Guid
        Get
            Return mID
        End Get
```