One case is the first-class object characteristic of an interface. An object implementing an interface can be passed using the interface type. If the sole goal of passing such an object is to wrap a single method, a delegate is usually a better choice. In languages like Java that lack delegates, the only way to achieve this is by providing a single-method interface like Runnable. However, in .NET you can do better by declaring a delegate à la ThreadStart. You'll learn about delegates later, including how a delegate can wrap addition state thanks to closures.

Another case occurs when an interface is simply used as a marker to declare that a type supports some kind of usage. A good example is to communicate the capability to expose a class through a web service. Instead of using a zero-member marker interface, the use of custom attributes is often better and reduces clutter:

```
[WebService(/* parameters can be specified here */)]
class PaymentService /* rather than : IWebService */
{ ... }
```

The preceding example stems from the .NET 1.x days with classic web services supported in ASP.NET. In today's world, Windows Communication Foundation is preferred, which also uses attributes to denote things such as contracts, even on interfaces themselves:

```
[OperationContract]
public interface IPaymentService
{
    void TransferBalance(int from, int to, decimal amount);
}
```

# REENFORCING THE INTERFACES AS CONTRACTS PHILOSOPHY

Windows Communication Foundation (WCF) takes the idea of interfaces as contracts one step further and maps the idea onto a distributed setting of services. The idea is to separate the contract from implementations, allowing an interface to be shared across tiers as the single authoritative contract. Such exchange of contracts can be exposed through various formats as well, including WSDL and the Metadata Exchange specification for web services. Either way, what denotes the contract in the world of CLR services and clients is the interface, annotated with custom attributes to provide more parameterization of intent.

If an interface is to be implemented on an object to add some aspect or "ability" to it, the use of an interface is recommended. An example includes IDisposable, where it suffices to implement a single method to turn on the "ability of disposing."

# Contracts: Take Two

Because interfaces can be regarded as contracts between different parties, it's important to provide good documentation stating what the different members should do. A good