# D.5 MARSHALLING

Marshalling is the process of transferring objects from one environment to another. Here, the environments could be application domains, processes or machines on a network. The actual transfer of data objects is done with the help of channels. The concept of marshalling is particularly relevant in the context of distributed and client-server computing.

+   - Marshal by Value In this method, a copy of the object is sent to the other side of the boundary by serializing the object into the channel. This serialization is done with the help of the Serializable attribute.
+   - Marshal by Reference In this method, an object reference is created for the object to be marshalled and is serialized into the channel. On the other side of the boundary, a proxy is created to interact with the actual object through this reference. To marshal an object by reference we must derive it from the MarshalByRefObject class.

# Marshalling Across Application Domains

An application domain is the CLR's way of isolating the execution of applications. It is a boundary within which an application's context lies. Application domains are created within an operating system process. Objects in different application domains may communicate with each other through marshalling.

The following code shows a simple application to demonstrate the concept of marshalling across application domains:

# Program D.6 | MARSHALLING ACROSS APPLICATION DOMAINS

```
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
```