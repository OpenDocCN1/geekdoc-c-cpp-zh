```
~~~csharp
var ad = AppDomain.CreateDomain("AddIn");

var calc = (IBinaryOperation)ad.CreateInstanceFromAndUnwrap(
    "AddIn.dll",
    "Pythagorean"
);

Console.WriteLine(calc.Compute(3, 4));
~~~
```

In a more realistic extensible application, both the assembly name and type name of the add-in will be loaded from some kind of configuration store.

With this separation between host and add-in put in place, we also see that unloading the AddIn domain becomes very effective, causing the loaded add-in assembly to get unloaded properly. The only remains of loading the add-in will be the shared interface assembly, which belongs to our host’s circle of trust. In other words, it’s now possible to get rid of a misbehaving add-in altogether by unloading the corresponding domain. This point is proven in Figure 25.47.

![](bbox=[0.093, 0.489, 0.926, 0.736])

# ### The Managed Add-In Framework

Although .NET Remoting as a communication mechanism for distributed computing has been largely superseded by service-oriented architecture (SOA) patterns (using either classic web services in ASP.NET or the WCF stack), it still pays off in scenarios where the most basic form of cross-domain communication is required. In particular, add-ins typically require strong isolation properties, which can be realized using application domains, as we saw before.

Use of application domains doesn’t provide a silver bullet, though. Certain behaviors can still have fatal consequences, such as an out-of-memory, stack-overflow, or other exceptions that corrupt the process state. To provide protection against those kinds of misbehavior caused by an add-in, a separate add-in process is required.