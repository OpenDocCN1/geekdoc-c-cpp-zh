
must be called. To cancel a transaction (and have no messages written to the queue), the Abort() method must be called, as you can see within the catch block:

```csharp
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {
        static void Main()
        {
            if (!MessageQueue.Exists(@"\\.\MyTransactionalQueue"))
            {
                MessageQueue.Create(@"\\.\MyTransactionalQueue", true);
            }

            var queue = new MessageQueue(@"\\.\MyTransactionalQueue");
            var transaction = new MessageQueueTransaction();

            try
            {
                transaction.Begin();
                queue.Send("a", transaction);
                queue.Send("b", transaction);
                queue.Send("c", transaction);
                transaction.Commit();
            }
            catch
            {
                transaction.Abort();
            }
        }
    }
}
```

## MESSAGE QUEUING WITH WCF

Chapter 43, “Windows Communication Foundation,” covers the architecture and core features of WCF. With WCF, you can configure a Message Queuing binding that makes use of the Windows Message Queuing architecture. With this, WCF offers an abstraction layer to Message Queuing. Figure 46-14 explains the architecture using a simple picture. The client application invokes a method of a WCF proxy to send a message to the queue. The message is created by the proxy. For the client developer, there’s no need to know that a message is sent to the queue. The client developer just invokes a method of the proxy. The proxy abstracts dealing with the classes from the System.Messaging namespace and sends a message to the queue. The MSMQ listener channel on the service side reads messages from the queue, converts them to method calls, and invokes the method calls with the service.

![](img/d7d2ffa0a76feaab821930e95daace93_1439_0.png)

Next, the Course Ordering application gets converted to make use of Message Queuing from a WCF viewpoint. With this solution, the three projects done earlier are modified, and one more assembly is added that includes the contract of the WCF service:

- The component library (CourseOrder) includes entity classes for the messages that are sent across the wire. These entity classes are modified to fulfill the data contract for serialization with WCF.
- A new library is added (CourseOrderService) that defines the contract offered by the service.
- The WPF sender application (CourseOrderSender) is modified to not send messages but instead invoke methods of a WCF proxy.
- The WPF receiving application (CourseOrderReceiver) is modified to make use of the WCF service that implements the contract.

## Entity Classes with a Data Contract

In the library CourseOrder, the classes Course, Customer, and CourseOrder are modified to apply the data contract with the attributes [DataContract] and [DataMember]. For using these attributes, you have to reference the assembly System.Runtime.Serialization and import the namespace System.Runtime.Serialization:

Serialization:

```csharp
using System.Runtime.Serialization;

namespace Wrox.ProCSharp.Messaging
{
    [DataContract]
    public class Course
    {
        [DataMember]
        public string Title { get; set; }
    }
}
```

code snippet CourseOrder/Course.cs

The Customer class requires the data contract attributes as well:

```csharp
[DataContract]
public class Customer
{
    [DataMember]
    public string Company { get; set; }

    [DataMember]
    public string Contact { get; set; }
}
```

code snippet CourseOrder/Customer.cs

With the class CourseOrder, not only the data contract attributes are added, but an override of the ToString() method as well to have a default string representation of these objects:

```csharp
[DataContract]
public class CourseOrder
{
    [DataMember]
    public Customer Customer { get; set; }

    [DataMember]
    public Course Course { get; set; }
```

```csharp
public override string ToString()
{
    return String.Format("Course Order ({0})", Customer.Company);
}
```
*code snippet CourseOrder/CourseOrder.cs*

## WCF Service Contract

To offer the service with a WCF service contract, add a WCF service library with the name CourseOrderServiceContract. The contract is defined by the interface ICourseOrderService. This contract needs the attribute [ServiceContract]. If you want to restrict using this interface only with message queues, you can apply the [DeliveryRequirements] attribute and assign the property QueuedDeliveryRequirements. Possible values of the enumeration QueuedDeliveryRequirementMode are Required, Allowed, and NotAllowed. The method AddCourseOrder() is offered by the service. Methods used by Message Queuing can only have input parameters. Because the sender and receiver can run independent of each other, the sender cannot expect an immediate result. With the attribute [OperationContract], the IsOneWay property is set. The caller of this operation does not wait for an answer from the service:

```csharp
using System.ServiceModel;

namespace Wrox.ProCSharp.Messaging
{
    [ServiceContract]
    [DeliveryRequirements(
        QueuedDeliveryRequirements=QueuedDeliveryRequirementMode.Required)]
    public interface ICourseOrderService
    {
        [OperationContract(IsOneWay = true)]
        void AddCourseOrder(CourseOrder courseOrder);
    }
}
```
*code snippet CourseOrderServiceContract/ICourseOrderService.cs*

> You can use acknowledgment and response queues to get answers to the client.

## WCF Message Receiver Application

The WPF application CourseOrderReceiver is now modified to implement the WCF service and receive the messages. References to the assembly System.ServiceModel and the WCF contract assembly CourseOrderServiceContract are required.

The class CourseOrderService implements the interface ICourseOrderService. With the implementation, the event CourseOrderAdded is fired. The WPF application will register to this event to receive CourseOrder objects.

Because WPF controls are bound to a single thread, the property UseSynchronizationContext is set with the [ServiceBehavior] attribute. This is a feature of the WCF runtime to pass the method call invocation to the thread that is defined by the synchronization context of the WPF application:

```csharp
using System.ServiceModel;

namespace Wrox.ProCSharp.Messaging
{
    [ServiceBehavior(UseSynchronizationContext=true)]
```

```csharp
CourseOrderService.CourseOrderAdded += (sender, e) =>
{
    courseOrders.Add(e.CourseOrder);
    buttonProcessOrder.IsEnabled = true;
}
var host = new ServiceHost(typeof(CourseOrderService));
try
{
    host.Open();
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
this.DataContext = courseOrders;
```

*code snippet CourseOrderReceiver/CourseOrderReceiverWindow.xaml.cs*

The WPF elements in the XAML code now make use of data binding. The ListBox is bound to the data context, and the single-item controls are bound to properties of the current item of the data context:

```xml
<ListBox Grid.Row="1" x:Name="listOrders" ItemsSource="{Binding}"
IsSynchronizedWithCurrentItem="true" />

<!-- ... -->

<TextBox x:Name="textCourse" Grid.Row="0" Grid.Column="1"
Text="{Binding Path=Course.Title}" />
<TextBox x:Name="textCompany" Grid.Row="1" Grid.Column="1"
Text="{Binding Path=Customer.Company}" />
<TextBox x:Name="textContact" Grid.Row="2" Grid.Column="1"
Text="{Binding Path=Customer.Contact}" />
```

*code snippet CourseOrderReceiver/CourseOrderReceiverWindow.xaml*

The application configuration file defines the netMsmqBinding. For reliable messaging, transactional queues are required. To receive and send messages to non-transactional queues, the exactlyOnce property must be set to false.

![](img/d7d2ffa0a76feaab821930e95daace93_1443_0.png)

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.serviceModel>
        <bindings>
            <netMsmqBinding>
                <binding name="NonTransactionalQueueBinding" exactlyOnce="false">
                    <security mode="None" />
                </binding>
            </netMsmqBinding>
        </bindings>
        <services>
            <service name="Wrox.ProCSharp.Messaging.CourseOrderService">
