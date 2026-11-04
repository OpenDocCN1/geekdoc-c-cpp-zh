# Working with Constructors and Destructors

Constructors are special methods used to instantiate a class or when an object is first created in an application. You can use a constructor to initialize objects and set any parameters. In addition, you can write constructors to accept arguments. The constructor is called by the same name as the class, while the name of the destructor is made up of the class name prefixed with a tilde symbol (~).

The syntax to define a constructor is as follows:

```
public class-name (parameter-list)
{
    //body
}
```

The main features of constructors are as follows:

+   - Have the same name as the class itself
+   - Do not have any return type
+   - It is not mandatory to declare a constructor; it is invoked automatically

A destructor (or finalizer) is called when an object is finally destroyed. Destructors are used to destruct the instances of classes when the instances are not required. A destructor is always invoked automatically, so you cannot call it in your application. C# provides a garbage collection mechanism that is executed when the runtime environment finds it necessary or when an object is not destroyed until its reference count drops to 0. You have no means to inform when an object will be destroyed and when the destructor will be called. However, implement a custom method that allows you to control object destruction by calling the destructor.

Let's perform the following steps to create an application named ConstructorApp to learn how to use constructors:

+   1. Repeat steps 1 to 3 of the Defining a Method section of this chapter.
+   2. Enter ConstructorApp in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The ConstructorApp application is created.
+   4. In the Program.cs file, add the highlighted code given in Listing 4.7:

# Listing 4.7: Defining a Constructor

```
class Program
{
    int length, breadth;
    public Program(int x, int y)
    {
        length = x;
        breadth = y;
    }
    public void area()
    {
        int result = length * breadth;
        Console.WriteLine("Area is: " + result);
    }
    static void Main(string[] args)
    {
        Program prg = new Program(10, 20);
        prg.area();
        Console.ReadLine();
    }
}
```