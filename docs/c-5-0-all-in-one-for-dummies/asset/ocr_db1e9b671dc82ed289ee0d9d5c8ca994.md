```
```csharp
public class NewEditionEventArgs : EventArgs
{
    public NewEditionEventArgs(DateTime date, string majorHeadline)
    {
        PubDate = date; Head = majorHeadline;
    }
    public DateTime PubDate { get; private set; }  // Compiler creates details.
    public string Head { get; private set; }       //
}
```
```

You should implement this class’s members as properties, as shown in the previous code example. The constructor uses the private setter clauses on the properties.

![](bbox=[0.133, 0.326, 0.208, 0.394])

Often, your event doesn’t require any extra arguments and you can just fall back on the EventArgs base class, as shown in the next section.

If you don’t need a special EventArgs-derived object for your event, just pass:

```
```csharp
NewEdition(this, EventArgs.Empty);  // Raise the event.
```
```

# A recommended way to raise your events

The earlier section “How to publish an event” shows the bare bones of raising an event. However, I recommend that you always define a special “event raiser” method, like this:

```
```csharp
protected virtual void OnNewEdition(NewEditionEventArgs e)
{
    EventHandler<NewEditionEventArgs> temp = NewEdition;
    if(temp != null)
    {
        temp(this, e);
    }
}
```
```

Providing this method ensures that you always remember to complete two steps:

+   1. **Store the event in a temporary variable.**
+   
+      This step makes your event more usable in situations where multiple “threads” try to use it at the same time — threads divide your program into a foreground task and one or more background tasks, which run simultaneously (concurrently). I don’t cover how to write multithreaded programs in this book; just follow this guideline.
+   
+   2. **Check the event for null before you try to raise it.**
+   
+      If it’s null, trying to raise it causes an error. Besides, null also means that no other objects have shown an interest in your event (none is subscribed), so why bother raising it? *Always* check the event for null, regardless of whether you write this `OnSomeEvent` method.

![](bbox=[0.13, 0.709, 0.209, 0.786])

Book II
Chapter 9

Delegating Those Important Events