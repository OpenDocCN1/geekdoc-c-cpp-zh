
```
BirthDate = DateAdd(DateInterval.Year, -value, Now)
End Set
End Property
```

Code snippet from Person

With this change, the very nature of the Age method has changed. It is no longer a simple read-only property; now it is a read-write property that includes code to calculate an approximate birth date based on the age value supplied.

As it stands, your application will continue to run just fine because you are only using the read-only functionality of the property in your form. You can change the form to make use of the new read-write functionality:

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click

Dim person As Person = New Employee()

With person
    .Name = "Fred"
    .BirthDate = #1/1/1960#
    .Age = 20

    txtName.Text = .Name
    txtBirthDate.Text = Format(.BirthDate, "Short date")
    txtAge.Text = CStr(.Age)
End With
End Sub
```

However, this results in a syntax error. The variable you are working with, person, is of data type Person, and that data type doesn’t provide a writeable version of the Age property. In order to use your enhanced functionality, you must use a variable and object of type Employee:

```
Dim person As Employee = New Employee()
```

If you now run the application and click the button, the Age is displayed as 20, and the birth date is now a value calculated based on that age value, indicating that you are now running the shadowed version of the Age method as implemented in the Employee class.

As if that weren’t odd enough, you can do some even stranger and more dangerous things. You can change Age into a variable, and you can even change its scope. For instance, you can comment out the Age property code in the Employee class and replace it with the following code:

```
Private Shadows Age As String
```

At this point, you have changed everything. Age is now a String instead of an Integer. It is a variable instead of a property or function. It has Private scope instead of Public scope. Your Employee object is now totally incompatible with the Person data type, something that shouldn’t occur normally when using inheritance.

This means that the code you wrote in Form1 will no longer work. The Age property is no longer accessible and can no longer be used, so your project will no longer compile. This directly illustrates the danger in shadowing a base-class element such that its very nature or scope is changed by the subclass.

Because this change prevents your application from compiling, remove the line in the Employee class that shadows Age as a String variable, and uncomment the shadowed Property routine:

```
Public Shadows Property Age() As Integer
    Get
        Return CInt(DateDiff(DateInterval.Year, BirthDate, Now))
    End Get
```

```
Set(ByVal value As Integer)
    BirthDate = DateAdd(DateInterval.Year, -value, Now)
End Set
End Property
```

Code snippet from Person

This restores your application to a working state.

## Levels of Inheritance

So far, you have created a single base class and a single subclass, thus demonstrating that you can implement inheritance that is a single level deep. You can also create inheritance relationships that are several levels deep. These are sometimes referred to as chains of inheritance.

## Multiple Inheritance

Don't confuse multilevel inheritance with multiple inheritance, which is an entirely different concept that is not supported by either Visual Basic or the .NET platform itself. The idea behind multiple inheritance is that you can have a single subclass that inherits from two base classes at the same time.

For instance, an application might have a class for Customer and another class for Vendor. It is quite possible that some customers are also vendors, so you might want to combine the functionality of these two classes into a CustomerVendor class. This new class would be a combination of both Customer and Vendor, so it would be nice to inherit from both of them at once.

While this is a useful concept, multiple inheritance is complex and somewhat dangerous. Numerous problems are associated with multiple inheritance, but the most obvious is the possibility of collisions of properties or methods from the base classes. Suppose that both Customer and Vendor have a Name property. CustomerVendor would need two Name properties, one for each base class. Yet it only makes sense to have one Name property on CustomerVendor, so to which base class does it link, and how will the system operate if it does not link to the other one?

These are complex issues with no easy answers. Within the object-oriented community, there is ongoing debate as to whether the advantages of code reuse outweigh the complexity that comes along for the ride.

Multiple inheritance isn't supported by the .NET Framework, so it is likewise not supported by Visual Basic, but you can use multiple interfaces to achieve an effect similar to multiple inheritance, a topic discussed later in the chapter when we talk about implementing multiple interfaces.

## Multilevel Inheritance

You have seen how a subclass derives from a base class with the Person and Employee classes, but nothing prevents the Employee subclass from being the base class for yet another class, a sub-subclass, so to speak. This is not at all uncommon. In the working example, you may have different kinds of employees, some who work in the office and others who travel.

To accommodate this, you may want OfficeEmployee and TravelingEmployee classes. Of course, these are both examples of an employee and should share the functionality already present in the Employee class. The Employee class already reuses the functionality from the Person class. Figure 3-9 illustrates how these classes are interrelated.

The Employee is a subclass of Person, and your two new classes are both subclasses of Employee. While both OfficeEmployee and TravelingEmployee are employees, and thus also people, they are each unique. An OfficeEmployee almost certainly has a cube or office number, while a TravelingEmployee will keep track of the number of miles traveled.

![](img/d99870e80390742f93963da7be0b2e61_178_0.png)

## FIGURE 3-9

Add a new class to your project and name it OfficeEmployee. To make this class inherit from your existing Employee class, add the following code to the class:

```
Public Class OfficeEmployee
    Inherits Employee
End Class
```

With this change, the new class now has Name, BirthDate, Age, HireDate, and Salary methods. Notice that methods from both Employee and Person are inherited. A subclass always gains all the methods, properties, and events of its base class.

You can now extend the interface and behavior of OfficeEmployee by adding a property to indicate which cube or office number the employee occupies:

```
Public Class OfficeEmployee
    Inherits Employee

    Private mOffice As String

    Public Property OfficeNumber() As String
        Get
            Return mOffice
        End Get
        Set(ByVal value As String)
            mOffice = value
        End Set
    End Property
End Class
```

To see how this works, let’s enhance the form to display this value. Add a new TextBox control named txtOffice and an associated label so that your form looks like the one shown in Figure 3-10.

Now change the code behind the button to use the new property:

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click

    Dim person As OfficeEmployee = New OfficeEmployee()

    With person
        .Name = "Fred"
        .BirthDate = #1/1/1960#
        .Age = 20

        .OfficeNumber = "A42"

        txtName.Text = .Name
        txtBirthDate.Text = Format(.BirthDate, "Short date")
        txtAge.Text = CStr(.Age)

        txtOffice.Text = .OfficeNumber
    End With
End Sub
```

![](img/d99870e80390742f93963da7be0b2e61_179_0.png)

FIGURE 3-10

Code snippet from Form1

You have changed the routine to declare and create an object of type OfficeEmployee — thus enabling you to make use of the new property, as well as all existing properties and methods from Employee and Person, as they’ve been “merged” into the OfficeEmployee class via inheritance. If you now run the application, the name, birth date, age, and office values are displayed in the form.

Inheritance like this can go many levels deep, with each level extending and changing the behaviors of the previous levels. In fact, there is no specific technical limit to the number of levels of inheritance you can implement in Visual Basic, although very deep inheritance chains are typically not recommended and are often viewed as a design flaw, something discussed in more detail later in this chapter.

## Interacting with the Base Class, Your Class, and Your Object

You have already seen how you can use the MyBase keyword to call methods on the base class from within a subclass. The MyBase keyword is one of three special keywords that enable you to interact with important object and class representations:

- Me
- MyBase
- MyClass

## The Me Keyword

The Me keyword provides you with a reference to your current object instance. Typically, you do not need to use the Me keyword, because whenever you want to invoke a method within your current object, you can just call that method directly.

To see clearly how this works, let’s add a new method to the Person class that returns the data of the Person class in the form of a String. This is interesting in and of itself, as the base System.Object class defines the ToString method for this exact purpose. Remember that all classes in the .NET Framework ultimately derive from System.Object, even if you do not explicitly indicate it with an Inherits statement.
