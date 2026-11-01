```
```csharp
public override string ToString()
{
    return String.Format("{Course Order ({0})}", Customer.Company);
}
```
*code snippet CourseOrder/CourseOrder.cs*
```

# WCF Service Contract

To offer the service with a WCF service contract, add a WCF service library with the name CourseOrderServiceContract. The contract is defined by the interface I CourseOrderService. This contract needs the attribute [ServiceContract]. If you want to restrict using this interface only with message queues, you can apply the [DeliveryRequirements] attribute and assign the property QueuedDeliveryRequirements. Possible values of the enumeration QueuedDeliveryRequirementMode are Required, Allowed, and NotAllowed. The method AddCourseOrder() is offered by the service. Methods used by Message Queuing can only have input parameters. Because the sender and receiver can run independent of each other, the sender cannot expect an immediate result. With the attribute [OperationContract], the IsOneWay property is set. The caller of this operation does not wait for an answer from the service:

```
```csharp
using System.ServiceModel;

namespace Wrox.ProCSharp.Messaging
{
    [ServiceContract]
    [DeliveryRequirements(
        QueuedDeliveryRequirements=QueuedDeliveryRequirementMode.Required)]
    public interface I CourseOrderService
    {
        [OperationContract(IsOneWay = true)]
        void AddCourseOrder(CourseOrder courseOrder);
    }
}
```
*code snippet CourseOrderServiceContract/ICourseOrderService.cs*
```

> You can use acknowledgment and response queues to get answers to the client.

# WCF Message Receiver Application

The WPF application CourseOrderReceiver is now modified to implement the WCF service and receive the messages. References to the assembly System.ServiceModel and the WCF contract assembly CourseOrderServiceContract are required.

The class CourseOrderService implements the interface I CourseOrderService. With the implementation, the event CourseOrderAdded is fired. The WPF application will register to this event to receive CourseOrder objects.

Because WPF controls are bound to a single thread, the property UseSynchronizationContext is set with the [ServiceBehavior] attribute. This is a feature of the WCF runtime to pass the method call invocation to the thread that is defined by the synchronization context of the WPF application:

```
```csharp
using System.ServiceModel;

namespace Wrox.ProCSharp.Messaging
{
    [ServiceBehavior(UseSynchronizationContext=true)]
```
```