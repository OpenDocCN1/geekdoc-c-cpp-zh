
```csharp
class ClassB
{
	public static void Main(string[] args)
	{
		ClassA = new ClassA();
		D.display();
		System.Console.Read();
	}
}
```

The output of the above code will be the same as shown in Figure D.2. However, if you open the executable of the above program with ILDasm, you'll see the usage of the custom CodeChecked attribute, as shown in Figure D.4.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_480_0.png)

Reflection is the method of reading metadata at runtime and facilitate type discovery. It is used to dynamically (at runtime) discover the types implemented in an assembly and make use of those types.

.NET allows the programmers to exercise reflection with the help of a number of types contained in the System.Reflection namespace. Table D.2 lists some of the types in the System.Reflection namespace:

## Table D.2 System.Reflection Types

| Type | Description |
|---|---|
| Assembly | Allows access to an assembly's metadata. |
| ModuleInfo | Allows access to a module's metadata. |
| MemberInfo | Allows access to a member's metadata. |
| MethodInfo | Allows access to a method's metadata. |
| PropertyInfo | Allows access to a property's metadata. |

The above types are used in conjunction with the members of the System.Type class to actually reflect metadata information. Here, System.Type symbolizes the type of an object. For example, we can use the System.Type.GetProperties() method to return an array of PropertyInfo types for an object.

We can use reflection to perform the following tasks:

- Viewing metadata
- Type discovery
- Reflecting on a type

## Viewing Metadata

As already stated, reflection can be used to simply view the metadata pertaining to a type. The following program code modifies the ConsoleApplication1.cs program to demonstrate the viewing of metadata pertaining to methods of the class ClassD. It retrieves the name and return types of all the public methods of the specified class.

## Program D.3 RETRIEVING NAME AND RETURN TYPES OF ALL PUBLIC METHODS OF A CLASS

```
//ViewingMetadD.cs
namespace ViewingMetada
{
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Reflection;

    public class ClassA
    {
        public void display()
        {
            Console.WriteLine("Hello! We are in ClassA");
        }
    }
    class ClassB
    {
        public static void Main(string[] args)
        {
            ClassA A = new ClassA();
```
```
D.display();
Type t = typeof(ClassA);
DisplayMethods(t);
System.Console.Read();
}
public static void DisplayMethods(Type t)
{
    MethodInfo[] MI = t.GetMethods();
    foreach (MethodInfo M in MI)
    {
        Console.WriteLine("Public Method: {0}", M.Name);
        Console.WriteLine("Return Type {0}\n", M.ReturnType);
    }
}
}
```

Figure D.5 shows the output of the above program:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_482_0.png)

Fig. D.5 Viewing metadata

## Type Discovery

Reflection can be used to reflect upon an assembly to discover the various encapsulated types. Similarly, it can be used to reflect upon a type to discover its containing members. The following code shows a program to discover the types associated with the default Mscorlib.dll assembly.

## Program D.4 TYPES ASSOCIATED WITH THE DEFAULT MSCORLIB.DLL ASSEMBLY

```
//TypeDisc.cs
namespace TypeDisc
{
using System;
using System.Reflection;
public class TypeDisc
{
public static void Main()
{
Assembly Assem = Assembly.Load("Mscorlib.dll");
Type[] Assem_Types = Assem.GetTypes();
Console.WriteLine("The various types in Mscorlib.dll are:\n");
foreach(Type t in Assem_Types)
Console.WriteLine("{0}", t);
}
```

Mscorlib.dll being the default .NET assembly contains numerous type implementations, as shown in the output in Fig. D.6:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_483_0.png)

Fig. D.6 Type Discovery

In the above program, we have used the GetTypes method to reflect upon all the types contained in the Mscorlib.dll library. However, if we want to reflect on a single pre-specified type then we can use the GetType method of the Type class, as explained in the next section.

## Reflecting on a Type

It may be required for us to look for a specific type in an assembly before it can be used in the main application. This reflection on a single type is done with the help of the Type.GetType method. The following code modifies the TypeDisc.cs program to reflect on a single type System.Console:

## Program D.5 | REFLECTING ON A TYPE

```
//SingleTypeDisc.cs
namespace SingleTypeDisc
{
using System;
using System.Reflection;
public class SingleTypeDisc
{
public static void Main()
{
Assembly Assem = Assembly.Load("Mscorlib.dll");
Type Assem_Type = Assem.GetType("System.Console");
Console.WriteLine("{0} found in Mscorlib.dll", Assem_Type);
}
}
}
```

Figure D.7 shows the output of the above program:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_484_0.png)

Fig. D.7 Reflecting on a Single Type

## D.5 MARSHALLING

Marshalling is the process of transferring objects from one environment to another. Here, the environments could be application domains, processes or machines on a network. The actual transfer of data objects is done with the help of channels. The concept of marshalling is particularly relevant in the context of distributed and client-server computing.

- Marshal by Value In this method, a copy of the object is sent to the other side of the boundary by serializing the object into the channel. This serialization is done with the help of the Serializable attribute.
- Marshal by Reference In this method, an object reference is created for the object to be marshalled and is serialized into the channel. On the other side of the boundary, a proxy is created to interact with the actual object through this reference. To marshal an object by reference we must derive it from the MarshalByRefObject class.

## Marshalling Across Application Domains

An application domain is the CLR's way of isolating the execution of applications. It is a boundary within which an application's context lies. Application domains are created within an operating system process. Objects in different application domains may communicate with each other through marshalling.

The following code shows a simple application to demonstrate the concept of marshalling across application domains:

## Program D.6 | MARSHALLING ACROSS APPLICATION DOMAINS

```csharp
//AppDomain.cs
using System;
using System.Reflection;
public class AD_Test : MarshalByRefObject
{
	public void DomainName()
	{
		Console.WriteLine("The current Application Domain is {0}", AppDomain.CurrentDomain.FriendlyName);
	}
}

class Marshal
{
	public static void Main()
	{
		AD_Test ADT1 = new AD_Test();
		ADT1.DomainName();
		AppDomain AD = AppDomain.CreateDomain("2nd Application Domain");
		AD_Test ADT2 = (AD_Test) AD.CreateInstanceAndUnwrap(Assembly.GetExecutingAssembly().GetName(), "AD_Test");
		ADT2.DomainName();
	}
}
```

In the above code, a new application domain is created by using the CreateDomain method. Fig. D.8 shows the output of the above code:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_486_0.png)

Fig. D.8 Marshaling Across Application Domains

## D.6 REMOTING

Remoting is a little more advanced concept in which marshalling of objects happens across process and machine boundaries. To set up remoting, we need to create server-side remote objects to cater to the client (application) requests.

## Understanding Server Object Types

The type of remote object to be configured on the server side depends on the type of request expected from the client. The various types of server side objects are the following:

- Single Call A single call object can service only one client request at a time. Thus, for multiple client requests, an equal number of single call objects are created.
- Singleton A singleton object can service multiple client requests single-handedly. Such an object is created when it is required for the different clients to share data with each other.
- Client-Activated Objects (CAO): Client-activated objects are server side objects that are instantiated only when a corresponding request is received from the client. Upon client's request, an object reference is sent back to the client, which then uses a proxy to interact with the object. For each client request a new object is created. Thus different clients do not share data with each other.

## Specifying a Server with an Interface

The first step towards creating a server side remote object is to create its corresponding interface. The following code shows a simple interface for realizing a remote object:
