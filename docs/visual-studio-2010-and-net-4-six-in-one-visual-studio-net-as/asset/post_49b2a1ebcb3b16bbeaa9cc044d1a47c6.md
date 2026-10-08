
The code is really simple. The Python object located in the Python.Hosting namespace is responsible for managing the run-time environment. You can obtain a reference for object (named calculator in this C# context) to access the operations defined by the Calculate.py mini-program:

```
var ipy = Python.CreateRuntime();
dynamic calculator = ipy.UseFile("Calculate.py");
```

You can invoke the Add operation defined in the Python snippet through the calculator object:

```
calculator.Add("Welcome in IronPython on ",
DateTime.Now.ToShortString());
calculator.Add(i, j)
```

As a benefit of dynamic behavior, you can pass two strings or integers to Add, and dynamically maps the call to concatenation or addition, respectively. Of course, there are many other type combinations accepted by Add. Figure 10-4 shows the output of the console application.

![](img/b5597c749e848b27b0d305153ae16106_448_0.png)

FIGURE 10-4: Output of the application

> The IronPython run-time comes with a brief language tutorial. Open the Tutorial\Tutorial.htm file under the installation folder, and play with the language by modifying the Calculate.py and Program.cs files.

## ExpandoObject Example

The DLR defines an interesting type called ExpandoObject in the System.Dynamic namespace. This is a great time to demonstrate the power of the DLR when used together with C# 4.0, which now supports dynamic operations (operations resolved at run-time). Instead of telling you what this type is about, let's first see an example.

Create a C# console application and name it ExpandoObjectDemo. Listing 10-2 shows the code to copy into the Program.cs file.

## LISTING 10-2: Program.cs File of ExpandoObjectDemo

```sharp
using System;
using System.Dynamic;

namespace ExpandoObjectDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic customer = new ExpandoObject();
            customer.Id = 116;
            customer.Name = "John Doe";
            Console.WriteLine("{0}, {1}", customer.Id, customer.Name);

            dynamic address = new ExpandoObject();
            address.Id = "SHIP";
            address.Line1 = "xxxx 7th Street";
            address.Line2 = "My Great Company";
            address.City = "Los Angeles";
            address.State = "CA";
            Console.WriteLine("address type and State: {0}, {1}", address.Id, address.State);
        }
    }
}
```

Code file [Program.cs] available for download at Wrox.com

Reading this, the first question might ask, "Does this code work at all?" It creates two ExpandoObjects. The first time it is used as a Customer object with Id and Name properties; the second time as an Address object with properties such as Id, Line1, State, and so on.

The answer is that this object compiles and runs without errors or warnings, because of the dynamic behavior of ExpandoObject. Moreover, the following code snippet is also valid. You could insert it into 10-2.

```csharp
dynamic triangle = new ExpandoObject();
triangle.A = new { X = 0, Y = 0, Z = 0 };
triangle.B = new { X = 100, Y = 100, Z = 0 };
triangle.C = new { X = 0, Y = 100, Z = 100 };
```

ExpandoObject is a "jolly joker" whose members can be dynamically added and removed at run-time. The only public member defined by this type is its default constructor, and of course, inherits public methods from System.Object. Figure 10-5 shows all of them as shown in the IntelliSense list when editing your code.

The key to this behavior is the dynamic type used to declare the variables referencing dynamic instances. This is a new type in C# that instructs the compiler to treat all operations on the referenced object dynamically, using the DLR.

For the statements setting ExpandoObject properties, instead of compiling MSIL directly to set those properties, the compiler emits send messages to the object, such as, "Set the property id to \"116\"" (Regardless, MSIL property setter instructions could not be emitted because an ExpandoObject does not have an id property).

The DLR sends the message to the object at run-time, and stores the name and value of property in a dictionary. When the id property is about to read, "Get the value of the property named id", and uses the ExpandoObject, and its dictionary to look up and retrieve the value.

## DynamicObject Example

The DLR provides you with utility types you can use to create your own dynamic objects. At run-time, a dynamic operation is dispatched to the target object with the following steps:

- 1. If the target is a COM object, the operation is dispatched dynamically through the Dispatch interface.
- 2. If the target object type implements the DynamicMetaToObject interface of the System.Dynamic namespace, interface is used, and the target is asked to perform the operation.
- 3. Otherwise, the target is a standard .NET object, and the operation will be dispatched using reflection on its type, and a C# "run-time binder" that implements a C# lookup and overload resolution semantics at run-time.

The DynamicMetaToObject interface contains about dozen methods to implement. The DLR provides the DynamicObject type to implement this interface as a base class for your dynamic objects.

Let’s create a simple class to resolve environment variables with property syntax. For example, you do not have to write something like this:

```csharp
Environment.GetVariable("Path")
```

Instead, you can use a dynamic shortcut such as this:

```csharp
envObject.Path =
```

![](img/b5597c749e848b27b0d305153ae16106_450_0.png)

FIGURE 10-5: ExpandoObject members in IntelliSense

Start with a C# sample application, and name it DynamicObjectDemo. Add a new class item file with the name DynamicEnvironment.cs to the project. Listing 10-3 shows the code you should copy to this file.

## LISTING 10-3: DynamicEnvironment.cs

```csharp
using System;
using System.Dynamic;

namespace DynamicObjectDemo
{
    public class DynamicEnvironment: DynamicObject
    {
        private EnvironmentTarget _TargetEnv;
        private bool _ignoreMissingProperty;

        public DynamicEnvironment(EnvironmentTarget targetEnv, bool ignoreMissingProperty = false)
        {
            _TargetEnv = targetEnv;
            _ignoreMissingProperty = ignoreMissingProperty;
        }

        public override bool TryGet(Binder binder, out object result)
        {
            result = Environment.GetVariable(binder.Name, _TargetEnv);
            return result != null || _ignoreMissingProperty;
        }
    }
}
```

> Code file [DynamicEnvironment.cs] available for download at Wrox.com

The constructor allows you to pass optional EnvironmentTarget to set if you want to bind the object to machine or user. The ignoreMissingProperty true value allows to retrieve null value for non-existing variables instead of raising exception. The property resolution is handled by the overridden TryGet method. It accepts two parameters. The binder receives the operation message from the DLR. In this case, it handles the name of the property to resolve. The result should be set to the object to be retrieved from the operation, and in this case, it will be the value. If the property name refers to an existing environment variable, the resolution is successful, and it retrieves the value; otherwise returns null, or fails, depending on the value of ignoreMissingProperty.

The return value of the method is set true if the operation can be handled by this method; otherwise it is false. The logic of the method is simple. Listing 10-4 shows the Program.cs.

## LISTING 10-4: Program.cs File of DynamicObjectDemo

```csharp
using System;

namespace DynamicObjectDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic env = new DynamicEnvironment(ignoreMissingProperty: true);
            Console.WriteLine(env.Path);
            Console.WriteLine(env.Temp);
            Console.WriteLine(env.NonExisting ?? "null");
        }
    }
}
```

This program runs as expected. Because there is no environment variable with name NonExisting, the third line will be "null". Set the ignoreMissingProperty value to false to have DynamicEnvironment to raise an exception when an unknown property is used. Running the program will now raise a RuntimeBinderException (shown in Figure 10-6) telling you that the NonExisting property could not be resolved.

![](img/b5597c749e848b27b0d305153ae16106_452_0.png)

FIGURE 10-6: RuntimeBinderException raised

> This is very simple, and not really robust. For example, it cannot resolve USERNAME or MACHINENAME, because those are not available through the Environment.GetVariable method. Play with this example and try to make it more useful by extending it with these features!

## Type Equivalence

.NET 4 has greatly improved COM interoperability. From the CLR's point of view, the most important feature is type equivalence. It is required to deploy applications without deploying PIAs for the COM components with which the application operates. This feature is implemented at the
