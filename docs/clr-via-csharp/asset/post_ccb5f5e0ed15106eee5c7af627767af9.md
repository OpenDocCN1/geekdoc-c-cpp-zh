
You'll notice that the `MarshalByRefType` type is derived from a very special base class: `System.MarshalByRefObject`. When `CreateInstanceAndUnwrap` sees that it is marshalling an object whose type is derived from `MarshalByRefObject`, the CLR will marshal the object by reference across the AppDomain boundaries. Here is what it means to marshal an object by reference from one AppDomain (the source AppDomain where the object is really created) to another AppDomain (the destination AppDomain from where `CreateInstanceAndUnwrap` is called).

When a source AppDomain wants to send or return the reference of an object to a destination AppDomain, the CLR defines a proxy type in the destination AppDomain's loader heap. This proxy type is defined using the original type's metadata, and therefore, it looks exactly like the original type; it has all of the same instance members (properties, events, and methods). The instance fields are not part of the type, but I'll talk more about this in a moment. This new type does have some instance fields defined inside of it, but these fields are not identical to that of the original data type. Instead, these fields indicate which AppDomain "owns" the real object and how to find the real object in the owning AppDomain. (Internally, the proxy object uses a `GCHandle` instance that refers to the real object. The `GCHandle` type is discussed in Chapter 21, "Automatic Memory Management (Garbage Collection).")

Once this type is defined in the destination AppDomain, `CreateInstanceAndUnwrap` creates an instance of this proxy type, initializes its fields to identify the source AppDomain and the real object, and returns a reference to this proxy object to the destination AppDomain. In my Ch22-1-AppDomains application, the `mbrt` variable will be set to refer to this proxy. Notice that the object returned from `CreateInstanceAndUnwrap` is actually not an instance of the `MarshalByRefType` type. The CLR will usually not allow you to cast an object of one type to an incompatible type. However, in this situation, the CLR does allow the cast because this new type has the same instance members as defined on the original type. In fact, if you use the proxy object to call `GetType`, it actually lies to you and says that it is a `MarshalByRefType` object.

However, it is possible to prove that the object returned from `CreateInstanceAndUnwrap` is actually a reference to a proxy object. To do this, my Ch22-1-AppDomains application calls `System.Runtime.Remoting.RemotingServices`' public, static `IsTransparentProxy` method passing in the reference returned from `CreateInstanceAndUnwrap`. As you can see from the output, `IsTransparentProxy` returns `true`, indicating that the object is a proxy.

Now, my Ch22-1-AppDomains application uses the proxy to call the `SomeMethod` method. Since the `mbrt` variable refers to a proxy object, the proxy's implementation of this method is called. The proxy's implementation uses the information fields inside the proxy object to transition the calling thread from the default AppDomain to the new AppDomain. Any actions now performed by this thread run under the new AppDomain's security and configuration settings. Then, the thread uses the proxy object's `GCHandle` field to find the real object in the new AppDomain, and then it uses the real object to call the real `SomeMethod` method.

When the default AppDomain attempts to use the proxy object to call the **SomeMethod** method, the proxy's implementation of this method is called. The proxy's implementation determines that the AppDomain that contained the real object has been unloaded, and the proxy's **SomeMethod** method throws an **AppDomainUnloadedException** to let the caller know that the operation cannot complete.

Wow! The CLR team at Microsoft had to do a lot of work to ensure AppDomain isolation, but it is important work because these features are used heavily and are being used more and more by developers every day. Obviously, accessing objects across AppDomain boundaries by using marshal-by-reference semantics has some performance costs associated with it, so you typically want to keep the use of this feature to a minimum.

I promised you that I'd talk a little more about instance fields. A type derived from **MarshalByRefObject** can define instance fields. However, these instance fields are not defined as being part of the proxy type and are not contained inside a proxy object. When you write code that reads from or writes to an instance field of a type derived from **MarshalByRefObject**, the JIT compiler emits code that uses the proxy object (to find the real AppDomain object) by calling **System.Object's FieldGetter** or **FieldSetter** methods, respectively. These methods are private and undocumented; they are basically methods that use reflection to get and set the value in a field. So although you can access fields of a type derived from **MarshalByRefObject**, the performance is particularly bad because the CLR really ends up calling methods to perform the field access. In fact, the performance is bad even if the object that you are accessing is in your own AppDomain.<sup>3</sup>

### The Performance of Accessing Instance Fields

To demonstrate the significance of this performance hit, I wrote the following code:

```csharp
private sealed class NonMBRO : Object                { public Int32 x; }
private sealed class MBRO    : MarshalByRefObject    { public Int32 x; }

private static void FieldAccessTiming() {
    const Int32 count = 10000000;
    NonMBRO nonMbro = new NonMBRO();
    MBRO    mbro    = new MBRO();

    Int64 time = Stopwatch.GetTimestamp();
    for (Int32 c = 0; c < count; c++) nonMbro.x++;
    Console.WriteLine("{0:N0}", Stopwatch.GetTimestamp() - time);   // 134,174

    time = Stopwatch.GetTimestamp();
    for (Int32 c = 0; c < count; c++) mbro.x++;
    Console.WriteLine("{0:N0}", Stopwatch.GetTimestamp() - time);   // 1,533,886
}
```

<sup>3</sup> If the CLR required that all fields be private (which is recommended for good data encapsulation), then the **FieldGetter** and **FieldSetter** methods wouldn't have to exist and accessing fields from methods could always have been direct, avoiding any performance penalty.

When I ran this code, it took 134,174 ticks to access the instance field of a **NonMBRO** class that is derived from **Object**, and it took 1,533,886 ticks to access the instance field of an **MBRO** class that is derived from **MarshalByRefObject**. So, accessing an instance field of a class derived from **MarshalByRefObject** takes more than 11 times longer!

From a usability standpoint, a type derived from **MarshalByRefObject** should really avoid defining any static members. The reason is that static members are always accessed in the context of the calling AppDomain. No AppDomain transition can occur because a proxy object contains the information identifying which AppDomain to transition to, but there is no proxy object when calling a static member. Having a type's static members execute in one AppDomain while instance members execute in another AppDomain would make a very awkward programming model.

Since there are no roots in the second AppDomain, the original object referred to by the proxy could be garbage collected. Of course, this is not ideal. On the other hand, if the original object is held in memory indefinitely, then the proxy could go away and the original object would still live; this is also not ideal. The CLR solves this problem by using a *lease manager*. When a proxy for an object is created, the CLR keeps the object alive for 5 minutes. If no calls have been made through the proxy after 5 minutes, then the object is *deactivated* and will have its memory freed at the next garbage collection. After each call into the object, the lease manager renews the object's lease so that it is guaranteed to remain in memory for another 2 minutes before being deactivated. If an application attempts to call into an object through a proxy after the object's lease has expired, the CLR throws a **System.Runtime.Remoting.RemotingException**.

It is possible to override the default lease times of 5 minutes and 2 minutes by overriding **MarshalByRefObject**'s virtual **InitializeLifetimeService** method. For more information, see the section titled "Lifetime Leases" in the .NET Framework SDK documentation.

## Demo #2: Cross-AppDomain Communication Using Marshal-by-Value

Demo #2 is very similar to Demo #1. Again, another AppDomain is created exactly as Demo #1 did it. Then, **CreateInstanceAndUnwrap** is called to load the same assembly into the new AppDomain and create an instance of a **MarshalByRefType** object in this new AppDomain. Next, the CLR creates a proxy to the object, and the **mbrt** variable (in the default AppDomain) is initialized referring to the proxy. Now, using the proxy, I call **MethodWithReturn**. This method, which takes no arguments, will execute in the new AppDomain to create an instance of the **MarshalByValType** type before returning a reference to the object to the default AppDomain.
