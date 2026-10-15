
uses one of the two methods—Assembly.GetType or Assembly.GetTypes-- to get the Type object from assemblies that has not been loaded.

- Module class--Retrieves information about parent assembly, classes in the module, and all the global methods available in the classes.
- ConstructorInfo class--Retrieves the information about a constructor, such as constructor name, parameters, access modifiers, and various implementation details. The ConstructorInfo class uses the GetConstructor or GetConstructors method of a Type object to retrieve the constructor information.
- MethodInfo class--Retrieves information about a method in the class, module, or assembly, such as method name, return type, parameters, access modifiers, and implementation details. The MethodInfo class uses either the GetMethod or GetMethods method of a type to retrieve the information.
- FieldInfo class--Retrieves information about the fields, such as name, access modifiers, and implementation details. In addition, you can use this class to get or set field values of a class.
- EventInfo class--Retrieves information about events, such as name, event-handler data type, custom attributes, declaring type, and reflected type.
- PropertyInfo class--Retrieves information about properties, such as property name, data type, declaring type, reflected type, and read-only or writable status of a property. In addition, this class also gets or sets the properties values.
- ParameterInfo class--Retrieves information about a parameter, such as its name, data type, whether it is an input or an output parameter, and its position in a method signature. This class uses the GetParameters method to return an array of ParameterInfo objects that represents the parameters of a method.

The other namespace used for reflection is System.Reflection.Emit. This namespace creates the type at runtime and invokes this type as and when required. The System.Reflection.Emit namespace typically writes the information to appropriate types. This namespace contains classes that can be used by the compiler or tool to emit metadata and Microsoft Intermediate Language (MSIL).

Next, you learn about dynamic loading of assembly using reflection.

## Using Reflection for Dynamic Loading of Assembly

Let's look at the simplest form of reflection—loading an assembly at runtime and investigating what information you can find out about the assembly. To do this, you need to make use of the Reflection namespace. The following import statement is used to know about this functionality in your application:

```
using System.Reflection;
```

Loading of individual assemblies from the outside world can be done after the reflection library functionality has been loaded in your application. You can use the LoadFrom static method of the Assembly class from the Reflection library to load the individual assemblies. Now, if you have the name of the assembly you want to load in a variable named assemblyName, the following code-snippet is used:

```
Assembly assembly = Assembly.LoadFrom(assemblyName);
```

After you have access to the assembly object, you can interrogate it. The easiest way to interrogate the assembly object is to use the GetTypes method. This method returns an array of Type objects that contain information about the various kinds of types defined in this assembly. You can find out the class names, namespaces, access levels, and much more from the following Type object for a given type:

```
Type[] types = assembly.GetTypes()
```

After you have the list of available types in an assembly, you can find various kinds of information from them. The first group of functions available in the Type class determines what kind of type you are dealing with. Table 34.1 describes the properties of the Type object:

## Table 34.1: Properties Available in the Type Object

| Property | Purpose |
|---|---|
| IsClass | Indicates that the type is a class if this property is true. |
| IsEnum | Indicates that the type is an enumeration if this property is true |
| IsInterface | Indicates that the type is an interface if this property is true |
| IsValueType | Indicates that the type is a Value Type (a struct) if this property is true |

You can determine the type and deal with it appropriately using the preceding four simple properties. After you have ascertained the type of the property, you can determine whether it is publicly available to use in an application.

Two properties are available for determining the access scope of a type—IsPublic and IsNotPublic properties. The IsPublic property determines a public method, while the IsNotPublic property determines private or protected method, or which is actually a non-public method. For example, the following code snippet shows all the public types of an assembly:

```
Type[] types = assembly.GetTypes();
foreach ( Type t in types )
{
if ( t.IsPublic )
Console.WriteLine("Class {0} is public!", t.FullName );
}
```

> NOTE
> You learn more about classes in the Obtaining Class and Type Information from an Assembly Section in the Immediate Solutions section later in this chapter.

Moreover, reflection enables you to explore into the implementation of a class and the parameters and methods that are used in the class; however, reflection does not allow you to get a dump of the code of the method. If it does so, it is easy for unscrupulous individuals to copy algorithms and code from a C# assembly for their own use.

All the methods that allow you to get information about the types defined in the class have a common functionality. Table 34.2 lists the most common methods that are used to retrieve information about the types in general as well as information stored within these types:

## Table 34.2: Common Methods That are Used to Retrieve Type Information

| Value Type | What it Represents |
|---|---|
| GetTypes | Retrieves all types for a given assembly |
| GetMethods | Retrieves all methods for a given current Type |
| GetConstructors | Retrieves all constructors for a given current Type |
| GetProperties | Retrieves all properties for a given current Type |
| GetEvents | Retrieves all events for a given current Type |
| GetInterfaces | Retrieves all interfaces supported by a given current Type |

You first retrieve the types from the assembly by using the GetTypes method to use these common methods. These method return an array of types for the assembly, which consists of classes, structures, enumerations, and events. If you check for the appropriate type of the Type object and verify that it is a class or a structure, you can then apply the other methods, such as GetMethods and GetConstructors methods, to retrieve the information you are interested in. For more information on this process, check the example in the Dumping the Methods and Their Parameters for a Class section later in the Immediate Solutions section of this chapter.

## Immediate Solutions

We have aforementioned that the purpose of reflection is to find out information about classes and other types in C# without exploring the source code manually. Let's imagine that you need to create an application that consists of a class implementing certain methods. Now, you can use the reflection process to write a tool that allows you to see all the classes in all the assemblies, which you need to know about your application. You can also examine each assembly for the class names and other type information available in the assembly. In this chapter, we are creating console applications, which you can execute on the command prompt of Visual Studio 2010. All the created applications are saved and executed in the D:\Black Books\C# 2010\Chapter 34 location

## Obtaining Class and Type Information from an Assembly

In this section, we are creating two classes, namely, ObtainClassInformation and EventTestClass classes, to examine an assembly and explore the classes, interfaces, and events present within an assembly.

The following steps are performed to create and execute the ObtainClassInformation.cs and EventTestClass.cs files (also available in the CD):

- 1. Open a Notepad and add the code given in Listing 34.1:

### Listing 34.1: Showing the Code for Obtaining Class and Type Information

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
namespace ObtainClassInformation
{
    class Program
    {
        public static void ShowInterfaces(Type t)
        {
            Type[] interfaces = t.GetInterfaces();
            Console.WriteLine("Implemented Interfaces");
            foreach (Type type in interfaces)
            {
                Console.WriteLine("Interface : {0}", type.FullName);
                if (type.IsPublic)
                    Console.WriteLine("Scope: Public");
                else
                    Console.WriteLine("Scope: Private");
            }
        }
        public static void ShowEvents(Type t)
        {
            EventInfo[] events = t.GetEvents();
            Console.WriteLine("Implemented Events");
            foreach (EventInfo e in events)
            {
                Console.WriteLine("Event name: {0}", e.Name);
                Console.WriteLine("Multicast: {0}", e.IsMulticast ? "Yes" : "No");
                Console.WriteLine("Member Type {0}", e.MemberType.ToString());
            }
        }
        public static void ShowTypes(string name, Assembly assembly)
```
