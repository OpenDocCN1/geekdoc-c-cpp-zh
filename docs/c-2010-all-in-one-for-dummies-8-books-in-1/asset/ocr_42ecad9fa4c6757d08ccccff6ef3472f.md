# Stuff Happens — C# Events 371

A common example, which you can see in the SimpleProgress code example, discussed earlier in this chapter, is a Button advertising its various events, including a Click event. In C#, class Button exposes this event as

```
event _dispCommandControlEvents_ClickEventHandler Click;
```

where the second, lo-o-ing is a delegate defined somewhere in .NET.

Because events are used so commonly, .NET defines new EventHandler and EventHandler<TEEventArgs> types for you. You can change NewEditionEventHandler in the previous code to EventHandler or the generic EventHandler<TEEventArgs>, and you don't need your own delegate type. Throughout the rest of this chapter, I pretend that I used the built-in EventHandler<TEEventArgs> delegate type mentioned earlier, NewEventHandler or your custom type, NewEditionEventHandler. You should follow this form,

```
event EventHandler<NewEditionEventArgs> NewEdition;
```

The NewspaperEvents example on the site demonstrates correctly setting up your event and handling it in various subscribers. (A second sample program, NewspaperEventsNongeneric, avoids the generic stuff if you get <a>code free. If so, you can mentally omit the <eventhandlerargs> information in the following section.)

# How subscribers subscribe to an event

To receive a particular event, subscribers sign up something like this:

```
publisher.EventHandlerName +=
EventHandler<some EventArgs type here>(some method name here);
```

where publisher is an instance of the publisher class, the event name, and EventHandler<TEEventArgs> is the delegate underneath the event. More importantly, the code in the previous example might be:

```
myPublisher.NewEdition += new EventHandler<NewEditionEventArgs>(MyPublisher);
```

Because an event object is a delegate under its little hood, the += syntax is adding a method to the list of methods that the delegate will call when you invoke it.

Any number of objects can subscribe this way (and the delegate will hold a list of all subscribed "handler" methods) — the event on which the event was defined can subscribe, if you like. (And so, this example shows that a delegate can "point" to more than one method.)

![](bbox=[0.115, 0.125, 0.195, 0.185])

![](bbox=[0.115, 0.265, 0.195, 0.325])

![](bbox=[0.115, 0.45, 0.195, 0.51])

![](bbox=[0.115, 0.81, 0.195, 0.885])

Book II
Chapter 9

Delegating
Events