MyNewPublicQueue is created on the local host. To create a private queue, the pathname must include `Private$`; for example, `\\Private$\MyNewPrivateQueue`.

After the `Create()` method is invoked, properties of the queue can be changed. For example, using the `Label` property, the label of the queue is set to Demo Queue. The sample program writes the path of the queue and the format name to the console. The format name is automatically created with a UUID that can be used to access the queue without the name of the server:

```
```csharp
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {
        static void Main()
        {
            using (var queue = MessageQueue.Create(@".\\MyNewPublicQueue"))
            {
                queue.Label = "Demo Queue";
                Console.WriteLine("Queue created");
                Console.WriteLine("Path: {0}", queue.Path);
                Console.WriteLine("FormatName: {0}", queue.FormatName);
            }
        }
    }
}
```

*code snippet CreateMessageQueue/Program.cs*
```

> > Administrative privileges are required to create a queue. Usually, you cannot expect the user of your application to have administrative privileges. That's why queues usually are created with installation programs. Later in this chapter, you see how message queues can be created with the `MessageQueueInstaller` class.

# Finding a Queue

The pathname and the format name can be used to identify queues. To find queues, you must differentiate between public and private queues. Public queues are published in the Active Directory. For these queues, it is not necessary to know the system where they are located. Private queues can be found only if the name of the system where the queue is located is known.

You can find public queues in the Active Directory domain by searching for the queue’s label, category, or format name. You can also get all queues on a machine. The class `MessageQueue` has static methods to search for queues: `GetPublicQueuesByLabel()`, `GetPublicQueuesByCategory()`, and `GetPublicQueuesByMachine()`. The method `GetPublicQueues()` returns an array of all public queues in the domain:

```
```csharp
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {
```
```