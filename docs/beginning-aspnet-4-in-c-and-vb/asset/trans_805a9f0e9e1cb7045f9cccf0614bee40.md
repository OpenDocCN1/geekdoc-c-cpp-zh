

必须调用它。要取消事务（并且不向队列写入任何消息），必须调用 `Abort()` 方法，正如你在 `catch` 块中所看到的那样：

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

## 使用 WCF 进行消息队列

第 43 章“Windows Communication Foundation”介绍了 WCF 的架构和核心特性。使用 WCF，你可以配置一个利用 Windows 消息队列架构的消息队列绑定。这样，WCF 为消息队列提供了一个抽象层。图 46-14 用一张简单的图解释了该架构。客户端应用程序调用 WCF 代理的方法，将消息发送到队列。消息由代理创建。对于客户端开发人员来说，无需知道消息被发送到了队列中。客户端开发人员只需调用代理的方法即可。代理抽象了对 `System.Messaging` 命名空间中类的处理，并将消息发送到队列。服务端的 MSMQ 侦听通道从队列中读取消息，将其转换为方法调用，并使用服务来调用这些方法。

![](img/d7d2ffa0a76feaab821930e95daace93_1439_0.png)

接下来，课程订购（Course Ordering）应用程序将从 WCF 的角度转换为使用消息队列。在这个解决方案中，之前的三个项目被修改，并新增了一个包含 WCF 服务契约的程序集：

-   组件库（`CourseOrder`）包含在线路上发送的消息的实体类。这些实体类被修改，以满足 WCF 序列化的数据契约。
-   新增了一个库（`CourseOrderService`），用于定义服务提供的契约。
-   WPF 发送方应用程序（`CourseOrderSender`）被修改，不再直接发送消息，而是调用 WCF 代理的方法。
-   WPF 接收方应用程序（`CourseOrderReceiver`）被修改，使用实现该契约的 WCF 服务。

## 带有数据契约的实体类

在库 `CourseOrder` 中，`Course`、`Customer` 和 `CourseOrder` 类被修改，通过 `[DataContract]` 和 `[DataMember]` 特性应用数据契约。要使用这些特性，你需要引用程序集 `System.Runtime.Serialization` 并导入命名空间 `System.Runtime.Serialization`：

序列化：

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

*代码片段 CourseOrder/Course.cs*

`Customer` 类也需要数据契约特性：

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

*代码片段 CourseOrder/Customer.cs*

对于 `CourseOrder` 类，不仅添加了数据契约特性，还重写了 `ToString()` 方法，以便为这些对象提供默认的字符串表示形式：

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
*代码片段 CourseOrder/CourseOrder.cs*

## WCF 服务契约

要使用 WCF 服务契约提供服务，请添加一个名为 `CourseOrderServiceContract` 的 WCF 服务库。该契约由接口 `ICourseOrderService` 定义。此契约需要 `[ServiceContract]` 特性。如果希望限制此接口只能用于消息队列，可以应用 `[DeliveryRequirements]` 特性并指定 `QueuedDeliveryRequirements` 属性。枚举 `QueuedDeliveryRequirementMode` 的可能值为 `Required`、`Allowed` 和 `NotAllowed`。服务提供 `AddCourseOrder()` 方法。消息队列使用的方法只能具有输入参数。因为发送方和接收方可以独立运行，所以发送方无法期望立即得到结果。使用 `[OperationContract]` 特性，并设置 `IsOneWay` 属性。此操作的调用者不会等待服务的应答：

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
*代码片段 CourseOrderServiceContract/ICourseOrderService.cs*

> 你可以使用确认队列和响应队列来获取客户端的应答。

## WCF 消息接收应用程序

WPF 应用程序 `CourseOrderReceiver` 现在被修改为实现 WCF 服务并接收消息。需要引用程序集 `System.ServiceModel` 和 WCF 契约程序集 `CourseOrderServiceContract`。

类 `CourseOrderService` 实现了接口 `ICourseOrderService`。在实现中，会触发 `CourseOrderAdded` 事件。WPF 应用程序将注册到此事件以接收 `CourseOrder` 对象。

由于 WPF 控件绑定到单个线程，因此通过 `[ServiceBehavior]` 特性设置 `UseSynchronizationContext` 属性。这是 WCF 运行时的一项功能，用于将方法调用的执行传递给由 WPF 应用程序的同步上下文定义的线程：

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

*代码片段 CourseOrderReceiver/CourseOrderReceiverWindow.xaml.cs*

XAML 代码中的 WPF 元素现在使用数据绑定。`ListBox` 绑定到数据上下文，单项控件绑定到数据上下文当前项的属性：

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

*代码片段 CourseOrderReceiver/CourseOrderReceiverWindow.xaml*

应用程序配置文件定义了 `netMsmqBinding`。为了实现可靠的消息传递，需要使用事务性队列。若要接收和发送消息到非事务性队列，必须将 `exactlyOnce` 属性设置为 `false`。

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
```

