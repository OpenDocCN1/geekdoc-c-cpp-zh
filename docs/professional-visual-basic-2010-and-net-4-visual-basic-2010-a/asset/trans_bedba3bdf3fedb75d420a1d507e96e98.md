

With this change, you require the two parameter values to be supplied. Now add that second implementation, as shown here:

```
Public Sub New()
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

This second implementation accepts no parameters, meaning you can now create Person objects in two different ways — either with no parameters or by passing the name and birth date:

```
Dim myPerson As New Person()
```

or

```
Dim myPerson As New Person("Fred", "1/11/60")
```

This type of capability is very powerful because it enables you to define the various ways in which applications can create objects. In fact, the Visual Studio IDE considers this, so when you are typing the code to create an object, the IntelliSense tooltip displays the overloaded variations on the method, providing a level of automatic documentation for the class.

## Shared Methods, Variables, and Events

So far, all of the methods you have built or used have been instance methods, methods that require you to have an actual instance of the class before they can be called. These methods have used instance variables or member variables to do their work, which means that they have been working with a set of data that is unique to each individual object.

With Visual Basic, you can create variables and methods that belong to the class, rather than to any specific object. In other words, these variables and methods belong to all objects of a given class and are shared across all the instances of the class.

You can use the Shared keyword to indicate which variables and methods belong to the class, rather than to specific objects. For instance, you may be interested in knowing the total number of Person objects created as the application is running — kind of a statistical counter.

### Shared Variables

Because regular variables are unique to each individual Person object, they do not enable you to easily track the total number of Person objects ever created. However, if you had a variable that had a common value across all instances of the Person class, you could use that as a counter. Add the following variable declaration to the Person class:

```
Public Class Person
    Implements IDisposable
    Private Shared mCounter As Integer
```

By using the Shared keyword, you are indicating that this variable's value should be shared across all Person objects within your application. This means that if one Person object makes the value 42, then all other Person objects will see the value as 42: It is a shared piece of data.

You can now use this variable within the code. For instance, you can add code to the constructor method, New, to increment the variable so that it acts as a counter — adding 1 each time a new Person object is created. Change the New methods as shown here:

```
Public Sub New()
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
    mCounter += 1
End Sub
```

```
Public Sub New(ByVal name As String, ByVal birthDate As Date)
mName = name
mBirthDate = birthDate

Phone("home") = "555-1234"
Phone("work") = "555-5678"
mCounter += 1
End Sub
```

Code snippet from Person

The mCounter variable will now maintain a value indicating the total number of Person objects created during the life of the application. You may want to add a property routine to allow access to this value by writing the following code:

```
Public ReadOnly Property PersonCount() As Integer
    Get
        Return mCounter
    End Get
End Property
```

Code snippet from Form1

Note that you are creating a regular property that returns the value of a shared variable, which is perfectly acceptable. As shown shortly, you could also create a shared property to return the value.

Now you could write code to use the class as follows:

```
Dim myPerson As Person
myPerson = New Person()
myPerson = New Person()
myPerson = New Person()

Messagebox.Show(myPerson.PersonCount)
```

Code snippet from Form1

The resulting display would show 3, because you've created three instances of the Person class. You would also need to decrement the counter after the objects are destroyed.

### Shared Methods

You can share not only variables across all instances of a class, but also methods. Whereas a regular method or property belongs to each specific object, a shared method or property is common across all instances of the class. There are a couple of ramifications to this approach.

First, because shared methods do not belong to any specific object, they can't access any instance variables from any objects. The only variables available for use within a shared method are shared variables, parameters passed into the method, or variables declared locally within the method itself. If you attempt to access an instance variable within a shared method, you'll get a compiler error.

In addition, because shared methods are actually part of the class, rather than any object, you can write code to call them directly from the class without having to create an instance of the class first.

For instance, a regular instance method is invoked from an object:

```
Dim myPerson As New Person()

myPerson.Walk(42)
```

However, a shared method can be invoked directly from the class itself without having to declare an instance of the class first:

```
Person.SharedMethod()
```

This saves the effort of creating an object just to invoke a method, and can be very appropriate for methods that act on shared variables, or methods that act only on values passed in via parameters. You can also invoke a shared method from an object, just like a regular method. Shared methods are flexible in that they can be called with or without creating an instance of the class first.

To create a shared method, you again use the Shared keyword. For instance, the `PersonCount` property created earlier could easily be changed to become a shared method instead:

```
Public Shared ReadOnly Property PersonCount() As Integer
    Get
        Return mCounter
    End Get
End Property
```

> Code snippet from Form1

Because this property returns the value of a shared variable, it is perfectly acceptable for it to be implemented as a shared method. With this change, you can now determine how many Person objects have ever been created without having to actually create a Person object first:

```
MessageBox.Show(CStr(Person.PersonCount))
```

As another example, in the Person class you could create a method that compares the ages of two people. Add a shared method with the following code:

```
Public Shared Function CompareAge(ByVal person1 As Person, _
    ByVal person2 As Person) As Boolean

    Return person1.Age > person2.Age
End Function
```

> Code snippet from Form1

This method simply accepts two parameters — each a Person — and returns true if the first is older than the second. Use of the Shared keyword indicates that this method doesn’t require a specific instance of the Person class in order for you to use it.

Within this code, you are invoking the Age property on two separate objects, the objects passed as parameters to the method. It is important to recognize that you’re not directly using any instance variables within the method; rather, you are accepting two objects as parameters, and invoking methods on those objects. To use this method, you can call it directly from the class:

```
If Person.CompareAge(myPerson1, myPerson2) Then
```

Alternately, you can also invoke it from any Person object:

```
Dim myPerson As New Person()
```

```
If myPerson.CompareAge(myPerson, myPerson2) Then
```

Either way, you’re invoking the same shared method, and you’ll get the same behavior, whether you call it from the class or a specific instance of the class.

### Shared Properties

As with other types of methods, you can also have shared property methods. Properties follow the same rules as regular methods. They can interact with shared variables but not member variables. They can also invoke other shared methods or properties, but cannot invoke instance methods without first creating an instance of the class. You can add a shared property to the Person class with the following code:

```
Public Shared ReadOnly Property RetirementAge() As Integer
    Get
        Return 62
    End Get
End Property
```

> Code snippet from Person

