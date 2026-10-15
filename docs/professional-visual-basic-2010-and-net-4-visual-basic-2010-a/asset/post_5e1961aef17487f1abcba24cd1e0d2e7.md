
After this section, you will also see an additional capability provided through reflection: dynamic loading. You'll see how to gain a reference to an assembly on-the-fly and generate an instance of a type within the assembly.

> While the process of reflection is powerful and enables you to perform operations that would otherwise be impossible, you should be aware of the performance implications of using reflection heavily. Some reflection operations are rather slow; code that contains many such operations, as in a loop, can cause your program to experience noticeable delays.

## The Assembly Class

Almost all work with reflection will require you to work with the Assembly class. An instance of this class is associated with a .NET assembly.

There are several ways to get a reference to an instance of an Assembly class. Several shared methods of the Assembly class can return such an instance. The ones most commonly used are as follows:

- GetAssembly — Takes a Type instance and returns a reference to the assembly containing that Type. The assembly must already be available in the current application domain.
- GetExecutingAssembly — Returns the assembly that contains the code currently being executed.
- LoadFile — Loads an assembly using a string containing the filename in which the assembly resides.
- LoadFrom — Loads an assembly from a string containing a filename or URL.

Here is a code example that gets an assembly reference using each of the first three of these methods. The fourth method is covered in the section on dynamic loading later in the chapter.

```
Dim Assembly1 As [Assembly]
Assembly1 = [Assembly].GetAssembly(GetType(System.Boolean))
' This would return a reference to mscorlib

Dim Assembly2 As [Assembly]
Assembly2 = [Assembly].GetExecutingAssembly
' This would return a reference to the assembly
' containing this code.

Dim Assembly3 As [Assembly]
Dim sFileName As String
sFileName = "C:\Dev\MyProject\bin\Release\MyLibrary.dll"
Assembly3 = [Assembly].LoadFile(sFileName)
```

Code snippet from CodeSnippetsChapter31

You can also get a reference to an assembly by first getting a list of the assemblies loaded into an application and then choosing an assembly from that list.

## Getting Currently Loaded Assemblies

The application domain is the context for your current running application. You can work with an application domain using the AppDomain class in the System namespace. AppDomain has a shared property called CurrentDomain that will return the application domain in which you are currently running.

An application domain instance has a GetAssemblies method to obtain the assemblies currently loaded in the application domain. GetAssemblies returns an array of type Assembly.

Putting these capabilities together, you can print out the long name of each assembly in the current application domain using the following code:

```
Dim LoadedAssemblies As Assembly()
'Get the list of loaded assemblies from the current AppDomain.
LoadedAssemblies = AppDomain.CurrentDomain.GetAssemblies()

For Each LoadedAssembly In LoadedAssemblies
    ' There are many operations available on
    ' each assembly. This code simply lists the
    ' assembly's full name.
    Console.WriteLine(LoadedAssembly.FullName)
Next
```

## The Type Class

Chapter 4 discussed types in .NET. To recap, a type is a class, structure, or native value type such as a Double or Boolean.

A type is represented during reflection by an instance of the Type class. As Chapter 4 explained, you can get a reference to a type by using the GetType method of the type. However, you can also get a reference to a type via a method on an instance of the Assembly class that is associated with the assembly containing the type.

## Finding the Types in an Assembly

The GetTypes method of an Assembly class instance returns an array containing all the types in the assembly. You can also get a reference to a single type in an assembly with the GetType method, which takes a string with the fully qualified namespace path name of the type.

For example, the following code will print out the names of all the types in the assembly containing the currently executing code:

```
Dim CurrentAssembly As [Assembly]
CurrentAssembly = [Assembly].GetExecutingAssembly
For Each IndividualType In CurrentAssembly.GetTypes
    Console.WriteLine(IndividualType.Name)
Next
```

## Finding the Members of a Type

Reflection also allows you to explore a type and discover the members (properties and methods) of the type. The GetProperties method of a type will return an array of property descriptor objects, and the GetMethods method will return an array of method descriptors in the form of MethodInfo instances. The more general GetMembers method will return all the members of a Type, including properties, methods, events, and so forth. The following code, when placed inside a class, will print out all the properties, events, and public methods for the class:

```
For Each Member In Me.GetType.GetMembers
    Console.WriteLine(Member.Name)
Next

For Each IndividualProperty In Me.GetType.GetProperties
    Console.WriteLine(IndividualProperty.Name)
Next
```

There is some redundancy between these two methods. At a binary level, properties are actually pairs of get and set methods. That means you will see the get and set methods for a type's properties when you list out the methods.

Visual Basic Sub and Function routines are both considered methods in reflection. The only difference is that a Sub has no return value. If a method is a Function, and thus does have a return value, reflection allows you to discover the type of that return value.

Methods may have calling parameters. Reflection allows you to discover the calling parameters of a method, if there are any, using the GetParameters method of the MethodInfo instance for the method. The GetParameters method returns an array of ParameterInfo objects.

Using parameters, if any, a method can be invoked with the Invoke method of the MethodInfo instance. Suppose, for example, that the current class has a function named CalculateFee that takes an integer for customer ID and returns a decimal value.

Here is sample code to print the parameters for the method:

```
Dim MyMethodInfo As MethodInfo = Me.GetType.GetMember("CalculateFee")(0)
For Each ParamInfo In MyMethodInfo.GetParameters
    Console.WriteLine("Parameter name:" & ParamInfo.Name)
    Console.WriteLine("Parameter type:" & ParamInfo.ParameterType.Name)
Next
```

Code snippet from CodeSnippetsChapter31

To set up the parameter values and invoke the method, the code would look like this:

```
Dim MyMethodInfo2 As MethodInfo = _
    Me.GetType.GetMember("CalculateFee")(0)

'Create array of objects to serve as parameters.
'In this case, only one integer is needed.
Dim MyParameters() As Object = {4321}
Dim oReturn As Object
oReturn = MyMethodInfo2.Invoke(Me, MyParameters)
' Now cast oReturn to Decimal
```

Code snippet from CodeSnippetsChapter31

The code download for this chapter includes a WPF program that enables you to locate an assembly on disk and load the types from that assembly. For any type available in the assembly, you can then load all the methods of the type.

## DYNAMIC LOADING OF ASSEMBLIES

The preceding discussion about locating and loading assemblies refers to assemblies that are known at compile time through the application’s references. There is an alternative method of locating and loading an assembly that is useful for certain scenarios.

In this technique, the location of the assembly is supplied by the application, using a URL or filename. The normal rules for locating the assembly do not apply — only the location specified by the application is used.

The location is just a string variable, so it may come from a configuration file or a database. In fact, the assembly to be loaded may be newly created, and perhaps did not even exist when the original application was compiled. Because the information to load the assembly can be passed into the application on-the-fly at runtime, this type of assembly loading is called dynamic loading.

### The LoadFrom Method of the Assembly Class

The Assembly class has a shared method called LoadFrom that takes a URL or filename and returns a reference to the assembly at that location. Here’s a code example of LoadFrom in action, getting an assembly reference from a URL:
