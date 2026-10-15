
```
var game = new Pair<string>("Redskins", "Eagles");
foreach (string name in game.GetReverseEnumerator())
{
    Console.WriteLine(name);
}
```

Note that you return IEnumerable<T>, not IEnumerator<T>. This is different from IEnumerable<T>.GetEnumerator(), which returns IEnumerator<T>. The code in Main() demonstrates how to call GetReverseEnumerator() using a foreach loop.

## yield Statement Requirements

You can use the yield return statement only in members that return an IEnumerator<T> or IEnumerable<T> type, or their nongeneric equivalents. Members whose bodies include a yield return statement may not have a simple return. If the member uses the yield return statement, the C# compiler generates the necessary code to maintain the state of the iterator. In contrast, if the member uses the return statement instead of yield return, the programmer is responsible for maintaining his own state machine and returning an instance of one of the iterator interfaces. Further, just as all code paths in a method with a return type must contain a return statement accompanied by a value (assuming they don’t throw an exception), so all code paths in an iterator must contain a yield return statement if they are to return any data.

The following additional restrictions on the yield statement result in compiler errors if they are violated:

- The yield statement may appear only inside a method, a user-defined operator, or the get accessor of an indexer or property. The member must not take any ref or out parameter.
- The yield statement may not appear anywhere inside an anonymous method or lambda expression (see Chapter 12).
- The yield statement may not appear inside the catch and finally clauses of the try statement. Furthermore, a yield statement may appear in a try block only if there is no catch block.

## 17

## Reflection, Attributes, and Dynamic Programming

ATTRIBUTES ARE A MEANS OF inserting additional metadata into an assembly and associating the metadata with a programming construct such as a class, method, or property. This chapter investigates the details surrounding attributes that are built into the framework and describes how to define custom attributes. To take advantage of custom attributes, it is necessary to identify them. This is handled through reflection. This chapter begins with a look at reflection, including how you can use it to dynamically bind at execution time based on member invocation by name (or metadata) at compile time. This is frequently performed within tools such as a code generator. In addition, reflection is used at execution time when the call target is unknown.

![](img/25683ccec0773ba5b8794b11f2b12877_721_0.png)

XmlSerializer, ValueType, and DataBinder are a few of the classes in the framework that use reflection for portions of their implementation as well.

## Accessing Metadata Using System.Type

The key to reading a type’s metadata is to obtain an instance of System.Type that represents the target type instance. System.Type provides all the methods for retrieving the information about a type. You can use it to answer questions such as the following:

- What is the type’s name (Type.Name)?
- Is the type public (Type.IsPublic)?
- What is the type’s base type (Type.BaseType)?
- Does the type support any interfaces (Type.GetInterfaces())?
- Which assembly is the type defined in (Type.Assembly)?
- What are a type’s properties, methods, fields, and so on (Type.GetProperties(), Type.GetMethods(), Type.GetFields(), and so on)?
- Which attributes decorate a type (Type.GetCustomAttributes())?

There are more such members, but all of them provide information about a particular type. The key is to obtain a reference to a type’s Type object, and the two primary ways to do so are through object.GetType() and typeof().

Note that the GetMethods() call does not return extension methods. These methods are available only as static members on the implementing type.

## GetType()

object includes a GetType() member and, therefore, all types include this function. You call GetType() to retrieve an instance of System.Type corresponding to the original object. Listing 17.1 demonstrates this process, using a Type instance from DateTime. Output 17.1 shows the results.

## LISTING 17.1: Using Type.GetProperties() to Obtain an Object’s Public Properties

```
DateTime dateTime = new DateTime();

Type type = dateTime.GetType();
foreach (
    System.Reflection.PropertyInfo property in
    type.GetProperties()
)
{
    Console.WriteLine(property.Name);
}
```

The typeof expression is resolved at compile time such that a type comparison—perhaps comparing the type returned from a call to GetType()—can determine if an object is of a specific type.

## Member Invocation

The possibilities with reflection don’t stop with retrieving the metadata. The next step is to take the metadata and dynamically invoke the members it references. Consider the possibility of defining a class to represent an application’s command line. The difficulty with a CommandLineInfo class such as this relates to populating the class with the actual command-line data that started the application. However, using reflection, you can map the command-line options to property names and then dynamically set the properties at runtime. Listing 17.3 demonstrates this process.

## LISTING 17.3: Dynamically Invoking a Member

```
using System;
using System.Diagnostics;

public partial class Program
{
    public static void Main(string[] args)
    {
        string errorMessage;
        CommandLineInfo commandLine = new CommandLineInfo();
        if (!CommandLineHandler.TryParse(
            args, commandLine, out errorMessage))
        {
            Console.WriteLine(errorMessage);
            DisplayHelp();
        }

        if (commandLine.Help)
        {
            DisplayHelp();
        }
        else
        {
            if (commandLine.Priority !=
                ProcessPriorityClass.Normal)
            {
                // Change thread priority
            }
        }
        // ...
    }
```

The CAS permissions are set up to allow private member invocation in this case because the program runs from the local computer. By default, locally installed programs are part of the trusted zone and have appropriate permissions granted. Programs run from a remote location will need to be explicitly granted such a right.

## Reflection on Generic Types

The introduction of generic types in version 2.0 of the CLR necessitated additional reflection features. Runtime reflection on generics determines whether a class or method contains a generic type, and any type parameters or arguments it may include.

## Determining the Type of Type Parameters

In the same way that you can use a typeof operator with nongeneric types to retrieve an instance of System.Type, so you can use the typeof operator on type parameters in a generic type or generic method. Listing 17.4 applies the typeof operator to the type parameter in the Add method of a Stack class.

## LISTING 17.4: Declaring the Stack<T> Class

```
public class Stack<T>
{
    // ...
    public void Add(T i)
    {
        // ...
        Type t = typeof(T);
        // ...
    }
    // ...
}
```

Once you have an instance of the Type object for the type parameter, you may then use reflection on the type parameter itself to determine its behavior and tailor the Add method to the specific type more effectively.

## Determining Whether a Class or Method Supports Generics

In the System.Type class for the version 2.0 release of CLR, a handful of methods were added that determine whether a given type supports generic parameters and arguments. A generic argument is a type parameter
