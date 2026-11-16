# CREATE THE CLR EVENT

In the same way that a dependency property is backed by a POCO property, a routed event is backed by a POCO event with a very simple structure, but because the POCO event needs to reference the routed event, it's declared after the routed event is registered.

The event should be declared public.

The type of the event should be the delegate type—either the custom one you’ve declared, or one of the types defined in the Framework.

The add accessor should call the AddHandler method with the signature

```
AddHandler(<RoutedEventName>, value)
```

The remove accessor should call the RemoveHandler method with the signature

```
RemoveHandler(<RoutedEventName>, value)
```

# CREATE A METHOD TO RAISE THE EVENT

While not strictly necessary, it’s considered good practice to expose a method that raises the event. This method can be called elsewhere in the class (eliminating duplicate code). The signature of the method is determined by your program logic, but typically returns a void and by convention, should be named On<Event>.

If your class exposes a tunnel/bubble event pair, a single method is typically used to raise both of them.

Here’s an example of a basic event-raising method:

```
protected OnMyCustomEvent ()
{
    RoutedEventArgs newArgs = new RoutedEventArgs(MyClass.MyCustomEvent);
    RaiseEvent(newArgs);
}
```

![](bbox=[0.1, 0.73, 0.22, 0.9])

# PUT ON YOUR THINKING HAT

Add two events to the project we’ve been working on. The first, called MyDefaultEvent, should use the default RoutedEventArgs, and the second, called MyCustomEvent, should use a custom argument called CustomArgs that adds an int MyProp. Call the custom delegate MyCustomHandler. Both events should use RoutingStrategy.Bubble.