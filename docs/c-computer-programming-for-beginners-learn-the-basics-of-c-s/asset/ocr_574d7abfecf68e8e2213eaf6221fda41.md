reference can be changed at runtime. They are especially used for implementing
events and the call-back methods.

# Declaring delegates

It determines the methods that can be referenced by the delegate. A delegate can refer
to a method, which has the same signature as that of the delegate.

Syntax –

```
delegate <return type> <delegate-name> <parameter list>
```

Once a delegate type is declared, a delegate object must be created with the new
keyword and be associated with a particular method.

Delegate objects can be composed using the “+\” operator. Only delegates of the same
t can be composed. The “-” can be used to remove a component delegate from a
composed delegate. You can create an invocation list of methods by using this
property of delegate that will be called when a delegate is invoked and this is called
as multicicasting of a delegate.

# Using delegates with events

Events are user actions such as clicks, key press, mouse movements or some
occurrence such as system generated notifications. The events are used for inter-
process communication.

Events are raised and declared in class and associated with the event handlers using
delegates within the same class or some other class. The class containing the event is
used to publish the event and is called as the publisher class, whereas, some other
class that accepts this event is called the subscriber class.

A publisher is an object that contains the definition of the event and the delegate. A
publisher object invokes the event and it is notified to other objects. The
other hand, subscriber is an object that accepts the event and provides an event
handler.

To declare an event inside a class, first delegate type for the event must be declared.
Example -