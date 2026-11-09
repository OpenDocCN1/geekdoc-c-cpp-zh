A class that uses `MailManager` as a base type is free to override the `OnNewMail` method. This capability gives the derived class control over the raising of the event. The derived class can handle the new e-mail message in any way it sees fit. Usually, a derived type calls the base type's `OnNewMail` method so that the registered method(s) receive the notification. However, the derived class might decide to disallow the event from being forwarded.

# ## Step #4: Define a method that translates the input into the desired event

Your class must have some method that takes some input and translates it into the raising of the event. In my `MailManager` example, the `SimulateNewMail` method is called to indicate that a new e-mail message has arrived into `MailManager`:

```
```csharp
internal class MailManager {

    // Step #4: Define a method that translates the
    // input into the desired event
    public void SimulateNewMail(String from, String to, String subject) {

        // Construct an object to hold the information we wish
        // to pass to the receivers of our notification
        NewMailEventArgs e = new NewMailEventArgs(from, to, subject);

        // Call our virtual method notifying our object that the event
        // occurred. If no type overrides this method, our object will
        // notify all the objects that registered interest in the event
        OnNewMail(e);
    }
}
```
```

`SimulateNewMail` accepts information about the message and constructs a `NewMailEventArgs` object, passing the message information to its constructor. `MailManager`'s own virtual `OnNewMail` method is then called to formally notify the `MailManager` object of the new e-mail message. Usually, this causes the event to be raised, notifying all of the registered methods. (As mentioned before, a class using `MailManager` as a base class can override this behavior.)

# ## How the Compiler Implements an Event

Now that you know how to define a class that offers an event member, let's take a closer look at what an event really is and how it works. In the `MailManager` class, we have a line of code that defines the event member itself:

```
```csharp
public event EventHandler<NewMailEventArgs> NewMail;
```
```