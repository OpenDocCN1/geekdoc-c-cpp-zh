| SERVICEBEHAVIOR PROPERTY | DESCRIPTION |
|---|---|
| ConcurrencyMode | Because stateful objects can be used by multiple clients (or multiple threads of a single client), you must pay attention to concurrency issues with such object types. If the property ConcurrencyMode is set to Multiple, multiple threads can access the object, and you must deal with synchronization. If you set the option to Single, only one thread accesses the object at a time. Here, you don't have to do synchronization; however, scalability problems can occur with a higher number of clients. The value Reentrant means that only a thread coming back from a callout might access the object. For stateless objects, this setting has no meaning, because new objects are instantiated with every method call and thus no state is shared. |
| UseSynchronizationContext | With Windows Forms and WPF, members of controls can be invoked only from the creator thread. If the service is hosted in a Windows application, and the service methods invoke control members, set the UseSynchronizationContext to true. This way, the service runs in a thread defined by the SynchronizationContext. |
| IncludeExceptionDetailInFaults | With .NET, errors show up as exceptions. SOAP defines that a SOAP fault is returned to the client in case the server has a problem. For security reasons, it's not a good idea to return details of server-side exceptions to the client. Thus, by default, exceptions are converted to unknown faults. To return specific faults, throw an exception of type FaultException. For debugging purposes, it can be helpful to return the real exception information. This is the case when changing the setting of IncludeExceptionDetailInFaults to true. Here a FaultException<Detail> is thrown where the original exception contains the detail information. |
| MaxItemsInObjectGraph | With the property MaxItemsInObjectGraph, you can limit the number of objects that are serialized. The default limitation might be too low if you serialize a tree of objects. |
| ValidateMustUnderstand | The property ValidateMustUnderstand set to true means that the SOAP headers must be understood (which is the default). |

To demonstrate a service behavior, the interface IStateService defines a service contract with two operations to set and get state. With a stateful service contract, a session is needed. That's why the SessionMode property of the service contract is set to SessionMode.Required. The service contract also defines methods to initiate and close the session by applying the IsInitiating and IsTerminating properties to the operation contract:

```
[ServiceContract(SessionMode=SessionMode.Required)]
public interface IStateService
{
    [OperationContract(IsInitiating=true)]
    void Init(int i);

    [OperationContract]
    void SetState(int i);

    [OperationContract]
    int GetState();
}
```