
```
Console.WriteLine("class {0} contains method", t.FullName);
```

+   2. Save the file as VerifyClassMethod.cs in the D:\Black Books\C# 2010\Chapter 34 folder.

+   3. Compile the VerifyClassMethod.cs file by using the following command:
+    csc VerifyClassMethod.cs

+   4. Execute the following command to see the output of the file:
+    VerifyClassMethod VerifyClassMethod.exe Main

Figure 34.4 shows the output of the preceding command:

![](img/e073a4882197be4ab61103cbe0bcb394_1623_0.png)

Figure 34.4: Verifying that a Class Contains a Method

Let's explore how the code is executed. The SearchForMethod method contains the code to search for all the methods of a class. First, you retrieve each type in the assembly that represents a class in the source code. After you have verified that it is a class, you retrieve all the methods in the class and verify whether the name of the method is the same as the method passed into the application at the command line.

Reflection in C# is a powerful technique that can be used as much for proactive verification as for information processing. For example, you might check to see whether a given class contains a given method name to see whether this class is the same as the you expect it to be. The process of proactive verification protects your application against unexpected conditions that might occur in the real-world programming.

## Dumping the Methods and Their Parameters

Until now, this chapter has considered only the various elements of an assembly, such as the classes, derivations, and enumerations within the assembly. However, it is considerably more important to retrieve information about a single class. For example, if you want to write a documentation tool, you need to get the output of all the information about a class. In the following example, you explore the detailed information of the class architecture, the methods of the class, and the parameters associated with these methods.

The DumpParametersandMethods.cs example in the CD shows a simple application you can run on an assembly to dump the contents of a class. This application finds the class that you indicate at the command line and then dumps each method of the class, including the constructors for the class and their parameters. Note that the constructors are a separate type of method in C# and are not grouped with normal methods.

The following steps are performed to create and execute the DumpParametersandMethods.cs file (also available in the CD):

+   1. Open a Notepad and add the code given in Listing 34.6:

### Listing 34.6: Showing the Code for Example of Dumping the Methods and Their Parameters for a Class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Reflection.Emit;
class DumpParameterandMethod
{
    public static void DumpParameters(ParameterInfo[] pars)
    {
        // Dump them out
        foreach (ParameterInfo pi in pars) {
            Console.WriteLine("\n    Parameter Name: {0}",
            pi.Name);
            Console.WriteLine("    Parameter Type: {0}",
            pi.ParameterType);
            Console.WriteLine("    Is In? {0}",
            pi.IsIn);
            Console.WriteLine("    Is Out? {0}",
            pi.IsOut);
        }
    }
    public static void DumpType(Type t)
    {
        // Dump the constructors
        ConstructorInfo[] cons = t.GetConstructors();
        foreach (ConstructorInfo ci in cons)
        {
            // Get all the parameters
            ParameterInfo[] pars = ci.GetParameters();
            Console.WriteLine("\nConstructor: {0}", ci.Name);
            DumpParameters(pars);
        }
        // Dump each method
        MethodInfo[] methods = t.GetMethods();
        foreach (MethodInfo m in methods)
        {
            Console.WriteLine("\nMethod: {0}", m.Name);
            Console.WriteLine("Return Type: {0}", m.ReturnType);
            // Get all the parameters
            ParameterInfo[] pars = m.GetParameters();
            // Dump the parameters
            DumpParameters(pars);
        }
    }
    public static void ShowType(string assemblyName,
    string className)
    {
        Assembly assembly = Assembly.LoadFrom(assemblyName);
        if (assembly == null)
            return;
        Type[] types = assembly.GetTypes();
        foreach (Type t in types)
        {
            // only classes
            if (t.IsClass == false)
                continue;
            // only the one we want
            string Name = (string)t.FullName;
            if (Name != className)
                continue;
            // Okay, this is it, dump it
            DumpType(t);
        }
    }
    static void Main(string[] args)
```

## 35

## .NET Remoting in C# 2010

| If you need an Immediate Solution to: | See page: |
|---|---|
| Creating and Using Application Domains | 1599 |
| Using Objects in another Application Domain | 1601 |
| Creating a Remotable Class | 1602 |
| Creating a Host Application | 1603 |
| Creating a SingleCall Client Object | 1609 |
| Creating a Class for SingleTon Client Object | 1611 |
| Creating a Client Activated Object | 1616 |

![](img/e073a4882197be4ab61103cbe0bcb394_1626_0.png)

The remoting system on the client sends a call over a channel to the remoting system for sending objects on the server. Before sending the call to the server remoting system, an object is serialized into a specific transfer format using a formatter, such as SOAP or binary. The serialized message later reaches a transport channel that transfers it to the server remoting system using a specific protocol, such as HTTP or TCP. The remoting system on the server then handles the request and passes it to the formatter that deserializes the message back into its original format and forwards it to the dispatcher. The dispatcher forwards the message to the server object for taking appropriate action. The remoting system of server passes the result of server object to the remoting system of the client through the communication channel.

Now, let’s discuss the following topics to learn about the .NET remoting architecture in detail:

- Application domains
- Remotable and non-remotable objects
- Setting up remoting communication
- Channels
- Message sinks
- Formatters
- Proxies

### Application Domains

In .NET Framework, application domains are represented by the AppDomain class. This class provides isolation, unloading, and security boundaries to execute managed code.

The class hierarchy of the AppDomain class is as follows:

System.Object
  System.MarshalByRefObject
    System.AppDomain

Table 35.1 lists the noteworthy public properties of the AppDomain class:

| Table 35.1: Noteworthy Public Properties of the AppDomain Class |
| Property | Description |
| CurrentDomain | Obtains the current application domain for the current thread |
| FriendlyName | Obtains the friendly name of the application domain |
| SetupInformation | Obtains the application domain configuration information for an instance |
| ShadowCopyFiles | Obtains an indication whether or not all assemblies loaded in the application domain are shadow-copied |

Table 35.2 lists the noteworthy public methods of the AppDomain class:

| Table 35.2: Noteworthy Public Methods of the AppDomain Class |
| Method | Description |
| AppendPrivatePath() | Appends the specified name of the directory to the private path |
| ClearPrivatePath() | Resets the path that specifies the location of private assemblies to the empty string |
| ClearShadowCopyPath() | Resets the list of directories containing shadow-copied assemblies to the empty string |
| CreateInstance() | Builds a new instance of a specified type defined in a specified assembly |
| CreateInstanceAndUnwrap() | Builds a new instance that is not wrapped of a specified type in a specified assembly |
| CreateInstanceFrom() | Builds a new instance of a specified type defined, where the source is specified in the specified assembly file |
