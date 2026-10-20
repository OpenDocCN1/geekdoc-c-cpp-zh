# How to define and use events

An *event* is a signal that a particular action has occurred on an object that’s created from the class. Then, any class that uses that object can respond to the event by wiring an event handler to it. Figure 13-7 illustrates how this works using a delegate like the one in the last figure.

To define an event, you start by declaring a delegate that will be used to refer to the event handler for the event. This is done by the first statement in the ProductList class. Then, you code an event declaration as shown by the second statement. This declaration names the delegate followed by an event name. In this case, the event declaration specifies the ChangeHandler delegate and the Changed event.

Once you’ve declared an event, you can raise it by referring to it by name as shown in the Add() method of the ProductList class. This method raises the Changed event after it adds a product to the list. Here, the this keyword is used as the parameter, which causes the ProductList object that raised the event to be passed to the event handler.

To respond to an event that’s raised by a class, you use code like that shown in the second example. This code includes a method named PrintToDebug() that will handle the event. Notice that this event handler accepts the ProductList parameter that will be passed by the Changed event.

To use this event handler, you start by creating an instance of the class that raises the event. In this case, an instance of the ProductList class named products is created. Then, you wire the event handler to the event. Here, the ChangeHandler delegate is used to wire the PrintToDebug() event handler to the Changed event of the products list. As a result, the PrintToDebug() method will be called whenever the Changed event is raised for this object.

In most cases, you’ll code the statement that wires the event handler in the Load event of the form that uses it as shown here. However, you can also wire an event handler in the constructor of a class. The only restriction is that this statement must be executed before the event is raised. If the event is raised before you’ve wired the event handler to it, the event handler won’t execute.