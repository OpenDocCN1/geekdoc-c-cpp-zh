To solve this problem, C# also enables defining events with a property-like syntax, as shown in Listing 6.4.

# **LISTING 6.4** Event Declaration Using Event Properties

```
1. public class Contact
   { 
   2.    private EventHandlerList events = new EventHandlerList();
   3.    private static readonly object addressChangedEventKey = new object();
   4.
   5.    public event EventHandler AddressChanged
   6.    {
   7.       add
   8.       {
   9.          this.events.AddHandler(addressChangedEventKey, value);
   10.      }
   11.     remove
   12.     {
   13.        this.events.RemoveHandler(addressChangedEventKey, value);
   14.     }
   15. }
   16.}
```

Line 3 declares an **EventHandlerList** specifically designed to contain a list of event delegates. This enables you to use a single variable that contains an entry for every event that has a subscriber. Next, line 4 declares a static read-only **object** variable named **addressChangedEventKey** that represents the key used for the event in the **EventHandlerList**. Finally, lines 6 through 16 declare the actual event property.

This syntax should be familiar to you because it is almost the same syntax for defining a property. The difference is that rather than get and set accessors, you have add and remove accessors. The add accessor simply adds the input delegate instance to the list, whereas the remove accessor removes it. Both of the accessors use the predefined key for the event property to add and remove instances from the list.

Now that you understand the basics of publishing an event, a convenient and consistent way to describe when the event occurs are to categorize them as pre-events and post-events.

Post-events are the most common type of event and occur after the state of the object has changed. Pre-events, also called **cancellable events**, occur before the state of the object changes and provide the capability to cancel the event. These events use the **CancelEventArgs** class to store event data. The **CancelEventArgs** class simply adds a **Cancel** property your code can read and write. If you create or own cancellable events, you should derive your own custom event data class from the **CancelEventArgs** class.