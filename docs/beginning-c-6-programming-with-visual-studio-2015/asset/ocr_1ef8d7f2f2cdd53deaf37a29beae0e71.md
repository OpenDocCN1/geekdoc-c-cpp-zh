```
public void Connect() => pollTimer.Start();
public void Disconnect() => pollTimer.Stop();
...
```

Also in the constructor, you register an event handler for the Elapsed event, just as you did in the first example. The handler method, CheckForMessage(), raises an event on average once every 10 times it is called. You will look at the code for this, but first it would be useful to look at the event definition itself.

Before you define an event, you must define a delegate type to use with the event — that is, a delegate type that specifies the return type and parameters to which an event handling method must conform. You do this using standard delegate syntax, defining it as public inside the Ch13Ex02 namespace to make the type available to external code:

```
namespace Ch13Ex02
{
    public delegate void MessageHandler(string messageText);
}
```

This delegate type, called MessageHandler here, is a void method that has a single string parameter. You can use this parameter to pass an instant message received by the Connection object to the Display object. Once a delegate has been defined (or a suitable existing delegate has been located), you can define the event itself, as a member of the Connection class:

```
public class Connection
{
    public event MessageHandler MessageArrived;
}
```

You simply name the event (here it is MessageArrived) and declare it by using the event keyword and specifying the delegate type to use (the MessageHandler delegate type defined earlier). After you have declared an event in this way, you can raise it simply by calling it by name as if it were a method with the return type and parameters specified by the delegate. For example, you could raise this event using the following:

```
MessageArrived("This is a message.");
```

If the delegate had been defined without any parameters, then you could simply use the following:

```
MessageArrived();
```

Alternatively, you could define more parameters, which would require more code to raise the event. The CheckForMessage() method looks like this:

```
private static Random random = new Random();
private void CheckForMessage(object source, ElapsedEventArgs e)
{
    WriteLine("Checking for new messages.");
    if ((random.Next(9) == 0) && (MessageArrived != null))
    {
        MessageArrived("Hello Mami!");
    }
}
```

You use an instance of the Random class shown in earlier chapters to generate a random number between 0 and 9, and raise an event if the number generated is 0, which should happen 10 percent of