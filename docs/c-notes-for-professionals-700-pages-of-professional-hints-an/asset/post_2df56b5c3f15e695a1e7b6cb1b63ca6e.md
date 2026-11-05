
## Chapter 133: Structural Design Patterns

Structural design patterns are patterns that describe how objects and classes can be combined and form a large structure and that ease design by identifying a simple way to realize relationships between entities. There are seven structural patterns described. They are as follows: Adapter, Bridge, Composite, Decorator, Facade, Flyweight and Proxy

### Section 133.1: Adapter Design Pattern

"Adapter" as the name suggests is the object which lets two mutually incompatible interfaces communicate with each other.

**For example:** if you buy a iPhone 8 (or any other Apple product) you need a lot of adapters. Because the default interface does not support audio jack or USB. With these adapters you can use earphones with wires or you can use a normal Ethernet cable. So "two mutually incompatible interfaces communicate with each other".

**So in technical terms this means:** Convert the interface of a class into another interface that a client expects. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces. The classes and objects participating in this pattern are:

### The adapter pattern consists of 4 elements

- 1. **ITarget:** This is the interface which is used by the client to achieve functionality.
- 2. **Adaptee:** This is the functionality which the client desires but its interface is not compatible with the client.
- 3. **Client:** This is the class which wants to achieve some functionality by using the adaptee's code.
- 4. **Adapter:** This is the class which would implement ITarget and would call the Adaptee code which the client wants to call.

### UML

![](img/5da9b5c72747b887ec63f57c832400bf_681_0.png)

### First code Example (Theoretical example).

```
public interface ITarget
{
    void MethodA();
}

public class Adaptee
{
    public void MethodB()
    {
        Console.WriteLine("MethodB() is called");
    }
}

public class Client
{
    private ITarget target;

    public Client(ITarget target)
    {
        this.target = target;
    }

    public void MakeRequest()
    {
        target.MethodA();
    }
}

public class Adapter : Adaptee, ITarget
{
    public void MethodA()
    {
        MethodB();
    }
}
```

### Second code example (Real world implementation)

```
/// <summary>
/// Interface: This is the interface which is used by the client to achieve functionality.
/// </summary>
public interface ITarget
{
    List<string> GetEmployeeList();
}

/// <summary>
/// Adaptee: This is the functionality which the client desires but its interface is not compatible
with the client.
/// </summary>
public class CompanyEmployees
{
    public string[][] GetEmployees()
    {
        string[][] employees = new string[4][];

        employees[0] = new string[] { "100", "Deepak", "Team Leader" };
        employees[1] = new string[] { "101", "Rohit", "Developer" };
        employees[2] = new string[] { "102", "Gautam", "Developer" };
        employees[3] = new string[] { "103", "Dev", "Tester" };

return employees;
    }
}

/// <summary>
/// Client: This is the class which wants to achieve some functionality by using the adaptee's code (list of employees).
/// </summary>
public class ThirdPartyBillingSystem
{
    /*
     * This class is from a third party and you don't have any control over it.
     * But it requires a Employee list to do its work
     */

    private ITarget employeeSource;

    public ThirdPartyBillingSystem(ITarget employeeSource)
    {
        this.employeeSource = employeeSource;
    }

    public void ShowEmployeeList()
    {
        // call the client list in the interface
        List<string> employee = employeeSource.GetEmployeeList();
        Console.WriteLine("######## Employee List ########");
        foreach (var item in employee)
        {
            Console.Write(item);
        }
    }
}

/// <summary>
/// Adapter: This is the class which would implement ITarget and would call the Adaptee code which the client wants to call.
/// </summary>
public class EmployeeAdapter : CompanyEmployees, ITarget
{
    public List<string> GetEmployeeList()
    {
        List<string> employeeList = new List<string>();
        string[][] employees = GetEmployees();
        foreach (string[] employee in employees)
        {
            employeeList.Add(employee[0]);
            employeeList.Add(",");
            employeeList.Add(employee[1]);
            employeeList.Add(",");
            employeeList.Add(employee[2]);
            employeeList.Add("\n");
        }

        return employeeList;
    }
}

/// 
/// Demo
///
class Programs
{
    static void Main(string[] args)
    {
        ITarget Itarget = new EmployeeAdapter();
        ThirdPartyBillingSystem client = new ThirdPartyBillingSystem(Itarget);
        client.ShowEmployeeList();
        Console.ReadKey();
    }
}
```

### When to use

- Allow a system to use classes of another system that is incompatible with it.
- Allow communication between new and already existing system which are independent of each other
- Ado.Net SqlAdapter, OracleAdapter, MySqlAdapter are best examples of Adapter Pattern.

## Chapter 134: Creational Design Patterns

### Section 134.1: Singleton Pattern

The Singleton pattern is designed to restrict creation of a class to exactly one single instance.

This pattern is used in a scenario where it makes sense to have only one of something, such as:

- a single class that orchestrates other objects' interactions, ex. Manager class
- or one class that represents a unique, single resource, ex. Logging component

One of the most common ways to implement the Singleton pattern is via a static factory method such as a CreateInstance() or GetInstance() (or a static property in C#, Instance), which is then designed to always return the same instance.

The first call to the method or property creates and returns the Singleton instance. Thereafter, the method always returns the same instance. This way, there is only ever one instance of the singleton object.

Preventing creation of instances via new can be accomplished by making the class constructor(s) private.

Here is a typical code example for implementing a Singleton pattern in C#:

```csharp
class Singleton
{
    // Because the _instance member is made private, the only way to get the single
    // instance is via the static Instance property below. This can also be similarly
    // achieved with a GetInstance() method instead of the property.
    private static Singleton _instance = null;

    // Making the constructor private prevents other instances from being
    // created via something like Singleton s = new Singleton(), protecting
    // against unintentional misuse.
    private Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            // The first call will create the one and only instance.
            if (_instance == null)
            {
                _instance = new Singleton();
            }

            // Every call afterwards will return the single instance created above.
            return _instance;
        }
    }
}
```

To illustrate this pattern further, the code below checks whether an identical instance of the Singleton is returned when the Instance property is called more than once.

```csharp
class Program
{
static void Main(string[] args)
{
    Singleton s1 = Singleton.Instance;
    Singleton s2 = Singleton.Instance;

    // Both Singleton objects above should now reference the same Singleton instance.
    if (Object.ReferenceEquals(s1, s2))
    {
        Console.WriteLine("Singleton is working");
    }
    else
    {
        // Otherwise, the Singleton Instance property is returning something
        // other than the unique, single instance when called.
        Console.WriteLine("Singleton is broken");
    }
}
```
```

Note: this implementation is not thread safe.

To see more examples, including how to make this thread-safe, visit: Singleton Implementation

Singletons are conceptually similar to a global value, and cause similar design flaws and concerns. Because of this, the Singleton pattern is widely regarded as an anti-pattern.

Visit "What is so bad about Singletons?" for more information on the problems that arise with their use.

In C#, you have the ability to make a class static, which makes all members static, and the class cannot be instantiated. Given this, it is common to see static classes used in place of the Singleton pattern.

For key differences between the two, visit C# Singleton Pattern Versus Static Class.

### Section 134.2: Factory Method pattern

Factory Method is one of the creational design patterns. It is used to deal with the problem of creating objects without specifying exact result type. This document will teach you how to use Factory Method DP properly.

Let me explain the idea of it to you on a simple example. Imagine you're working in a factory that produces three types of devices - Ammeter, Voltmeter and resistance meter. You are writing a program for a central computer that will create selected device, but you don't know final decision of your boss on what to produce.

Let's create an interface IDevice with some common functions that all devices have:

```
public interface IDevice
{
    int Measure();
    void TurnOff();
    void TurnOn();
}
```

Now, we can create classes that represent our devices. Those classes must implement IDevice interface:

```
public class AmMeter : IDevice
{
    private Random r = null;
    public AmMeter()
    {
```
