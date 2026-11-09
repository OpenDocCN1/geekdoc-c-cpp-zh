
```csharp
// We're calling a method on an object; no exception is thrown
Console.WriteLine("Returned object created " + mbt.ToString());
Console.WriteLine("Successful call.");
}
catch (AppDomainUnloadedException) {
    Console.WriteLine("Failed call.");
}


// DEMO 3: Cross-AppDomain Communication using non-marshallable type ***
Console.WriteLine("{0}Demo #3", Environment.NewLine);

// Create new AppDomain (security & configuration match current AppDomain)
ad2 = AppDomain.CreateDomain("AD #2", null, null);

// Load our assembly into the new AppDomain, construct an object, marshal
// it back to our AD (we really get a reference to a proxy)
mbrt = (MarshalByRefType)
    ad2.CreateInstanceAndUnwrap(exAssembly, "MarshalByRefType");

// The object's method returns a non-marshallable object; exception
NonMarshalableType nmt = mbrt.MethodArgAndReturn(callingDomainName);
// We won't get here...
}


// Instances can be marshaled-by-reference across AppDomain boundaries
public sealed class MarshalByRefType : MarshalByRefObject {
    public MarshalByRefType() {
        Console.WriteLine("{0} ctor running in {1}",
            this.GetType().ToString(), Thread.GetDomain().FriendlyName);
    }

    public void SomeMethod() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
    }

    public MarshalByValType MethodWithReturn() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
        MarshalByValType t = new MarshalByValType();
        return t;
    }

    public NonMarshalableType MethodArgAndReturn(String callingDomainName) {
        // NOTE: callingDomainName is [Serializable]
        Console.WriteLine("Calling from {0} to {1}.",
            callingDomainName, Thread.GetDomain().FriendlyName);
        NonMarshalableType t = new NonMarshalableType();
        return t;
    }
}


// Instances can be marshaled-by-value across AppDomain boundaries
[Serializable]
public sealed class MarshalByValType : Object {
    private DateTime m_CreationTime = DateTime.Now; // NOTE: DateTime is [Serializable]

    public MarshalByValType() {
        Console.WriteLine("{0} ctor running in {1}, Created on {2:D}",
            this.GetType().ToString(),
            Thread.GetDomain().FriendlyName,
            m_CreationTime);
    }

    public override String ToString() {
        return m_CreationTime.ToLongDateString();
    }
}

// Instances cannot be marshaled across AppDomain boundaries
// [Serializable]
public sealed class NonMarshalableType : Object {
    public NonMarshalableType() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
    }
}
```

If you build and run the Ch22-1-AppDomains application, you get the following output:

```
Default AppDomain's friendly name= Ch22-1-AppDomains.exe
Main assembly=Ch22-1-AppDomains, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null

Demo #1
MarshalByRefType ctor running in AD #2
Type=MarshalByRefType
Is proxy=True
Executing in AD #2
Failed call.

Demo #2
MarshalByRefType ctor running in AD #2
Executing in AD #2
MarshalByValType ctor running in AD #2, Created on Friday, August 07, 2009
Is proxy=False
Returned object created Friday, August 07, 2009
Returned object created Friday, August 07, 2009
Successful call.

Demo #3
MarshalByRefType ctor running in AD #2
Calling from 'Ch22-1-AppDomains.exe' to 'AD #2'.
Executing in AD #2

Unhandled Exception: System.Runtime.Serialization.SerializationException:
Type 'NonMarshalableType' in assembly 'Ch22-1-AppDomains, Version=0.0.0.0,
Culture=neutral, PublicKeyToken=null' is not marked as serializable.
at MarshalByRefType.MethodArgAndReturn(String callingDomainName)
at Program.Marshalling()
at Program.Main()
```

Now, I will discuss what this code and the CLR are doing.

Inside the **Marshalling** method, I first get a reference to an **AppDomain** object that identifies the AppDomain the calling thread is currently executing in. In Windows, a thread is always created in the context of one process, and the thread lives its entire lifetime in that process. However, a one-to-one correspondence doesn’t exist between threads and AppDomains. AppDomains are a CLR feature; Windows knows nothing about AppDomains. Since multiple AppDomains can be in a single Windows process, a thread can execute code in one AppDomain and then execute code in another AppDomain. From the CLR’s perspective, a thread is executing code in one AppDomain at a time. A thread can ask the CLR what AppDomain it is currently executing in by calling **System.Threading.Thread**’s static **GetDomain** method. The thread could also query **System.AppDomain**’s static, read-only **CurrentDomain** property to get the same information.

When an AppDomain is created, it can be assigned a *friendly name*. A friendly name is just a **String** that you can use to identify an AppDomain. This is typically useful in debugging scenarios. Since the CLR creates the default AppDomain before any of our code can run, the CLR uses the executable file’s file name as the default AppDomain’s friendly name. My **Marshalling** method queries the default AppDomain’s friendly name by using **System.AppDomain**’s read-only **FriendlyName** property.

Next, my **Marshalling** method queries the strong-name identity of the assembly (loaded into the default AppDomain) that defines the entry point method **Main** that calls **Marshalling**. This assembly defines several types: **Program**, **MarshalByRefType**, **MarshalByValType**, and **NonMarshalableType**. At this point, we’re ready to look at the three demos that are all pretty similar to each other.

## Demo #1: Cross-AppDomain Communication that Uses Marshal-by-Reference

In Demo #1, **System.AppDomain**’s static **CreateDomain** method is called, instructing the CLR to create a new AppDomain in the same Windows process. The **AppDomain** type actually offers several overloads of the **CreateDomain** method; I encourage you to study them and select the version that is most appropriate when you are writing code to create a new AppDomain. The version of **CreateDomain** that I call accepts three arguments:

- A **String** identifying the friendly name I want assigned to the new AppDomain — I’m passing in "AD #2" here.
- A **System.Security.Policy.Evidence** identifying the evidence that the CLR should use to calculate the AppDomain’s permission set — I’m passing **null** here so that the new AppDomain will inherit the same permission set as the AppDomain creating it.

Usually, if you want to create a security boundary around code in an AppDomain, you’d construct a **System.Security.PermissionSet** object, add the desired permission objects to it (instances of types that implement the **IPermission** interface), and then pass the resulting **PermissionSet** object reference to the overloaded version of the **CreateDomain** method that accepts a **PermissionSet**.

- A **System.AppDomainSetup** identifying the configuration settings the CLR should use for the new **AppDomain**. Again, I’m passing **null** here so that the new AppDomain will inherit the same configuration settings as the AppDomain creating it. If you want the AppDomain to have a special configuration, construct an **AppDomainSetup** object, set its various properties to whatever you desire such as the name of the configuration file for example, and then pass the resulting **AppDomainSetup** object reference to the **CreateDomain** method.

Internally, the **CreateDomain** method creates a new AppDomain in the process. This AppDomain will be assigned the specified friendly name, security, and configuration settings. The new AppDomain will have its very own loader heap, which will be empty because there are currently no assemblies loading into the new AppDomain. When you create an AppDomain, the CLR does not create any threads in this AppDomain; no code runs in the AppDomain unless you explicitly have a thread call code in the AppDomain.

Now to create an instance of an object in the new AppDomain, we must first load an assembly into the new AppDomain and then construct an instance of a type defined in this assembly. This is precisely what the call to **AppDomain**’s public, instance **CreateInstanceAndUnwrap** method does. When calling **CreateInstanceAndUnwrap**, I pass two arguments: a **String** identifying the assembly I want loaded into the new AppDomain (referenced by the **ad2** variable) and another **String** identifying the name of the type that I want to construct an instance of. Internally, **CreateInstanceAndUnwrap** causes the calling thread to transition from the current AppDomain into the new AppDomain. Now, the thread (which is inside the call to **CreateInstanceAndUnwrap**) loads the specified assembly into the new AppDomain and then scans the assembly’s type definition metadata table, looking for the specified type (“MarshalByRefType”). After the type is found, the thread calls the **MarshalByRefType**’s parameterless constructor. Now the thread transitions back to the default AppDomain so that **CreateInstanceAndUnwrap** can return a reference to the new **MarshalByRefType** object.

> **Note** There are overloaded versions of **CreateInstanceAndUnwrap** that allow you to call a type’s constructor passing in arguments.

While this sounds all fine and good, there is a problem: the CLR cannot allow a variable (root) living in one AppDomain to reference an object created in another AppDomain. If **CreateInstanceAndUnwrap** simply returned the reference to the object, isolation would be broken, and isolation is the whole purpose of AppDomains! So just before **CreateInstanceAndUnwrap** returns the object reference, it performs some additional logic.
