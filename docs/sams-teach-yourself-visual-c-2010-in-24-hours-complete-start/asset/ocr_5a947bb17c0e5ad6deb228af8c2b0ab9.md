# Understanding Events

Events follow a publish/subscribe model where the publisher determines when an event is raised. The subscribers determine the action taken in response to that event. Events can have multiple subscribers, in which case the event handlers are invoked synchronously when the event is raised. If an event has no subscribers, it is never actually raised. Subscribers can handle multiple events from multiple publishers.

> **By the Way**

**Delegates**

In traditional programming terms, an event is a form of a callback, which enables a method to be passed as an argument to other methods. In C#, these callbacks are referred to as delegates. Event handlers are actually nothing more than methods invoked through delegates.

You can think of delegates as being similar to C or C++ function pointers or Delphi closures and are a type-safe and secure means of writing a callback. Delegates run under the caller's security permissions, not the declarer's permissions. A delegate type simply defines a method signature and any method with a compatible signature can be associated with a delegate. One key difference between delegate signatures and regular method signatures is that the return type is included in the signature and the use of the params modifier in the parameter list is allowed.

# Subscribing and Unsubscribing

When you are interested in responding to an event published by another class, you subscribe to that event by defining an event handler method whose signature matches the event delegate signature. You then use the addition assignment operator (+=) to attach the event handler to the event. Listing 6.1 shows how you would subscribe to an event based on the ElapsedEventHandler delegate.

# LISTING 6.1 Subscribing to an Event

```
```
var timer = new Timer(1000);
timer.Elapsed += new ElapsedEventHandler(TimerElapsedHandler);

void TimerElapsedHandler(object sender, ElapsedEventArgs e)
{
    MessageBox.Show("The timer has expired.");
}
```
```

The first parameter should always be an object parameter named sender that represents the object that raised the event. The second parameter represents the data passed to the event handler method. This is always an EventArgs type or a type