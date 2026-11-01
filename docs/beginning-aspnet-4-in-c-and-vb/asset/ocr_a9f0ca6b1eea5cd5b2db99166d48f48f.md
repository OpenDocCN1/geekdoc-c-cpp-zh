The class ProcessPersonRequestMessage is used with the service contract that is defined with the interface IProcessPerson:

```
[ServiceContract]
public interface IProcessPerson
{
    [OperationContract]
    public PersonResponseMessage ProcessPerson(
        ProcessPersonRequestMessage message);
}
```

Another contract that is important in regard to WCF services is the fault contract. This contract is discussed in the next section with Error Handling.

# SERVICE IMPLEMENTATION

The implementation of the service can be marked with the attribute ServiceBehavior, as shown with the class RoomReservationService:

```
[ServiceBehavior]
public class RoomReservationService: IRoomService
{
    public bool ReserveRoom(RoomReservation roomReservation)
    {
        // implementation
    }
}
```

The attribute ServiceBehavior is used to describe behavior as is offered by WCF services to intercept the code for required functionality, as shown in the following table.

| SERVICEBEHAVIOR PROPERTY | DESCRIPTION |
|---|---|
| TransactionAutoCompleteOn SessionClose | When the current session is finished without error, the transaction is automatically committed. This is similar to the AutoComplete attribute, which is discussed with Enterprise Services in Chapter 51 (this is a downloadable chapter). |
| TransactionIsolationLevel | To define the isolation level of the transaction within the service, the property TransactionIsolationLevel can be set to one value of the IsolationLevel enumeration. You can read information about transaction information levels in Chapter 23, "System.Transactions." |
| ReleaseServiceInstanceOn TransactionComplete | When the transaction is finished, the instance of the service is recycled. |
| AutomaticSessionShutdown | If the session should not be closed when the client closes the connection, you can set the property AutomaticSessionShutdown to false. By default, the session is closed. |
| InstanceContextMode | With the property InstanceContextMode, you can define whether stateful or stateless objects should be used. The default setting is InstanceContextMode.PerCall to create a new object with every method call. Other possible settings are PerSession and Single. With both of these settings, stateful objects are used. However, with PerSession a new object is created for every client. Single allows the same object to be shared with multiple clients. |