```
```csharp
// Instances cannot be marshaled across AppDomain boundaries
// [Serializable]
public sealed class NonMarshalableType : Object {
    public NonMarshalableType() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
    }
}
```
```

If you build and run the Ch22-1-AppDomains application, you get the following output.

```
```text
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
```

Now, I will discuss what this code and the CLR are doing.

Inside the *Marshalling* method, I first get a reference to an AppDomain object that identifies the AppDomain the calling thread is currently executing in. In Windows, a thread is always created in the context of one process, and the thread lives its entire lifetime in that process. However, a one-to-one correspondence doesn't exist between threads and AppDomains. AppDomains are a CLR feature; Windows knows nothing about AppDomains. Because multiple AppDomains can be in a single Windows process, a thread can execute code in one AppDomain and then execute code in another AppDomain. From the CLR's perspective, a thread is executing code in one AppDomain at a time. A thread can ask the CLR what AppDomain it is currently executing in by calling System.Threading.Thread's static *GetDomain* method. The thread could also query System.AppDomain's static, read-only *CurrentDomain* property to get the same information.