
When you analyze these tables, you can retrieve an assembly’s attributes and types.

## Uses for Reflection in C#

There are a whole lot of uses of reflection in C#, as we have mentioned here:

- Use Module to acquire all global and non-global methods defined in the module.
- Use MethodInfo to look at parameters, name, return type, access modifiers, and implementation details.
- Use EventInfo to figure out the event-handler data type, the name, declaring type, and custom attributes.
- Use PropertyInfo to get the declaring type, reflected type, data type, name, and writable status of a property, or to get and set property values.
- Use CustomAttributeData to figure out information on custom attributes or to review attributes without creating more instances.
- Other uses for reflection include constructing symbol tables to determine which fields to persist, and through serialization.
- Use ConstructorInfo to get data on the parameters, access modifiers, and implementation details of a constructor.
- Use Assembly to load modules listed in the assembly manifest.

The code will compile, but we will get an exception when we run the application:

RuntimeBinderException is the exception you will see the most when you work with dynamic types. As the exception message states, we cannot use the `++` operator on a variable of type string. So that means that the dynamic type behaves like the last type we’ve assigned to it.

One more example to wrap it up. We have a class that provides us with an instance of some logger implementation:

```csharp
public class Logger
{
    public void LogInfo(string message)
    {
        Console.WriteLine($"INFO: {message}");
    }

    public void LogWarning(string message)
    {
        Console.WriteLine($"WARNING: {message}");
    }

    public void LogError(string message)
    {
        Console.WriteLine($"ERROR: {message}");
    }
}

public class LoggerFactory
{
    public static Logger GetLogger()
    {
        return new Logger();
    }
}
```

```csharp
dynamic logger = LoggerFactory.GetLogger();
logger.LogInfo("Hi");
logger.LogWarning("You are going to enter a time warp");
logger.LogError("System is malfunctioning");
logger.LogTrace("Communication lost");
```

When we consider the compiler, everything is comfortable.⁴ But once more, we get the RuntimeBinderException because the LogTrace method is not defined.

## Short Overview of DLR

DLR, or Dynamic Language Runtime, makes the dynamic type easy to use in C#, a statically typed language. DLR attaches a set of services to the CLR that do dynamic work.

As we can see, the services DLR added to the already existing functionalities of CLR include Call Site Caching, Expression Trees, and Dynamic Object Interoperability.

### Call Site Caching

DLR provides a way to cache previously called operations to achieve maximum efficiency in operation execution. A dynamic call site is where you may use the `a.b()` and `a+b` operations on dynamic objects. DLR caches the types of objects used while executing these operations and stores them in a cache. If a similar operation is performed once more, DLR can retrieve the information from that cache.

### Expression Trees

Expression trees constitute code in a tree-like data structure, where each node is an expression, for example, a method call or a binary operation. DLR has extended LINQ expression trees with assignment, control flow, and other language-modeling nodes.

### Dynamic Object Interoperability

To achieve interoperability with different languages and enable authors to implement dynamic libraries, DLR gives a set of classes and interfaces used for this purpose: `IDynamicMetaObjectProvider`, `ExpandoObject`, `DynamicMetaObject`, and `DynamicObject`.

The advantages of DLR are:

- Simplified portability of dynamic languages to .NET.
- Allow dynamic features in static languages.
- Enhanced sharing of libraries and communication between static and dynamic languages.
- Fast dispatch and invocation (using caching).

In conclusion, DLR makes the dynamic type work as we know it, and we wouldn’t be able to use the dynamic type without it and the mechanisms it provides.

## Why Should We Use the Dynamic Type

By now, you might have caught a glimpse of where you can use a dynamic type. But let’s wade through some common scenarios in which dynamics could potentially enhance our applications and ensure our lives as developers are a bit more comfortable.

First of all, let’s make it evident that dynamic is not a magical solution. We shouldn’t try to use it just because we can.

While it has its own merits, dynamic objects are harder to work with while writing code since we don’t have IntelliSense for them due to the nature of the dynamic type. On the other hand, if we need to implement dynamic types everywhere, we are probably using the wrong type of language. Dynamic languages are best suited for those kinds of cases.

So what are the typical cases to apply a dynamic type to:

- Communicating with other kinds of dynamic languages
- Simplifying responses from API calls when we are unfamiliar with what type of object to expect (or we don’t care)

Ok, so let’s look into some concrete examples of dynamic in action.

## Dynamic vs. Reflection

Reflection is a mechanism to acquire a type from an abstract `System.Object`, and to invoke its members without any knowledge of the concrete type of that object.

For example, let’s see what a typical reflection flow looks like:

```csharp
EmployeeFactory employeeFactory = GetEmployeeFactory();
object firstEmployee = employeeFactory.GetFirstEmployee();
Type firstEmployeeType = firstEmployee.GetType();
object workStatusObject = firstEmployeeType.InvokeMember(
    "GetWorkStatus",
    BindingFlags.InvokeMethod,
    null,
    firstEmployee,
    null);
WorkStatus workStatus = Enum.Parse<WorkStatus>(workStatusObject.ToString());
Console.WriteLine(workStatus);
```

Although very complicated and extensive for its purpose, this piece of code retrieves an employee’s work status. All of that code was written to call a single method.

Because our `EmployeeFactory` class returns a generic `System.Object` type as an employee, this is the case. `System.Object` is the base class for all other classes, and we may use it if we don’t know what type of object we should anticipate.

To call the method of a `System.Object`, we must first determine what type of object it is. We do that by calling the `object.GetType()` method. Then, using the `InvokeMember()` method, we’ll be able to execute the `GetWorkStatus` function on the `firstEmployee` object.

After some enum parsing, we can finally determine the `firstEmployee`’s work status.

A bit complicated as it seems, but it works.

Now let’s look at how the same example looks when using dynamic:

```csharp
EmployeeFactory employeeFactory = GetEmployeeFactory();
dynamic firstEmployee = employeeFactory.GetFirstEmployee();
WorkStatus workStatus = firstEmployee.GetWorkStatus();
Console.WriteLine(workStatus);
```

Well, that looks much easier and quite simple to read. Types and method names didn’t have to be thought of as strings.

As a result of the dynamic vs. reflection struggle, we shall get:

- Cleaner and more readable code.
- Good performance due to dynamic type caching.
- Not having hardcoded strings in our code.
- Simpler implementation.

This example is for illustration purposes only. Both reflection and dynamic must be used sparingly and not just “because we can.”

Both of them can reduce the performance of an application and introduce bugs we could have avoided by properly implementing static mechanisms and abstractions.

## Var vs. Object vs. Dynamic

If you are a beginner to the C# world, you might still be trying to distinguish these three main keywords.

### Var Keyword

`var` is used to type a variable implicitly in a method scope. The variable is strongly typed, but the compiler makes up its mind which type it will be at runtime. We can even notice the type by hovering over the `var` keyword.

```csharp
var imNumber = 10; // implicitly typed variable
int exNumber = 10; // explicitly typed variable
```

Our opinion is that `var` enhances the readability of the code, and it should be used because, generally, we don’t need to type our variables explicitly, especially when the types are complicated.

Take, for example, `Dictionary<string, IEnumerable<Employee>>` or something even more complicated. The type of the variable cannot be altered at runtime.

### Object Keyword

`object` is an alias for `System.Object`. `System.Object` is the base class in C#. Every class in C# is obtained from `System.Object`, and we can employ that fact to make a more generic codebase. We will get the concrete type of the object we are working on at runtime through the `object` type. At the same time, we can achieve pretty much anything in terms of abstraction with `System.Object`, but sometimes we are constrained to use reflection to achieve our goal, which is not ideal.

If you want to use the type that is assigned to the `System.Object` variable, we need to explicitly cast it first. For example:

```csharp
object testObj = 10;
testObj = (int)testObj + 10;
```
