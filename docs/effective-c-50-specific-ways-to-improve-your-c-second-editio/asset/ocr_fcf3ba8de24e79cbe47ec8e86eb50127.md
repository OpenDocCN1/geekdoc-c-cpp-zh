```
get { return theOnly; }
}
```

```
// Define the event:
public event EventHandler<LoggerEventArgs> Log;
```

```
// add a message, and log it.
public void AddMsg(int priority, string msg)
{
    // This idiom discussed below.
    EventHandler<LoggerEventArgs> l = Log;
    if (l != null)
        l(this, new LoggerEventArgs(priority, msg));
}
```

The AddMsg method shows the proper way to raise events. The temporary variable to reference the log event handler is an important safeguard against race conditions in multithreaded programs. Without the copy of the reference, clients could remove event handlers between the if statement check and the execution of the event handler. By copying the reference, that can’t happen.

I’ve defined LoggerEventArgs to hold the priority of an event and the message. The delegate defines the signature for the event handler. Inside the Logger class, the event field defines the event handler. The compiler sees the public event field definition and creates the Add and Remove operators for you. The generated code is exactly the same as though you had written the following:

```
public class Logger
{
    private EventHandler<LoggerEventArgs> log;

    public event EventHandler<LoggerEventArgs> Log
    {
        add { log = log + value; }
        remove { log = log - value; }
    }
}
```