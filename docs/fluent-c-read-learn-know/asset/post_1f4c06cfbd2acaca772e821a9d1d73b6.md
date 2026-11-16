
## LISTEN FOR HANDLED EVENTS

Well, the Window caught the MouseDown when you clicked outside a control, and the Button caught the Click event (but the Window didn't get the MouseDown), and the ListBox only behaved as expected when you clicked on the background, not on a ListBoxItem. So what happened?

Routed events aren't broken; they do work the way I've described, but there's a little wrinkle we haven't seen yet. If you look back at the class diagram for the RoutedEventArgs, you'll see a Handled property. If that's set to true inside an event handler, the event still bubbles or tunnels, but most of the handlers that are defined for the event aren't called, because the event system assumes that the handlers aren't interested unless they tell it otherwise.

Controls like the Button and RadioButton are setting the Handled property to true, so our Window-level handler isn't getting called. In fact, they're not just handling the MouseDown event; they're converting it into an entirely different event (Click). That's a pretty common pattern in WPF—controls often consume low-level input events and replace them with something a little more useful.

If you do want to know about events that some low-level object is helpfully handling for you, you can use the AddHandler() method and pass true as the HandledEventsToo parameter. Let's try it out. Take out the event handler specification in the Window XAML tag and replace it with an AddHandler() call inside the constructor.

Now run the application and test the results. Closer to what we expected, isn't it? But did you notice that the Button is no longer clicking? It reports the MouseDown, but the Click event doesn't appear to be raised at all.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_649_0.png)

## HOW'D YOU DO?

Did you find the answer? It's a bug in the Framework. Andrej Burger posted the solution on the MSDN forums (search for "Button does not click" if you want to read his post). If you interrupt processing by displaying a MessageBox or opening another window or, as Andrej found, setting a breakpoint so that Visual Studio opens the debugger, the Click event goes missing.

There's a lesson to be learned here. The vast majority of the bug in your application will be yours. When you track most of them down, you'll probably feel a little silly. (That doesn't change with experience.) But sometimes it's not your fault. There ARE bugs in the Framework. Not a lot, and that shouldn't be your first (second, or third) guess, but it happens.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_650_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_650_1.png)

## WORK AROUND THE BUG

Obviously, you can't fix bugs in the Framework itself, so you need to find a way to work around them. Sometimes that's easy: sometimes it's hard. Sometimes it requires completely re-thinking how you're doing something. I once spent a month re-designing an application to work around a bug in the way tab controls handled data binding in the first version of WPF. (I'd really like to have that month of my life back.)

This time it's easy, because what we're doing isn't very important. The problem is with interrupting the UI, so we just won't do that. We can replace the MessageBox with a Console.WriteLine() call

```
Console.WriteLine(eventDetailsSB.ToString());
```

Make that change to the ShowArguments() method, and re-run the application. It should work the way it's supposed to now, but you'll have to look in the Output window in Visual Studio to see the EventArgs details.

If the Output window isn't displayed automatically when you run the application, you can show it from the View menu or by pressing Ctrl+W, O. (Note: Many programmers routinely use Console.WriteLine() instead of the MessageBoxes we've been using to display internal information like this, but I personally find it no easier to call and a little cluttered to read.)

## EVENT ELEMENTS

You've probably noticed that routed events are a lot like dependency properties. WPF takes the basic POCO object and adds some additional functionality. It probably won't come as a surprise that the process for creating one is very similar. You need to create the objects involved in a different order, but the components are the same:

| DEPENDENCY PROPERTY | ROUTED EVENT |
| :--- | :--- |
| CLR PROPERTY<br>Accessors must only call GetValue() and SetValue(). | CLR EVENT<br>Accessors must only call AddHandler() and RemoveHandler(). |
| PROPERTY METADATA<br>Describes property to the WPF property system. | EVENTARGS & DELEGATE<br>You can use existing types such as RoutedEventArgs and RoutedEventHandler, or create custom objects if you need to pass additional information to methods that handle your events. |
| CALLBACK METHODS<br>These optional methods are invoked by the property system. | EVENT METHOD<br>This optional method will raise the event. |
| PROPERTY REGISTRATION<br>The call to one of the DependencyProperty.Register...() methods tells the WPF property system to manage the property. | EVENT REGISTRATION<br>The call to one of the EventManager.Register...() methods tells the WPF property system to manage the property. |

## CREATING ROUTED EVENTS

Unfortunately, Visual Studio doesn't include a snippet for creating routed events (probably because you'll do it a lot less frequently). But the steps are similar to creating a dependency property, which you already know how to do, and none is particularly difficult. Here's the process in detail:

### 1 CREATE THE EVENTARGS CLASS, IF NECESSARY

Many events can use RoutedEventArgs or one of its descendants, but if you need to pass additional information to the methods that respond to your events, you'll need to create your own argument class. The class can be defined independently or nested within the class that declares the event, which is convenient if you won't be using it elsewhere. In either case, the class should be public.

The class should usually derive directly from RoutedEventArgs or from one of its descendants.

The new properties of the class should be standard CLR properties, not dependency properties.

### 2 CREATE THE DELEGATE, IF NECESSARY

If you're using one of the .NET Framework argument classes, you can use the RoutedEventHandler as your event delegate, but if you declare a new argument type, you'll also need to declare a delegate.

The delegate should be declared public void.

The first parameter should be an Object, by convention called sender.

The second parameter should be your custom argument class, by convention called e.

### 3 CREATE THE ROUTED EVENT

As with dependency properties, the routed event is created by registering it with the WPF event system using the static RegisterRoutedEvent() method of the EventManager class. But there's only one version of RegisterRoutedEvent():

```csharp
public static readonly RoutedEvent <ClrEventName>Event = EventManager.RegisterRoutedEvent("<ClrEventName>", <routingStrategy>, typeof(<delegate>), typeof(<ownerClass>))
```

Routed events are declared public, static and readonly.

This is a member of the RoutingStrategy enumeration that has the values Tunnel, Bubble and Direct.

### CREATE THE CLR EVENT

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

### CREATE A METHOD TO RAISE THE EVENT

While not strictly necessary, it’s considered good practice to expose a method that raises the event. This method can be called elsewhere in the class (eliminating duplicate code). The signature of the method is determined by your program logic, but typically returns a void and by convention, should be named On<Event>.

If your class exposes a tunnel/bubble event pair, a single method is typically used to raise both of them.

Here’s an example of a basic event-raising method:

```csharp
protected void OnMyCustomEvent ()
{
    RoutedEventArgs newArgs = new RoutedEventArgs(MyClass.MyCustomEvent);
    RaiseEvent(newArgs);
}
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_653_0.png)

### PUT ON YOUR THINKING HAT

Add two events to the project we’ve been working on. The first, called MyDefaultEvent, should use the default RoutedEventArgs, and the second, called MyCustomEvent, should use a custom argument called CustomArgs that adds an int MyProp. Call the custom delegate MyCustomHandler. Both events should use RoutingStrategy.Bubble.
