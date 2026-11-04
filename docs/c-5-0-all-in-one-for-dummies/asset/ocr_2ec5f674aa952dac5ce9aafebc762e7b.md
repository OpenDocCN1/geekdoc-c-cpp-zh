# How to publish an event

When the publisher decides that something worthy of publishing to all subscribers has occurred, it raises (sends) the event. This situation is analogous to a real newspaper putting out the Sunday edition.

To publish the event, the publisher would have code like this in one of its methods (but see the later section “A recommended way to raise your events”):

```
NewEditionEventArgs e = new NewEditionEventArgs(<args to constructor here>);
NewEdition(this, e); // Raise the event -- 'this' is the publisher object.
```

Or for the Button example, though this is hidden in class Button:

```
EventArgs e = new EventArgs(); // See next section for more on this topic.
Click(this, e); // Raise the event.
```

In each of these examples, you set up the necessary arguments — which differ from event to event; some events need to pass along a lot of info. Then you raise the event by “calling” its name (like invoking a delegate!):

```
eventName(<argumentlist>); // Raising an event (distributing the newspaper)
NewEdition(this, e);
```

![](bbox=[0.12, 0.55, 0.22, 0.7])

Events can be based on different delegates with different signatures, that have different parameters, as in the earlier NewEditionEventHandler example, but providing the sender and e parameters is conventional for events. The built-in EventHandler and EventHandler<TEventArgs> delegate types define them for you.

Passing along a reference to the event’s sender (the object that raises the event) is useful if the event-handling method needs to get more information from it. Thus a particular Button object, button1, can pass a reference to the Form class the button is a part of. The button’s Click event handler resides in a Form class, so the sender is the form: You would pass this.

![](bbox=[0.12, 0.78, 0.22, 0.92])

You can “raise” an event in any method on the publishing class. But when? Raise it whenever appropriate. I have a bit more to say about raising events after the next section.

# How to pass extra information to an event handler

The e parameter to an event handler method is a custom subclass of the System.EventArgs class. You can write your own NewEditionEventArgs class to carry whatever information you need to convey: