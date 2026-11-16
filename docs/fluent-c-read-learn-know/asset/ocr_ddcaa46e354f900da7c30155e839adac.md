# # EVENT OBJECTS

Defining an event is a whole lot easier than implementing any of the Observer patterns directly, but it does require four things.

# ## AN ARGUMENT CLASS

The second argument passed to an event handler is an instance of System.EventArgs or a class that descends from it. EventArgs itself doesn't pass any information, but the Framework defines dozens of classes that derive from it (everything from AccessKeyEventArgs to XsltMessageEncounteredEventArgs), so if you want to pass some information, you might be able to use one of them, or you can define your own class that inherits System.EventArgs. By convention, the argument class should be named <EventName>EventArgs.

# ## AN EVENT DELEGATE

If you're using an EventArgs class that's defined by the Framework, there will be a delegate defined for it as well. The handler will be named <EventNameHandler>, and you should follow the same convention when you create a delegate for a new argument type.

The delegate defines the signature of methods that can respond to the event. All delegates have the same basic pattern: they are declared as public, return void, and have two arguments. The first argument is an Object named sender, and represents the instance that is raising the event. The second argument is named e, and represents an instance of the appropriate event argument class.

# ## AN EVENT DECLARATION

Of course, you need to declare the event so the CLR knows about it. The syntax is simple:

```
. public event <DelegateType> <EventName>;
```

# ## A METHOD TO RAISE THE EVENT

Finally, you need a method that will actually raise the event. In C#, the syntax to raise an event looks like a method call, and by convention the event-raising method is named On<EventName>, is protected, and takes the event arguments as a parameter, so the basic pattern looks like this:

```
protected void On<EventName>(<EventName>Args e)
{
. <EventName>(this, e);
}
```