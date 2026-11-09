
![](img/3f2c86949cdef7e2f9e27c37c607b28e_554_0.png)

FIGURE 22-1 A single Windows process hosting the CLR and two AppDomains.

In addition, each AppDomain has some assemblies loaded into it. AppDomain #1 (the default AppDomain) has three assemblies: MyApp.exe, TypeLib.dll, and System.dll. AppDomain #2 has two assemblies loaded into it: Winellect.dll and System.dll.

You'll notice that the System.dll assembly has been loaded into both AppDomains. If both AppDomains are using a single type from System.dll, both AppDomains will have a type object for the same type allocated in each loader heap; the memory for the type object is not shared by all of the AppDomains. Furthermore, as code in an AppDomain calls methods defined by a type, the method's Intermediate Language (IL) code is JIT-compiled, and the resulting native code is associated with each AppDomain; the code for the method is not shared by all AppDomains that call it.

Not sharing the memory for the type objects or native code is wasteful. However, the whole purpose of AppDomains is to provide isolation; the CLR needs to be able to unload an AppDomain and free up all of its resources without adversely affecting any other AppDomain. Replicating the CLR data structures ensures that this is possible. It also ensures that a type used by multiple AppDomains has a set of static fields for each AppDomain.

Some assemblies are expected to be used by several AppDomains. The best example is MSCorLib.dll.

```csharp
Console.WriteLine("Type={0}", mbrt.GetType());  // The CLR lies about the type

// Prove that we got a reference to a proxy object
Console.WriteLine("Is proxy={0}", RemotingServices.IsTransparentProxy(mbrt));

// This looks like we’re calling a method on MarshalByRefType but, we’re not.
// We’re calling a method on the proxy type. The proxy transitions the thread
// to the AppDomain owning the object and calls this method on the real object.
mbrt.SomeMethod();

// Unload the new AppDomain
AppDomain.Unload(ad2);
// mbrt refers to a valid proxy object; the proxy object refers to an invalid AppDomain

try {
    // We’re calling a method on the proxy type. The AD is invalid, exception is thrown
    mbrt.SomeMethod();
    Console.WriteLine("Successful call.");
}
catch (AppDomainUnloadedException) {
    Console.WriteLine("Failed call.");
}

// *** DEMO 2: Cross-AppDomain Communication using Marshal-by-Value ***
Console.WriteLine("{0} #2", Environment.NewLine);

// Create new AppDomain (security and configuration match current AppDomain)
ad2 = AppDomain.CreateDomain("AD #2", null, null);

// Load our assembly into the new AppDomain, construct an object, marshal
// it back to our AD (we really get a reference to a proxy)
mbrt = (MarshalByRefType)
    ad2.CreateInstanceAndUnwrap(eAssembly, "MarshalByRefType");

// The object’s method returns a COPY of the returned object;
// the object is marshaled by value (not by reference).
MarshalByValType mbvt = mbrt.MethodWithReturn();

// Prove that we did NOT get a reference to a proxy object
Console.WriteLine("Is proxy={0}", RemotingServices.IsTransparentProxy(mbvt));

// This looks like we’re calling a method on MarshalByValType and we are.
Console.WriteLine("Returned object created " + mbvt.ToString());

// Unload the new AppDomain
AppDomain.Unload(ad2);
// mbvt refers to valid object; unloading the AppDomain has no impact.

try {
    // We’re calling a method on an object; no exception is thrown
    Console.WriteLine("Returned object created " + mbvt.ToString());
    Console.WriteLine("Successful call.");
}
```

```csharp
public MarshalByValType() {
    Console.WriteLine("{0} ctor running in {1}, Created on {2:D}",
        this.GetType().ToString(),
        Thread.GetDomain().FriendlyName,
        m_creationTime);
}

public override String ToString() {
    return m_creationTime.ToLongDateString();
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

```text
Default AppDomain's friendly name: Ch22-1-AppDomains.exe
Main assembly: Ch22-1-AppDomains, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null

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
Returned object created Saturday, June 23, 2012
Returned object created Saturday, June 23, 2012
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

Inside the `Marshalling` method, I first get a reference to an `AppDomain` object that identifies the `AppDomain` the calling thread is currently executing in. In Windows, a thread is always created in the context of one process, and the thread lives its entire lifetime in that process. However, a one-to-one correspondence doesn’t exist between threads and `AppDomains`. `AppDomains` are a CLR feature; Windows knows nothing about `AppDomains`. Since multiple `AppDomains` can be in a single Windows process, a thread can execute code in one `AppDomain` and then execute code in another `AppDomain`. From the CLR’s perspective, a thread is executing code in one `AppDomain` at a time. A thread can ask the CLR what `AppDomain` it is currently executing in by calling `System.Threading.Thread`’s static `GetDomain` method. The thread could also query `System.AppDomain`’s static, read-only `CurrentDomain` property to get the same information.

When an `AppDomain` is created, it can be assigned a friendly name. A friendly name is just a `String` that you can use to identify an `AppDomain`. This is typically useful in debugging scenarios. Since the CLR creates the default `AppDomain` before any of your code can run, the CLR uses the executable file’s file name as the default `AppDomain`’s friendly name. My `Marshalling` method queries the default `AppDomain`’s friendly name by using `System.AppDomain`’s read-only `FriendlyName` property.

Next, my `Marshalling` method queries the strong-name identity of the assembly (loaded into the default `AppDomain`) that defines the entry point method `Main` that calls `Marshalling`. This assembly defines several types: `Program`, `MarshalByRefType`, `MarshalByValType`, and `NonMarshalableType`. At this point, we’re ready to look at the three types that are all pretty similar to each other.

## Demo #1: Cross-AppDomain Communication that Uses Marshal-by-Reference

In Demo #1, `System.AppDomain`’s static `CreateDomain` method is called, instructing the CLR to create a new `AppDomain` in the same Windows process. The `AppDomain` type actually offers several overloads of the `CreateDomain` method; I encourage you to study them and select the version that is most appropriate when you are writing code to create a new `AppDomain`. The version of `CreateDomain` that I call accepts three arguments:

- **A String identifying the friendly name I want assigned to the new AppDomain** — I’m passing in "AD #2" here.
- **A System.Security.Policy.Evidence identifying the evidence that the CLR should use to calculate the AppDomain’s permission set** — I’m passing `null` here so that the new `AppDomain` will inherit the same permission set as the `AppDomain` creating it. Usually, if you want to create a security boundary around code in an `AppDomain`, you’d construct a `System.Security.PermissionSet` object, add the desired permission objects to it (instances of types that implement the `IPermission` interface), and then pass the resulting
