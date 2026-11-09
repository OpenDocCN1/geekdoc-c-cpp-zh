implementation data of the inherited class. Because of this shortcoming, it is sometimes said that COM does not support implementation inheritance.

Two types of implementation inheritance are provided for in COM+: containment and aggregation. Containment inheritance is implemented by having a COM+ class reimplement the methods of the inherited class. These implementations would simply redirect calls to the contained COM+ class.

# Aggregation

Aggregation inheritance enables clients to call inherited methods directly. One disadvantage of this method is that the aggregated object's IUnknown methods must be integrated with the aggregator's IUnknown methods. Another disadvantage is that only in-process servers can implement aggregation inheritance.

Aggregation inheritance is accomplished using the IClassFactory interface. Each COM+ class, whether it can be aggregated or not, must implement a class factory object that implements the IClassFactory interface. The class factory object is responsible for creating the COM+ class. Listing 9.9 shows the definition of the IClassFactory interface.

```
**LISTING 9.9** Definition of the IClassFactory Interface

```cpp
interface IClassFactory : IUnknown
{
    HRESULT CreateInstance(IUnknown * punk,
        REFIID iid, void ** ppvobj);
    HRESULT LockServer(BOOL fLock);
}
```
```

All COM+ objects are created by calling this IClassFactory::CreateInstance() method. If the first parameter of the call to the IClassFactory::CreateInstance() method is NULL, the object being created will not be aggregated. If this same parameter is a pointer to an IUnknown, the object being created will be aggregated and delegate all calls to its IUnknown methods to the alternate IUnknown interface.

Aggregation is a very powerful feature of COM+ that is rarely used. ATL enables you to take advantage of aggregation by writing two proxy code. In aggregation inheritance, we say that an aggregator inherits the implementation of an aggregate. You’ll need to know this to understand the next ATL code listings.

ATL classes can serve as aggregates as long as they do not define the DECLARE_NOT_AGGREGABLE macro. This makes coding aggregates easy because it requires no additional code in the aggregate. Listing 9.10 shows the class that I will be using as the aggregate. Again, no additional coding is needed to support aggregation in the aggregate.