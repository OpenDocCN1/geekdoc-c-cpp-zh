| QUEUE TYPE | SYNTAX |
|---|---|
| Public queue | MachineName\QueueName |
| Private queue | MachineName\Private$\QueueName |
| Journal queue | MachineName\QueueName\Journal$ |
| Machine journal queue | MachineName\Journal$ |
| Machine dead-letter queue | MachineName\DeadLetter$ |
| Machine transactional dead-letter queue | MachineName\XactDeadLetter$ |

When you use the pathname to open public queues, it is necessary to pass the machine name. If the machine name is not known, the format name can be used instead. The pathname for private queues can be used only on the local system. The format name must be used to access private queues remotely.

# Format Name

Instead of the pathname, you can use the format name to open a queue. The format name is used for searching the queue in the Active Directory to get the host where the queue is located. In a disconnected environment where the queue cannot be reached at the time the message is sent, it is necessary to use the format name:

```
MessageQueue queue = new MessageQueue(
    "@FormatName:PUBLIC=C09816AFF-5608-4c5d-B892-6975BA5151FF*");
```

The format name has some different uses. It can be used to open private queues and to specify a protocol that should be used:

+   - To access a private queue, the string that has to be passed to the constructor is FormatName:PRIVATE\MachineGUID\QueueNumber. The queue number for private queues is generated when the queue is created. You can see the queue numbers in the <windows>\System32\msmq\storage\logs directory.
+   - With FormatName:DIRECT=Protocol:MachineAddress\QueueName, you can specify the protocol that should be used to send the message. The HTTP protocol is supported since Message Queuing 3.0.
+   - FormatName:DIRECT=OS:MachineName\QueueName is another way to specify a queue using the format name. This way you don't have to specify the protocol but still can use the machine name with the format name.

# Sending a Message

You can use the Send method of the MessageQueue class to send a message to the queue. The object passed as an argument of the Send() method is serialized to the associated queue. The Send() method is overloaded so that a label and a MessageQueueTransaction object can be passed. Transactional behavior of Message Queuing is discussed later.

The code example first checks if the queue exists. If it doesn't exist, a queue is created. Then the queue is opened and the message Sample Message is sent to the queue using the Send() method.

The pathname specifies a dot (just like a period) for the server name, which is the local system. Pathnames to private queues work only locally:

```
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {
        static void Main()
        {
```