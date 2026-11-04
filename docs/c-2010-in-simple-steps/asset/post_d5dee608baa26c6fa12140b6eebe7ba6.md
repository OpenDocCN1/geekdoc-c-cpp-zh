
In this section, you learned about the garbage collection mechanism and how you can enforce garbage collection for any unused resources in your application. Now, let's learn about the IDisposable interface in the next section.

## The IDisposable Interface

Garbage collection in .NET applications is non-deterministic in nature. This means that one cannot predict when garbage collection will be performed by the GC. Therefore, the need to explicitly enforce garbage collection arises for applications that have significant memory requirements. In such cases, it is recommended to implement the IDisposable interface. This interface defines a method to free allocated unmanaged resources because the GC does not possess any knowledge about unmanaged resources, such as open files and streams. The IDisposable interface defines the Dispose() method that is responsible for the release of managed as well as unmanaged resources. The Dispose() method is used in conjunction with the GC.

> **Note**
> *When you implement the IDisposable interface, use the try ... catch ... finally block to ensure that the unmanaged resources are released despite the occurrence of any exception. An unmanaged resource is anything that is not included within the .NET Framework, such as the operating system resources, which include a text file or a window. Network or database connections are also examples of unmanaged resources.*

Next, let's learn about the methods used to release any resources owned by an object of a .NET application.

## The Dispose and Close Methods

The Dispose() method is defined inside the IDisposable interface and is used to release any unmanaged resources. This is the preferred method to release resources that are assigned to an object or to prepare the object for reuse. Let's consider the Listing 4.10, which defines the Dispose() method:

### Listing 4.10: Defining the Dispose() method

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ReleasingObject
{
    class Program : IDisposable
    // class Program implements the IDisposable interface
    {
        // calling the Dispose() method
        public void Dispose()
        {
            // some code
            Console.WriteLine("Outside the Dispose() method!");
        }
    }
}
```

In Listing 4.10, the IDisposable interface is implemented by the Program class, which contains the Dispose() method. You can add code to perform any clean-up operations inside the Dispose() method.

In .NET Framework, there is another method to release resources, which is known as the Close() method. The Close() method is executed to temporarily close any managed resource, such as a database connection. This implies that a particular resource for which you have called the Close() method can be reopened. However, the Dispose() method removes an unmanaged resource permanently from the memory and that resource is not available for any further processing.

## Working with Partial Classes

A partial class in C# is the class that enables you to specify the definition of a class in two or more source files. All the source files contain a section of the class definition. The definitions in the different source files are combined when the application is executed. You can distribute a partial class over multiple separate files, so that you can work on the separate files simultaneously by using one partial class.

You can declare a partial class by using the partial keyword. The partial keyword indicates that all the parts of the class must be available at compile time to generate the final type.

Let's perform the following steps to create an application named PartialClass to learn how to use a partial class:

- 1. Repeat the steps 1 to 3 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
- 2. Enter PartialClass in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box
- 3. Click the OK button. The PartialClass application is created.
- 4. In the Program.cs file, add the highlighted code given in Listing 4.11:

### Listing 4.11: Using a Partial Class

```csharp
namespace PartialClass
{
    public partial class Orders
    {
        private int x;
        private int y;
        public Orders(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }
    public partial class Orders
    {
        public void PrintOrders()
        {
            Console.WriteLine("Orders: {0}, {1}", x, y);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Orders ord = new Orders(20, 60);
            ord.PrintOrders();
            Console.ReadLine();
        }
    }
}
```

In Listing 4.11, the fields and constructors of the Orders class are declared in one partial class definition, and the PrintOrders() method is declared in another partial class definition.

- 5. Press the F5 key to run the PartialClass application.

The output of the application appears, as shown in Fig.C4-4.9:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_119_0.png)

### Fig.C4-4.9

Fig.C4-4.9 shows that all partial classes are compiled as a single class and then executed. In the next section, you learn about static classes.

## Working with Static Classes

A static class in C# is the same as a non-static class; however, unlike a non-static class, it cannot be instantiated. In other words, it means that when you declare a class as static, then you cannot use the new keyword to create an object of that class. Static classes in C# can be used to create data members and functions, which are accessible even if you do not create any objects of the class. You can access the members of a static class by using the class name itself. The static keyword is used to define a class and its members as static.

A static class does not contain instance constructors, which are used to create and initialize instances. The features of a static class are as follows:

- A static class can contain only static members
- A static class cannot be instantiated
- Static classes are sealed
- You cannot inherit static classes

Let’s now learn how to declare a static class and use a static method in a class.

## Declaring a Static Class

When you declare a static class in your C# application, you must consider the basic rule that static classes cannot be instantiated. Declaring a static class is similar to creating a class that contains only static members and a private constructor. The following code snippet shows how to declare a static class:

```csharp
static class Employee
{
    public static int id;
    public static int tele_no;
}
```

In the preceding code snippet, Employee is the static class, and id and tele_no are its static data members. If a class is static, its members are also static.

## Using a Static Method in a Class

You can call a static method within a class, in which the static method is declared, without creating the instance of the class. If you create an instance of the class, you cannot use it to call static members. A static member can exist inside a static or a non-static class.

Let’s perform the following steps to create an application named StaticMethod to learn how to use a static method in a class:

- 1. Repeat the steps 1 to 3 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
- 2. Enter StaticMethod in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
- 3. Click the OK button. The StaticMethod application is created.
- 4. In the Program.cs file, add the highlighted code given in Listing 4.12:

### Listing 4.12: Showing the Code to Add a Static Method in a Class

```csharp
namespace StaticMethod
{
    static class MathFunction
    {
        static public double square(double num)
        {
```
