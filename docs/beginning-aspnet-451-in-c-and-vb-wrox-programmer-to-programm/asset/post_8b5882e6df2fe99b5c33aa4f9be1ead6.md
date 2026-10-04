
With this code, you can create a new Person object:

```VB.NET
Dim MyPerson As Person = New Person("Imar", "Spaanjaars", New DateTime(1971, 8, 9))

C#
Person myPerson = new Person("Imar", "Spaanjaars", new DateTime(1971, 8, 9));
```

The constructor accepts the values passed to it and assigns them to the private backing variables, so right after this line of code, the myPerson object is fully initialized.

You can have multiple constructors for the same class, as long as each one has a different method signature.

Visual Basic supports a slightly different syntax to declare and initialize an object in one sweep using the Dim myVariable As New Classname. The following code is equivalent to the previous instantiation of a Person instance:

```VB.NET
Dim MyPerson As New Person("Imar", "Spaanjaars", New DateTime(1971, 8, 9))
```

In addition, .NET offers another way to create an object and initialize a few properties: object initializers. With an initializer, you provide the initial values for the properties at the same time you create an instance of your object. The following code creates a Person object and assigns it a value for the FirstName and LastName properties:

```VB.NET
Dim MyPerson As New Person() With .FirstName = "Imar", .LastName = "Spaanjaars"

C#
Person myPerson = new Person() { FirstName = "Imar", LastName = "Spaanjaars" };
```

In .NET, you use the With keyword in front of the properties list. In addition, you need to prefix each property name with a dot. Other than that, the syntax is the same for both languages. Object initializers are great if you need to set a bunch of properties on an object quickly without being forced to write specialized versions of the constructor.

Although it is useful to use this Person class in your application, you might need specialized versions of Person. For example, your application may require classes like Employee and Student. What would you do in this? Create two copies of the Person class and name them Employee and Student, respectively.

Although this approach works well, it has a few drawbacks. The biggest problem is the duplication of code. If you decide to add a SocialSecurityNumber property, you would need to add it in multiple locations: in the general Person class and in the Employee and Student classes. Object inheritance, a major pillar of object orientation, is designed to solve problems of this.

## Inheritance

Earlier you learned that System.Object is the parent of all other data types in .NET, including the built-in types and types that you define, meaning that each type in .NET (except Object itself) inherits from Object. One of the benefits of inheritance is that you can define a behavior at a high level (for example in the Object class) that is available to inheriting classes automatically without the need to duplicate the code. .NET Framework, the Object class defines a few members that all other objects inherit, including the ToString() method.

To let one class inherit, you need to use the Inherits keyword in VB.NET and the colon (:) in C#, as shown in the following example that defines a Student class that inherits Person:

### VB.NET

```vb
Public Class Student
Inherits Person
```

### C#

```csharp
public class Student : Person
{
```

To see how inheritance works, think again the Person class shown in earlier examples. That class has few properties, such as FirstName and LastName, and a Save method. But if it is inheriting from Object, does it also have a ToString() method? You bet it. Figure 5-7 shows the relationship between the Object class and the Person class that inherits from Object.

![](img/9e033e3b9560597824f8b22941d6d8bb_224_0.png)
![](img/9e033e3b9560597824f8b22941d6d8bb_224_1.png)

FIGURE 5-7

Figure 5-7 shows that Person inherits from Object (indicated by the arrow pointing in the direction of the class that is inherited from), which means that a Person instance can do whatever an Object can do. If so, you can call ToString() on your person object:

```csharp
Label.Text = myPerson.ToString() // Writes out Person
```

The default behavior of the ToString() method defined in Object is to say its own name. In the preceding example, it means that Person class inherits this behavior and says Person as its name. Usually, this default behavior is not enough, and would be much better if the Person could return the full name of the person it is representing, for example. You can easily do this by overriding the ToString() method. Overriding a method or property redefines the class it inherits from its its parent class. To override a method use the keyword Overrides in VB.NET and in C#. The following snippet redefines the behavior of ToString in the Person class:

### VB.NET

```vb
Public Overrides Function ToString() As String
Return FullName & " , born at " & _dateOfBirth.ToShortString()
End Function
```

### C#

```csharp
public override string ToString()
{
return FullName + " , born at " + _dateOfBirth.ToShortDateString();
}
```

## CHAPTER 5 PROGRAMMING YOUR ASP.NET WEB PAGES

With this definition of ToString in the Person class, it no longer returns the word Person, but now returns the full name of the person it is representing:

```csharp
Label.Text = myPerson.ToString() ' Imar Spanjaars, born at 8/9/1971
```

Notice how the code uses the read-only FullName property to avoid coding the logic of concatenating the two names. You can't override any method you want to. For a method to be overrideable, the parent class needs to mark the method with the keyword virtual (in C#) or Override (in VB.NET).

Object inheritance in .NET enables you to create a hierarchy of objects that enhance, or add functionality to, other objects. You can start with a generic base class (object). Other classes can then inherit from this class, adding specialized behavior. If you need to, the inheritance allows you to reuse code and maintain consistency.

![](img/9e033e3b9560597824f8b22941d6d8bb_225_0.png)

Object inheritance in .NET enables you to create a hierarchy of objects that enhance, or add functionality to, other objects. You can start with a generic base class (object). Other classes can then inherit from this class, adding specialized behavior. If you need to, the inheritance allows you to reuse code and maintain consistency.

![](img/9e033e3b9560597824f8b22941d6d8bb_225_1.png)

Object inheritance in .NET enables you to create a hierarchy of objects that enhance, or add functionality to, other objects. You can start with a generic base class (object). Other classes can then inherit from this class, adding specialized behavior. If you need to, the inheritance allows you to reuse code and maintain consistency.

![](img/9e033e3b9560597824f8b22941d6d8bb_226_0.png)

Object inheritance in .NET enables you to create a hierarchy of objects that enhance, or add functionality to, other objects. You can start with a generic base class (object). Other classes can then inherit from this class, adding specialized behavior. If you need to, the inheritance allows you to reuse code and maintain consistency.
