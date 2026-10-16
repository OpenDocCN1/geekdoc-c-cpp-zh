```
namespace WebSocketsSample
{
    [ServiceContract]
    public interface IDemoCallback
    {
        [OperationContract(IsOneWay = true)]
        Task SendMessage(string message);
    }
    [ServiceContract(CallbackContract = typeof(IDemoCallback))]
    public interface IDemoService
    {
        [OperationContract]
        void StartSendingMessages();
    }
}
```

The implementation of the service is done in the DemoService class. Within StartSendingMessages, the callback interface to go back to the client is retrieved with OperationContext.Current.GetCallbackChannel. When the client invokes the method, it returns immediately as soon as the first time the SendMessage method is invoked. The thread is not blocked until the SendMessage method completes. With await, a thread just comes back to the StartSendingMessages when the SendMessage is completed. Then a delay of 1 second occurs before the client receives another message. In case the communication channel is closed the while loop exits (code file

```
WebSocketsSample/WebSocketsSample/DemoService.svc.cs:
```

```
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.Threading.Tasks;

namespace WebSocketsSample
{
    public class DemoService : IDemoService
    {
        public async Task StartSendingMessages()
        {
            IDemoCallback callback =
OperationContext.Current.GetCallbackChannel<IDemoCallback>();

            int loop = 0;
            while ((callback as IChannel).State ==
CommunicationState.Opened)
            {
                await callback.SendMessage($"Hello from the server {loop++}");
                await Task.Delay(1000);
            }
        }
    }
}
```

The client application is created as a console application. Because metadata is available with the service, adding a service reference creates a proxy class that can be used to call the service and also to implement the callback interface. Adding the service reference not only creates the proxy class, but also adds the netHttpBinding to the configuration file