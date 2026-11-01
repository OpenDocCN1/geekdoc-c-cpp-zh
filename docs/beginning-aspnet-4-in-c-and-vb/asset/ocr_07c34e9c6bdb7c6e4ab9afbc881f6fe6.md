A message formatter implements the interface `IMessageFormatter`. Three message formatters are available with the namespace `System.Messaging`:

+   - The `XmlMessageFormatter` is the default formatter. It serializes objects using XML. See Chapter 33, “Manipulating XML,” for more on XML formatting.
+   - With the `BinaryMessageFormatter`, messages are serialized in a binary format. These messages are shorter than the messages formatted using XML.
+   - The `ActiveXMessageFormatter` is a binary formatter so that messages can be read or written with COM objects. Using this formatter, it is possible to write a message to the queue with a .NET class and to read the message from the queue with a COM object or vice versa.

The sample message shown in Figure 46-8 with XML is formatted with the `BinaryMessageFormatter` in Figure 46-9.

![](bbox=[0.52, 0.15, 0.9, 0.6])

FIGURE 46-9

# Sending Complex Messages

Instead of passing strings, it is possible to pass objects to the `Send()` method of the `MessageQueue` class. The type of the class must fulfill some specific requirements, but they depend on the formatter.

For the binary formatter, the class must be serializable with the `[Serializable]` attribute. With the .NET runtime serialization, all fields are serialized (this includes private fields). Custom serialization can be defined by implementing the interface `ISerializable`. You can read more about the .NET runtime serialization in Chapter 29, “Manipulating Files and the Registry.”

XML serialization takes place with the XML formatter. With XML serialization, all public fields and properties are serialized. The XML serialization can be influenced by using attributes from the `System.Xml.Serialization` namespace. You can read more about XML serialization in Chapter 33.

# Receiving Messages

To read messages, again, you can use the `MessageQueue` class. With the `Receive()` method, a single message is read and removed from the queue. If messages are sent with different priorities, the message with the highest priority is read. Reading messages with the same priority may mean that the first message sent is not the first message read because the order of messages across the network is not guaranteed. For a guaranteed order, you should use transactional message queues.

In the following example, a message is read from the private queue `MyPrivateQueue`. Previously, a simple string was passed to the message. When you read a message using the `XmlMessageFormatter`, you have to pass the types of the objects that are read to the constructor of the formatter. In the example, the type `System.String` is passed to the argument array of the `XmlMessageFormatter` constructor. This constructor allows either a String array that contains the types as strings to be passed or a Type array.

The message is read with the `Receive()` method, and then the message body is written to the console:

```
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {

```