
```csharp
public partial class Robot : UserControl
{
    /// <summary>
    /// Dictionary containing Peripheral and the option
    /// </summary>
    public Dictionary<Peripheral, string> Peripherals = new Dictionary<Peripheral, string>();

    /// <summary>
    /// The core method used to create different representations
    /// </summary>
    public void Create()
    {
        while (true)
        {
            // Create new Computer
            _computer = new Bitmap(Image.Computer);

            foreach (Peripheral peripheral in Peripherals.Keys)
            {
                if (peripheral == Peripheral.Processor)
                    AssembleCPU(Peripherals[peripheral]);

                if (peripheral == Peripheral.Monitor)
                    AssembleMonitor(Peripherals[peripheral]);

                if (peripheral == Peripheral.Speakers)
                    AssembleSpeakers(Peripherals[peripheral]);
            }

            AddToStore();
        }
    }
}
```

The class Peripheral is an enumeration as following:

```csharp
public enum Peripheral
{
    Processor,
    Monitor,
    Speakers
}
```

## Summary

In this chapter we have seen the usage of Builder pattern. The attachment contains the source code of the example we have discussed.

## 10. Chain of Responsibility Pattern

Chain of Responsibility is one among the 23 Design Patterns by Gang of Four. It is an interesting pattern and similar to Observer pattern. In this chapter we are exploring the Chain of Responsibility pattern.

I am using the same Challenge and Solution style for explaining this pattern.

### Challenge

You are working on an application in which the **Logic** class generates various messages. The messages are of two types.

- Normal Priority
- High Priority

The Normal Priority messages are to be processed by **Logger** class and High Priority messages by **Emailer** class.

You have to make the design in such a way that the **Logic** class need not think about right handler of the message. It will just send the message.

How the design will proceed?

### Definition

> GoF Definition: "Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it"

### Control Flow

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_40_0.png)

### Implementation

Following is the definition for Logic class:

```csharp
public class Logic
{
    public IReceiver Receiver;

    public void CreateMessage(Message message)
    {
        if (Receiver != null)
            Receiver.HandleMessage(message);
    }
}
```

We can see from the above code that the Logic class has a property of type IReceiver. On the CreateMessage method this Receiver is used to handle the message. So only one receiver is registered by the Logic class instance.

Following are the definitions of Message class and MessagePriority enumeration:

```csharp
public class Message
{
    public string Text;
    public MessagePriority Priority;
}
```

```csharp
public enum MessagePriority
{
    Normal,
    High
}
```

Following are the Receiver Interface and Implementation classes:

```csharp
public interface IReceiver
{
    bool HandleMessage(Message message);
}
```

```csharp
public class Logger : IReceiver
{
    private IReceiver _nextReceiver;

    public Logger(IReceiver nextReceiver)
    {
        _nextReceiver = nextReceiver;
    }

    public bool HandleMessage(Message message)
    {
        if (message.Priority == MessagePriority.Normal)
        {
            Trace.WriteLine(message.Text + " : Logger processed it!");
            return true;
        }
        else
        {
            if (_nextReceiver != null)
                _nextReceiver.HandleMessage(message);
        }

        return false;
    }
}
```

```csharp
public class Emailer : IReceiver
{
    private IReceiver _nextReceiver;

    public Emailer(IReceiver nextReceiver)
    {
        _nextReceiver = nextReceiver;
    }

    public bool HandleMessage(Message message)
    {
        if (message.Priority == MessagePriority.High)
        {
            Trace.WriteLine(message.Text + " : Emailer processed it!");
            return true;
        }
        else
        {
            if (_nextReceiver != null)
                _nextReceiver.HandleMessage(message);
        }

        return false;
    }
}
```

From the above code we can see that each receiver class checks the message priority and processes it. If the priority is not matching, it is sent to the next receiver in the chain.

Here each receiver takes care of passing the unprocessed message. The next receiver is stored through the constructor of each receiver.

The chain will be executed until:

- Message is processed
- Receiver chain exhausted

### Code Execution

The windows forms application attached can be used to test the control flow.

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_43_0.png)

Here the chain is built as following:

- Logic class holds the first receiver, which is Logger
- Logger class holds the next receiver, which is Emailer
- Emailer class has a null receiver denoting the end of the chain

Following code depicts the above chain creation:

```csharp
Logic logic = new Logic();
logic.Receiver = new Logger(new Emailer(null));
```

Note: Please note that the advantage of this pattern is decoupling of sender and receiver. The sender does not think about the right receiver. Instead it will pass the request and the appropriate receiver should process it. The above example can be written using a list of receivers in the Logic class with a Boolean property mentioning whether the message is processed or not.

### Comparing Observer and Chain of Responsibility

In the case of Observer pattern all the registered receivers will get the request. Each of the receivers is interested in processing it. But in chain of responsibility the request is passed until it is processed.

| Observer | Chain of Responsibility |
| --- | --- |
| All observers handles message | Only one receiver handles message |

### Summary

In this chapter we have explored Chain of Responsibility pattern with a C# example. The associated source code contains the example we discussed.

## 11. Abstract Factory Pattern

In this chapter I would like to explain the Abstract Factory pattern. This pattern is essential for learning the Factory Method and Bridge patterns.

### Challenge

You are working on an ORM (Object Relational Mapping) framework creation. The framework could be used in different databases like:

- Sql Server
- Oracle
- MS Access
- OleDb

Based on the database type, you need to create related classes like:

- SqlConnection, SqlCommand when Sql server
- OracleConnection, OracleCommand when Oracle etc.

How to create a family of related objects without implementation of them?

### Definition

GoF Definition: "Provide an interface for creating families of related or dependent objects without specifying their concrete classes"

### Implementation

Our idea is to create an interface which contains all related objects like:

```csharp
public abstract class DbProviderFactory
{
    public abstract DbConnection CreateConnection();
    public abstract DbCommand CreateCommand();
}
```

Luckily, ADO.NET already includes the same interface as Abstract Factory. The definition is given below: (I have excluded some irrelevant methods from it)

```csharp
namespace System.Data.Common
{
    public abstract class DbProviderFactory
    {
        public virtual DbCommand CreateCommand();
        public virtual DbCommandBuilder CreateCommandBuilder();
        public virtual DbConnection CreateConnection();
        public virtual DbDataAdapter CreateDataAdapter();
        public virtual DbParameter CreateParameter();
    }
}
```

From the above code we can see that the related classes are included as a family without going to the implementation details.

The abstract class DbProviderFactory contains related classes which are abstract: DbCommand, DbConnection etc.

### Concrete Implementations

ADO.NET provides the following implementations of the above abstract class DbProviderFactory.

- `System.Data.SqlClient.SqlClientFactory`
- `System.Data.OleDb.OleDbFactory`

The above classes implements all abstract methods from the base class. Thus it will be providing concrete implementations of DbConnection which is SqlConnection, DbCommand which is SqlCommand etc.

Instantiating from the above classes, we can start using the concrete implementations like following code.

```csharp
SqlClientFactory factory = SqlClientFactory.Instance;

DbConnection connection = factory.CreateConnection();
DbCommand command = factory.CreateCommand();

command.Connection = connection;
command.CommandText = "query here";
command.ExecuteNonQuery();
```

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_46_0.png)
