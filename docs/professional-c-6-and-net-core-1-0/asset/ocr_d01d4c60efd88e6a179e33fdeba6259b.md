a SOAP fault is returned to the client in case the server has a problem. For security reasons, it’s not a good idea to return details of server-side exceptions to the client. Thus by default, exceptions are converted to unknown faults. To return specific faults, throw an exception of type `FaultException`. For debugging purposes, it can be helpful to return the real exception information. This is the case when changing the setting of `IncludeExceptionDetailInFaults` to true. Here a `FaultException<TDetail>` is thrown where the original exception contains the detail information.

MaxItemsInObjectGraph

With the property `MaxItemsInObjectGraph`, you can limit the number of objects that are serialized. The default limitation might be too low if you serialize a tree of objects.

ValidateMustUnderstand

The property `ValidateMustUnderstand` set to true means that the SOAP headers must be understood (which is the default).

To demonstrate a service behavior, the interface `IStateService` defines a service contract with two operations to set and get state. With a stateful service contract, a session is needed. That’s why the `SessionMode` property of the service contract is set to `SessionMode.Required`. The service contract also defines methods to initiate and close the session by applying the `IsInitiating` and `IsTerminating` properties to the operation contract:

```
[ServiceContract(SessionMode=SessionMode.Required)]
public interface IStateService
{
    [OperationContract(IsInitiating=true)]
    void Init(int i);

    [OperationContract]
    void SetState(int i);
```