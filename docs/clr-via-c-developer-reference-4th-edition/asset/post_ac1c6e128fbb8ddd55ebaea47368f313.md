
When the application initializes, let's instantiate just one MailManager—the application can then instantiate any number of Fax and Pager types. Figure 11-1 shows how the application initializes and what happens when a new email message arrives.

![](img/0ce3b788d061e3d3095fa554b1a34adf_275_0.png)

- 1. A method in the Fax object registers interest with the MailManager's event.
- 2. A method in the Pager object registers interest with the MailManager's event.
- 3. A new mail message arrives at MailManager.
- 4. The MailManager object fires the notification off to all the registered methods, which process the mail message as desired.

**FIGURE 11-1** Architecting an application to events.

Here's how the application illustrated in Figure 11-1 works: the application initializes by constructing an instance of MailManager. Manager offers a NewMail event. When the Fax and Pager objects are constructed, they register an instance method with MailManager's NewMail event that MailManager knows to notify the Fax and Pager objects when new email messages arrive. Now, when MailManager receives a new email message (sometimes in the future), it will raise the NewMail event, giving all of the registered methods an opportunity to process the new message in any way.

## Designing a Type That Exposes an Event

There are many steps a developer must take in order to define a type that exposes one or more members. In this section, I'll walk through each of the necessary steps. The MailManager sample application (which can be downloaded from the Books section in Resources at http://wintlect.com/Books) shows all of the source code for the MailManager type, the Fax type, and the Pager type. You'll notice that the Pager type is practically identical to the Fax type.

## Step #1: Define a type that will hold any additional information that should be sent to receivers of the event notification

When an event is raised, the object raising the event may want to pass some additional information to objects receiving the event notification. This additional information needs to be encapsulated into its class, which typically contains a bunch of fields along with some read-only properties to expose these fields. By convention, classes that hold event information to be passed to the event handler should be derived from System.EventArgs, and the name of the class should be suffixed with EventArgs. In this example, the NewMailEventArgs class has fields identifying who sent the message (m_from), who is receiving the message (m_to), and the subject of the message

```
// Step #1: Define a type that will hold any additional information
// should be sent to receivers of the event notification
internal class NewMailEventArgs {

    private readonly String m_from, m_to, m_subject;

    public NewMailEventArgs(String from, String to, String subject) {
        m_from = from; m_to = to; m_subject = subject;
    }

    public String From { get { return m_from; } }
    public String To { get { return m_to; } }
    public String Subject { get { return m_subject; }}
}
```

> Note: The EventArgs class is defined in the Microsoft .NET Framework Class Library (FCL) and is implemented like the following.

```
[Visible(true), Serializable]
public class EventArgs {
    public static readonly EventArgs Empty = new EventArgs();
    public EventArgs() {
}}
```

As you can see, this type is nothing to write home about. It simply serves as a base type from which other types can derive. Many events don't have any additional information to pass on. For example, when a Button notifies its registered receivers that it has been clicked, just invoking the callback method is enough information. When you're defining an event that doesn't have any additional data to pass on, just use EventArgs.Empty rather than constructing a new EventArgs object.

## Step #2: Define the event member

An event is defined using the C# keyword event. Each event member is given accessibility (which is almost always public so that other code can access the event member), a type of delegate indicating the prototype of the method(s) that will be called, and a name (which can be any valid identifier). Here is what the event member in our MailManager class looks like.

```
internal class MailManager {
    // Step #2: Define the event member
    public event EventHandler<NewMailEventArgs> NewMail;
    ...
}
```

NewMail is the name of the event member. The type of the event member is EventHandler<NewMailEventArgs>, which means all receivers of the event notification must supply a callback method whose prototype matches that of the EventHandler<NewMailEventArgs> delegate type. Because the generic System.EventHandler delegate defined as follows:

```
public delegate void EventHandler<TEventArgs>(Object sender, TEventArgs);
```

the method prototypes must look like the following.

```
void MethodName(Object sender, NewMailEventArgs e);
```

> A lot of people wonder why the pattern requires the sender parameter to be of type Object. After all, because the MailManager will be the only type raising an event with a NewMailEventArgs object, it makes more sense for the callback method to be prototyped like the following:
void MethodName(MailManager sender, NewMailEventArgs e);

The pattern requires the sender parameter to be of type Object mostly because of inheritance. What if MailManager were used as a base class for SmtpMailManager? In this case, the callback method should have the sender parameter prototyped as SmtpMailManager instead of MailManager, but this can't happen because SmtpMailManager inherited the NewMail event. The next reason for using the sender parameter as Object is flexibility. It allows the delegate to be used by multiple types. For example, a PopMailManager class could use the delegate even if this class were not derived from MailManager.

The event pattern also requires that the delegate definition and the callback method name the EventArgs-derived parameter e. The only reason for this is add additional consistency to the pattern, making it easier for developers to learn and implement the pattern. Tools that spit out source code (such as Microsoft Visual Studio) also know to call the return type of void. This is necessary because the event pattern requires all event handlers to return void. raising an event might call callback methods, and there is no way to get the return values from all of them. Having a return type of void allows the callbacks to return a value after. Unfortunately, there are some event handlers in the FCL, such as ResolveEventHandler, that did not follow Microsoft's own prescribed pattern because it returns an object of type Assembly.

## Step #3: Define a method responsible for raising the event to notify registered objects that the event has occurred

By convention, the class should define a protected, virtual method that is called by code internally within the class and its derived classes when the event is raised. This method takes one parameter, a NewMailEventArgs object, which includes the information passed to the objects receiving the notification. The default implementation of this method simply checks if any objects have registered interest in the event and if so, the event will be raised, notifying the registered methods that the event has occurred. Here is what the method in our MailManager looks like.

```
internal class MailManager {
    ...
    // Step #3: Define a method for raising the event
    // to notify registered objects that the event has occurred
    // If this class is sealed, make this method private and nonvirtual
    protected virtual void OnMail(NewMailEventArgs args) {

        // Copy a reference to the delegate field now into a temporary field for thread safety
        EventHandler<NewMailEventArgs> temp = Volatile.Read(ref NewMail);

        // If any methods registered with our event, notify them
        if (temp != null) temp(this, args);
    }
    ...
}
```
