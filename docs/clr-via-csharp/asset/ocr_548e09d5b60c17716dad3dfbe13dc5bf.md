```
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
    ad2.CreateInstanceAndUnwrap(exassembly, "MarshalByRefType");

// The object's method returns a non-marshallable object; exception
NonMarshallableType nmt = mbrt.MethodArgAndReturn(callingDomainName);
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
```
```