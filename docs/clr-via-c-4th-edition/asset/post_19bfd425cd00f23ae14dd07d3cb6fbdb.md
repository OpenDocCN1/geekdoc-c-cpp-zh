
## Chapter 11: Events

### In This Chapter

- Designing a Type That Exposes an Event
- How the Compiler Implements an Event
- Designing a Type That Listens for an Event
- Explicitly Implementing an Event

In this chapter, I'll talk about the last kind of member a type can define: events. A type that defines an event member allows the type (or instances of the type) to notify other objects that something special has happened. For example, the Button class offers an event called Click. When a Button object is clicked, one or more objects in an application may want to receive notification about this event in order to perform some action. Events are type members that allow this interaction. Specifically, defining an event member means that a type is offering the following capabilities:

- A method can register its interest in the event.
- A method can unregister its interest in the event.
- Registered methods will be notified when the event occurs.

Types can offer this functionality when defining an event because they maintain a list of the registered methods. When the event occurs, the type notifies all of the registered methods in the collection.

The common language runtime's (CLR's) event model is based on delegates. A delegate is a type-safe way to invoke a callback method. Callback methods are the means by which objects receive the notifications they subscribed to. In this chapter, I'll be using delegates, but I won't fully explain all their details until Chapter 17, "Delegates."

To help you fully understand the way events work within the CLR, I'll start with a scenario in which events are useful. Suppose you want to design an email application. When an email message arrives, the user might like the message to be forwarded to a fax machine or a pager. In architecting this application, let's say that you'll first design a type called MailManager that receives the incoming email messages. MailManager will expose an event called NewMail. Other types (such as Fax and Pager) may register interest in this event. When MailManager receives a new email message, it will raise the event, causing the message to be distributed to each of the registered objects. Each object can process the message in any way it desires.

When the application initializes, let's instantiate just one MailManager instance—the application can then instantiate any number of Fax and Pager types. Figure 11-1 shows how the application initializes and what happens when a new email message arrives.

![](img/857bdf6cef9e242b53a37f88df9a1287_275_0.png)

1. A method in the Fax object registers interest with the MailManager's event.
2. A method in the Pager object registers interest with the MailManager's event.
3. A new mail message arrives at MailManager.
4. The MailManager object fires the notification off to all the registered methods, which process the mail message as desired.

**FIGURE 11-1** Architecting an application to use events.

Here's how the application illustrated in Figure 11-1 works: the application initializes by constructing an instance of MailManager. MailManager offers a NewMail event. When the Fax and Pager objects are constructed, they register an instance method with MailManager's NewMail event so that MailManager knows to notify the Fax and Pager objects when new email messages arrive. Now, when MailManager receives a new email message (sometime in the future), it will raise the NewMail event, giving all of the registered methods an opportunity to process the new message in any way they want.

### Designing a Type That Exposes an Event

There are many steps a developer must take in order to define a type that exposes one or more event members. In this section, I'll walk through each of the necessary steps. The MailManager sample application (which can be downloaded from the Books section in Resources at http://wintellect.com/Books) shows all of the source code for the MailManager type, the Fax type, and the Pager type. You'll notice that the Pager type is practically identical to the Fax type.

#### Step #1: Define a type that will hold any additional information that should be sent to receivers of the event notification

When an event is raised, the object raising the event may want to pass some additional information to the objects receiving the event notification. This additional information needs to be encapsulated into its own class, which typically contains a bunch of private fields along with some read-only public properties to expose these fields. By convention, classes that hold event information to be passed to the event handler should be derived from System.EventArgs, and the name of the class should be suffixed with EventArgs. In this example, the NewMailEventArgs class has fields identifying who sent the message (m_from), who is receiving the message (m_to), and the subject of the message (m_subject).

```csharp
// Step #1: Define a type that will hold any additional information that
// should be sent to receivers of the event notification
internal class NewMailEventArgs : EventArgs {

    private readonly String m_from, m_to, m_subject;

    public NewMailEventArgs(String from, String to, String subject) {
        m_from = from; m_to = to; m_subject = subject;
    }

    public String From    { get { return m_from; } }
    public String To      { get { return m_to;   } }
    public String Subject { get { return m_subject; } }
}
```

![](img/857bdf6cef9e242b53a37f88df9a1287_276_0.png)

> **Note** The EventArgs class is defined in the Microsoft .NET Framework Class Library (FCL) and is implemented like the following.
>
> ```csharp
> [ComVisible(true), Serializable]
> public class EventArgs {
>     public static readonly EventArgs Empty = new EventArgs();
>     public EventArgs() { }
> }
> ```
>
> As you can see, this type is nothing to write home about. It simply serves as a base type from which other types can derive. Many events don't have any additional information to pass on. For example, when a Button notifies its registered receivers that it has been clicked, just invoking the callback method is enough information. When you're defining an event that doesn't have any additional data to pass on, just use EventArgs.Empty rather than constructing a new EventArgs object.

#### Step #2: Define the event member

An event member is defined using the C# keyword `event`. Each event member is given accessibility (which is almost always `public` so that other code can access the event member), a type of delegate indicating the prototype of the method(s) that will be called, and a name (which can be any valid identifier). Here is what the event member in our MailManager class looks like.

```csharp
internal class MailManager {
    // Step #2: Define the event member
    public event EventHandler<NewMailEventArgs> NewMail;
    ...
}
```

`NewMail` is the name of this event. The type of the event member is `EventHandler<NewMailEventArgs>`, which means that all receivers of the event notification must supply a callback method whose prototype matches that of the `EventHandler<NewMailEventArgs>` delegate type. The generic `System.EventHandler` delegate is defined as follows:

```csharp
public delegate void EventHandler<TEventArgs>(Object sender, TEventArgs e);
```

The method prototypes must look like the following:

```csharp
void MethodName(Object sender, NewMailEventArgs e);
```

> **Note** A lot of people wonder why the event pattern requires the sender parameter to always be of type `Object`. After all, because the MailManager will be the only type raising an event with a `NewMailEventArgs` object, it makes more sense for the callback method to be prototyped like the following.
>
> ```csharp
> void MethodName(MailManager sender, NewMailEventArgs e);
> ```
>
> The pattern requires the sender parameter to be of type `Object` mostly because of inheritance. What if MailManager were used as a base class for SmtpMailManager? In this case, the callback method should have the sender parameter prototyped as SmtpMailManager instead of MailManager, but this can't happen because SmtpMailManager just inherited the NewMail event. So the code that was expecting SmtpMailManager to raise the event must still have to cast the sender argument to SmtpMailManager. In other words, the cast is still required, so the sender parameter might as well be typed as `Object`.
>
> The next reason for typing the sender parameter as `Object` is just flexibility. It allows the delegate to be used by multiple types that offer an event that passes a `NewMailEventArgs` object. For example, a PopMailManager class could use the delegate even if this class were not derived from MailManager.
