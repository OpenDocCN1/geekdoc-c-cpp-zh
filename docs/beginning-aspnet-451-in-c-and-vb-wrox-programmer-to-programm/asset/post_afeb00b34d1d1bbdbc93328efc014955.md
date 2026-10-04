
## CHAPTER 5 PROGRAMMING YOUR ASP.NET WEB PAGES

The cool thing about this type of commenting is that the comments you show up in IntelliSense in the code editor when you try to call the method (see Figure 5-6).

It makes much easier for you and other developers to understand the purpose of the method and its parameters.

In addition aiding development in the code editor, you can use the XML comments to create good-looking, MSDN-like documentation. A number of third-party tools are available that help you with this, including Microsoft's own Sandcastle (http://msdn.microsoft.com/en-us/vstudio/bb608422.aspx) and Document X from Innovas (www.innovas.com/).

```
/// SendMessage()
public void Calculator.SendMessage(string emailAddress, string mailBody)
Sends out an e-mail to the address specified by emailAddress.
/// emailAddress: The e-mail address of the recipient.
```

FIGURE 5-6

## OBJECT ORIENTATION BASICS

A chapter about writing in ASP.NET would not be complete without a section on object orientation (OO). Object orientation, or object-oriented programming, is a highly popular style of programming where the software is modeled as a set of objects interacting with each other. Object orientation is at the heart of the .NET Framework. Literally everything inside the framework is an object, from simple things to complex things like a DropDownList, connection to the database, or a data-driven control.

Because object orientation is such an important aspect of .NET, it's important to be familiar with the general concepts of object-oriented programming. At the same time, you don't have to be an expert on OO to be able to build websites with ASP.NET. This gives you a 10,000-foot overview of the most important terms and concepts. This helps you get started building useful applications in the next chapter instead of keeping your nose in the books for the next three weeks.

### Important OO Terminology

In object orientation, everything revolves around the concept of objects. In OO everything is, in fact, an object. But what is exactly an object? And what classes do we have to do with them?

### Objects

Objects are the basic building blocks of object-oriented programming languages. Just like in the real world, an object in OO-land is a thing, stored in the computer's memory. It can be an integer holding someone's age or an open database connection to a SQL Server located on the other side of the world, but it can also be more conceptual, like a web page. In your applications, you create a new object with the New (new in C#) keyword, as you saw with the calculator example. This process of creating new objects is called instantiating and the objects you create are called instances. You can instantiate object or custom types like Calculator, as well simple types like Integers and Strings:

### VB.NET

Dim myCalculator As Calculator = New Calculator ()

Dim age As Integer = New Integer ()

### C#

```
Calculator myCalculator = new Calculator ();
```

```
int age = new int();
```

Because it's common to create variables of simple types like Integer (int in C#) and String (string in C#), the compiler allows you to leave out the new keyword and the assignment. Therefore, the following code is functionally equivalent to the preceding age declaration:

### VB.NET

Dim age As Integer

### C#

```
int age;
```

All data types listed at the beginning of this chapter except System.Object can be created without the New keyword.

Once you have created an instance of an object, such as the myCalculator object, it's ready to be used. For example, you can access its methods and properties to do something useful with the object. But before you look at methods and properties, you need to understand classes.

### Classes

Classes are the blueprints of objects. Just as you can use a single blueprint to build a bunch of similar houses, you can use a single class to create multiple instances of that class. The class acts as the definition of the objects that you use in your application. At its most basic form, a class looks like this:

### VB.NET

```
Public Class ClassName

End Class
```

### C#

```
public class ClassName
{}
```

Because this code simply defines an empty class, it cannot do anything useful. To give the class some behavior, you can give it fields, properties, methods, constructors. In addition, you can let the class inherit from an existing class to give it a head start in terms of functionality and behavior. You'll come to understand these terms in the next couple of sections.

### Fields

Fields are simple variables declared at the class level that can contain data. They are often used as backing variables for properties (as you'll see in the next section), but that doesn't have to be the case. Here's a quick example of a field in a Person class:

```
VB.NET
Public Class Person
    Private _firstName As String
End Class

C#
public class Person
{
    private string _firstName;
}
```

Fields are often marked as Private (private in C#), which makes them visible only in the class that defines them. If you have the need to expose fields to other classes as well, you could use properties, which are discussed next. Later in the chapter you learn more about the Private keyword and other access modifiers.

### Properties

Properties of an object are the characteristics the object has. Consider a Person object. What kind of properties does a Person have? It's easy to come up with many different characteristics, but the most common are:

- First name
- Last name
- Date of birth

You define a property in a class with the Property keyword (in VB.NET) or with a property header similar to a method in C#. In both languages, you use a Get block (get in C#) and a Set block (set in C#) to define the so-called getters and setters of the property. The getter is accessed when an object is asked for the value of a specific property, and the setter is used to assign a value to the property. Properties only provide access to data stored in the object; they don't contain the actual data. To store data, you often use what is called a backing variable. This is often a simple field defined in the class that is able to store the value for the external property. In the following example, the variable _firstName is the backing variable for the Firstname property:

```
VB.NET
Public Class Person
    Private _firstName As String
    Public Property FirstName()
    Get
        Return _firstName
    End Get
    Set(value As String)
        _firstName = value
    End Set
End Property
End Class

C#
public class Person
{
    private string _firstName;
    public string FirstName
    {
        get { return _firstName; }
        set { _firstName = value; }
    }
}
```

It is common to prefix the private backing variables with an underscore, followed by the first word in all lowercase, optionally followed by words that start with a capital letter. So the FirstName property has a backing variable called _firstName, LastName has one called _lastName, and so on. This, all variables that apply to the entire class are nicely picked together in the IntelliSense list. Simply type an underscore and you'll get the full list of private variables. Note that the underscore is typically not used when defining variables inside a function or subroutine.

Just like the keyword you saw earlier, Private is also an access modifier. You learn more about access modifiers later in this chapter.

The main reason for a property in a class is to encapsulate data. The idea is that a property enables you to control the data that is being assigned to. This, you can perform validation or manipulation of the data before it's stored in the underlying backing variable. Imagine that one of the business rules of your application sets that all names must be written with the first letter as a capital. In non-object oriented languages, the developer setting the name would have to keep this rule in every time a variable was filled with a first name. In an OO approach, you can make the FirstName property responsible for this so others don't have to worry about anyone. You can do this type of data manipulation in the setter of the property:

```
VB.NET
Set(value As String)
If Not String.IsNullOrEmpty(value) Then
    _firstName = value.Substring(0, 1).ToUpper() & value.Substring(1)
Else
    _firstName = String.Empty
End If
```

```
C#
set
{
    if (!String.IsNullOrEmpty(value))
    {
        _firstName = value.Substring(0, 1).ToUpper() + value.Substring(1);
    }
}
```
