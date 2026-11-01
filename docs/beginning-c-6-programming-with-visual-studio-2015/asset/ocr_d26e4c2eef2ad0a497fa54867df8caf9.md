> **NOTE** The fact that delegates are used in events is one of the reasons why delegates are so useful. This is why some space was devoted to them in Chapter 6. You might want to review that material to refresh your memory about delegates and how you use them.

The basic sequence of processing is as follows: First, an application creates an object that can raise an event. For example, suppose an instant messaging application creates an object that represents a connection to a remote user. That connection object might raise an event when a message arrives through the connection from the remote user (see Figure 13-2).

![](bbox=[0.12, 0.44, 0.48, 0.58])

FIGURE 13-2

Next, the application subscribes to the event. Your instant messaging application would do this by defining a method that could be used with the delegate type specified by the event, passing a reference to this method to the event. The event handler method might be a method on another object, such as an object representing a display device to show instant messages when they arrive (see Figure 13-3).

![](bbox=[0.12, 0.8, 0.48, 0.93])

FIGURE 13-3

When the event is raised, the subscriber is notified. When an instant message arrives through the connection object, the event handler method on the display device object is called. Because you are using a standard method, the object that raises the event can pass any relevant information via parameters, making events very versatile. In the example case, one parameter might be the text of the instant message, which the event handler could display on the display device object. This is shown in Figure 13-4.