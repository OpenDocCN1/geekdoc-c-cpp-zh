
```csharp
    }
    public partial class Rectangle
    {
        public void Area()
        {
            Console.WriteLine("Area of the rectangle: " + length * width);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Rectangle rect = new Rectangle(20, 10);
            rect.Area();
            Console.ReadLine();
        }
    }
}
```

The first highlighted code snippet in Listing 2.3 defines a class, named **Rectangle**. The **Rectangle** class is divided into two partial classes. In the first partial class, we have declared two variables, **length** and **width**, for the **Rectangle** class and defined a constructor to initialize these variables. In the second partial class, we have defined a method, **Area()**, for the **Rectangle** class. The **Area()** method calculates and displays the area of the rectangle, represented by an object of the **Rectangle** class, on the screen. In the second highlighted code snippet, we have created an object, **rect**, of the **Rectangle** class and used that object to call the **Area()** method of the **Rectangle** class.

8. Press the **F5** key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-2.3:

![](img/9862a98a1a2d3bb14334137965a1ec60_329_0.png)

Fig.C#-2.3

## Static Classes

Static classes are used to define methods that can be accessed without creating an instance of the class. The **static** keyword is used to define a class and its members as static. You can use the class name to access the members of a static class. Some important features of a static class are as follows:

- It can contain only static members
- It cannot be instantiated
- It cannot have instance constructors, which are constructors that are used to create and initialize member variables of an instance
- It cannot be inherited

When you declare a static class, you must remember that static classes cannot be instantiated. Declaring a static class is similar to creating a class that contains only static members and a private constructor. Static methods cannot call non-static methods directly. To call a non-static method from a static method, you need to create an object of the class in which the non-static method is defined. Similarly, non-static methods cannot call static methods directly. To call a static method from a non-static method, you need to use the name of the class in which the static method is defined. A static member can exist inside a static or a non-static class.

Perform the following steps to create static classes:

1. *Start* Visual Studio 2010.

## Extension Methods

Extension methods, introduced in C# 2008, allow you to extend a class without deriving a new class from that class. The behavior of extension methods is similar to that of static methods and they are also defined with the static keyword. An extension method can be defined in a static class. The first parameter of an extension method is of the type that the extension method extends and it is preceded by the this keyword, as shown in the following code snippet:

```csharp
public static int MyExtensionMethod(this string number)
```

Perform the following steps to create extension methods:

1. *Start* Visual Studio 2010.
2. *Select* **File**→**New**→**Project** from the menu bar. The **New Project** dialog box opens.
3. *Select* **Visual C#**→**Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box. The project templates available for developing Windows applications in Visual C# are displayed in the right pane of the **New Project** dialog box.
4. *Select* **Console Application** from the right pane to create a Console application.
5. Enter the name of the application as **ExtensionMethods** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
6. Click the **OK** button to close the **New Project** dialog box and create the **ExtensionMethods** application.
7. *Add* the highlighted code snippets, shown in Listing 2.5, to the **Program.cs** file:

**Listing 2.5:** Creating Extension Methods

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ExtensionMethods
{
    public static class MyClass
    {
        public static int MyExtensionMethod(this string number)
        {
            return Int32.Parse(number);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            int num1 = 200, num2, result;
            string x = "300";
            num2 = x.MyExtensionMethod();
            result = num1 + num2;
            Console.WriteLine("Result = " + result);
            Console.ReadLine();
        }
    }
}
```

The first highlighted code snippet in Listing 2.5 shows the definition of a static class, MyClass. In the MyClass class, we have defined an extension method, MyExtensionMethod, which extends the string type. The MyExtensionMethod method takes a string type parameter, converts it into an equivalent integer value, and returns the integer value. You can notice that the this keyword is used before the parameter list of the MyExtensionMethod method.

In the second highlighted code snippet, we have declared three int type variables, num1, num2, and result, and assigned the value 200 to num1. After that, we have declared a string type variable, x, and assigned it the value 300. Next, we have called the extension method, MyExtensionMethod, by using the string variable, x. The MyExtensionMethod method converts the value stored in the x variable to an equivalent integer value and returns the resultant value. We have stored the value returned by the MyExtensionMethod method in the num2 variable. After that, we have added the values stored in the num1 and num2 variables and stored the resultant value in the result variable. Finally, we have displayed the value stored in the result variable on the screen.

8. Press the **F5** key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-2.5:

![](img/9862a98a1a2d3bb14334137965a1ec60_332_0.png)

Fig.C#-2.5

In this section, you have learned about classes and objects in C#. Let’s now discuss how to implement inheritance in C#.

## Implementing Inheritance

Inheritance is a principle of OOP that allows a class to inherit the features of some other class. In other words, inheritance is a mechanism of creating one class from another. The new class is known as the child class, derived class, or sub class, and the original class is known as the parent class, base class, or super class. A child class can have some or all the features of the parent class, apart from its own features.

Inheritance represents a relationship between two classes. Let’s understand the concept of inheritance through an example. Suppose, there are two classes, named A1 and A2, and class A2 inherits some features from class A1, as shown in Fig.C#-2.6:

![](img/9862a98a1a2d3bb14334137965a1ec60_332_1.png)

Fig.C#-2.6

In Fig.C#-2.6, class A1 represents the base class and class A2 represents the derived class. Derived class A2 is completely a new class that contains all the variables and methods of its base class and its own variables and methods. This implies that the derived class A2 can derive the content and behavior from its base class A1.

In this section, you learn to perform the following tasks related to inheritance:

- Define a derived class
- Access members of the base class
- Work with abstract classes
- Work with sealed classes

Let’s learn to perform each of these tasks, one by one.

### Defining a Derived Class

A derived class inherits all the members of its base class. The derived class has two effective types: the type of the new class and the type of the class from which it is derived.

The following code snippet shows how to derive a class from a base class:

```csharp
public class A1
{
```
