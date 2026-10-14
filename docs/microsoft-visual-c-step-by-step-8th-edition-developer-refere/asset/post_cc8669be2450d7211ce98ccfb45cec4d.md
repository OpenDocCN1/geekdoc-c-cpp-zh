
```
class Car : Vehicle
{
}
```

13. Add the Accelerate and Brake methods to the Car class, as shown in bold in the following:

Click here to view code image

```
class Car : Vehicle
{
    public void Accelerate()
    {
        Console.WriteLine("Accelerating");
    }

    public void Brake()
    {
        Console.WriteLine("Braking");
    }
}
```

14. Display the Vehicle.cs file in the Code and Text Editor window.

15. Add the virtual Drive method to the Vehicle class, as presented here in bold:

Click here to view code image

```
class Vehicle
{
    ...
    public virtual void Drive()
    {
        Console.WriteLine("Default implementation of the Drive method");
    }
}
```

16. Display the Program.cs file in the Code and Text Editor window.

17. In the doWork method, delete the // TODO: comment and add code to create an instance of the Airplane class and test its methods by simulating a quick journey by airplane, as follows:

Click here to view code image

```
static void doWork()
{
    Console.WriteLine("Journey by airplane:");
    Airplane myPlane = new Airplane();
    myPlane.StartEngine("Contact");
    myPlane.TakeOff();
    myPlane.Drive();
    myPlane.Land();
    myPlane.StopEngine("Whirr");
```

18. Add the statements that follow (shown in bold) to the doWork method after the code you just wrote. These statements create an instance of the Car class and test its methods.

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine("\nJourney by car:");
    Car myCar = new Car();
    myCar.StartEngine("Brm brm");
    myCar.Accelerate();
    myCar.Drive();
    myCar.Brake();
    myCar.StopEngine("Phut phut");
}
```

19. On the Debug menu, click Start Without Debugging.
In the console window, verify that the program outputs messages simulating the different stages of performing a journey by airplane and by car, as shown in the following image:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_334_0.png)

Notice that both modes of transport invoke the default implementation of the virtual Drive method because neither class currently overrides this method.

20. Press Enter to close the application and return to Visual Studio 2015.

21. Display the Airplane class in the Code and Text Editor window. Override the Drive method in the Airplane class, as follows in bold:

Click here to view code image

```
class Airplane : Vehicle
{
    ...
    public override void Drive()
    {
        Console.WriteLine("Flying");
    }
}
```

## Note

IntelliSense displays a list of available virtual methods. If you select the Drive method from the IntelliSense list, Visual Studio automatically inserts into your code a statement that calls the base.Drive method. If this happens, delete the statement, because this exercise does not require it.

22. Display the Car class in the Code and Text Editor window. Override the Drive method in the Car class, as shown in bold in the following:

Click here to view code image

```
class Car : Vehicle
{
    ...
    public override void Drive()
    {
        Console.WriteLine("Motoring");
    }
}
```

23. On the Debug menu, click Start Without Debugging.

In the console window, notice that the Airplane object now displays the message Flying when the application calls the Drive method, and the Car object displays the message Motoring:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_335_0.png)

24. Press Enter to close the application and return to Visual Studio 2015.

25. Display the Program.cs file in the Code and Text Editor window.

## 26. Add the statements shown here in bold to the end of the doWork method:

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine("\nTesting polymorphism");
    Vehicle v = myCar;
    v.Drive();
    v = myPlane;
    v.Drive();
}
```

This code tests the polymorphism provided by the virtual Drive method. The code creates a reference to the Car object by using a Vehicle variable (which is safe because all Car objects are Vehicle objects) and then calls the Drive method by using this Vehicle variable. The final two statements refer the Vehicle variable to the Airplane object and call what seems to be the same Drive method again.

## 27. On the Debug menu, click Start Without Debugging.

In the console window, verify that the same messages appear as before, followed by this text:

```
Testing polymorphism
Motoring
Flying
```

![](img/16f6e3fe08f01ddadb2741a92c392b0e_336_0.png)

The Drive method is virtual, so the runtime (not the compiler) works out which version of the Drive method to call when invoking it through a Vehicle variable, based on the real type of the object referenced by this variable. In the first case, the Vehicle object refers to a Car, so the application calls the Car.Drive method. In the second case, the Vehicle object refers to an Airplane, so the application calls the Airplane.Drive method.

28. Press Enter to close the application and return to Visual Studio 2015.

## Understanding extension methods

Inheritance is a powerful feature that makes it possible for you to extend the functionality of a class by creating a new class that derives from it. However, sometimes using inheritance is not the most appropriate mechanism for adding new behaviors, especially if you need to quickly extend a type without affecting existing code.

For example, suppose you want to add a new feature to the int type, such as a method named Negate that returns the negative equivalent value that an integer currently contains. (I know that you could simply use the unary minus operator [–] to perform the same task, but bear with me.) One way to achieve this is to define a new type named NegInt32 that inherits from System.Int32 (int is an alias for System.Int32) and adds the Negate method:

Click here to view code image

```
class NegInt32 : System.Int32  // don't try this!
{
    public int Negate()
    {
        ...
    }
}
```

The theory is that NegInt32 will inherit all the functionality associated with the System.Int32 type in addition to the Negate method. There are two reasons why you might not want to follow this approach:

- This method applies only to the NegInt32 type, and if you want to use it with existing int variables in your code, you have to change the definition of every int variable to the NegInt32 type.
- The System.Int32 type is actually a structure, not a class, and you cannot use inheritance with structures.

This is where extension methods become very useful.

Using an extension method, you can extend an existing type (a class or a structure) with additional static methods. These static methods become immediately available to your code in any statements that reference data of the type being extended.

You define an extension method in a static class and specify the type to which the method applies as the first parameter to the method, along with the this keyword. Here’s an example showing how you can implement the Negate extension method for the int type:

Click here to view code image

```
static class Util
{
    public static int Negate(this int i)
    {
        return -i;
    }
}
```

The syntax looks a little odd, but it is the this keyword prefixing the parameter to Negate that identifies it as an extension method, and the fact that the parameter that this prefixes is an int means that you are extending the int type.

To use the extension method, bring the Util class into scope. (If necessary, add a using statement that specifies the namespace to which the Util class belongs, or a using static statement that specifies the Util class directly.) Then you can simply use dot notation (.) to reference the method, like this:

Click here to view code image

```
int x = 591;
Console.WriteLine($"x.Negate {x.Negate()}");
```

Notice that you do not need to reference the Util class anywhere in the statement that calls the Negate method. The C# compiler automatically detects all extension methods for a given type from all the static classes that are in scope. You can also invoke the Util.Negate method by passing an int as the parameter, using the regular syntax you have seen before, although this use obviates the purpose of defining the method as an extension method:

Click here to view code image

```
int x = 591;
Console.WriteLine($"x.Negate {Util.Negate(x)}");
```

In the following exercise, you will add an extension method to the int type. With this extension method, you can convert the value in an int variable from base 10 to a representation of that value in a different number base.

## Create an extension method

- 1. In Visual Studio 2015, open the ExtensionMethod project, which is located in the \Microsoft Press\VCSBS\Chapter 12\ExtensionMethod folder in your Documents folder.
- 2. Display the Util.cs file in the Code and Text Editor window.
This file contains a static class named Util in a namespace named Extensions. Remember that you must define extension methods inside a static class. The class is empty apart from the // TODO: comment.
- 3. Delete the comment and declare a public static method in the Util class, named ConvertToBase. The method should take two parameters: an int parameter named i, prefixed with the this keyword to indicate that the
