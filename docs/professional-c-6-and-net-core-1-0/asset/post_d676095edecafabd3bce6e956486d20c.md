
> **NOTE** You can use lambda expressions anywhere the type is a delegate. Another use of lambda expressions is when the type is Expression or Expression<T>, in which case the compiler creates an expression tree. This feature is discussed in Chapter 13, “Language Integrated Query.”

## Events

Events are based on delegates and offer a publish/subscribe mechanism to delegates. You can find events everywhere across the framework. In Windows applications, the Button class offers the Click event. This type of event is a delegate. A handler method that is invoked when the Click event is fired needs to be defined, with the parameters as defined by the delegate type.

In the code example shown in this section, events are used to connect the CarDealer and Consumer classes. The CarDealer class offers an event when a new car arrives. The Consumer class subscribes to the event to be informed when a new car arrives.

### Event Publisher

You start with a CarDealer class that offers a subscription based on events. CarDealer defines the event named NewCarInfo of type EventHandler<CarInfoEventArgs> with the event keyword. Inside the method NewCar, the event NewCarInfo is fired by invoking the method RaiseNewCarInfo. The implementation of this method verifies whether the delegate is not null and raises the event (code file EventsSample/CarDealer.cs):

```csharp
using static System.Console;
using System;

namespace Wrox.ProCSharp.Delegates
{
    public class CarInfoEventArgs: EventArgs
    {
        public CarInfoEventArgs(string car)
        {
            Car = car;
        }

        public string Car { get; }
    }

    public class CarDealer
    {
        public event EventHandler<CarInfoEventArgs> NewCarInfo;

        public void NewCar(string car)
        {
            WriteLine($"CarDealer, new car {car}");

            NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
```

> **NOTE** The null propagation operator ?. used in the previous example is new with C# 6. This operator is discussed in Chapter 8, “Operators and Casts.”

The class CarDealer offers the event NewCarInfo of type EventHandler<CarInfoEventArgs>. As a convention, events typically use methods with two parameters; the first parameter is an object and contains the sender of the event, and the second parameter provides information about the event. The second parameter is different for various event types. .NET 1.0 defined several hundred delegates for events for all different data types. That’s no longer necessary with the generic delegate EventHandler<T>. EventHandler<TEventArgs> defines a handler that returns void and accepts two parameters. With EventHandler<TEventArgs>, the first parameter needs to be of type object, and the second parameter is of type T. EventHandler<TEventArgs> also defines a constraint on T; it must derive from the base class EventArgs, which is the case with CarInfoEventArgs:

```csharp
public event EventHandler<CarInfoEventArgs> NewCarInfo;
```

The delegate EventHandler<TEventArgs> is defined as follows:

```csharp
public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e)
    where TEventArgs : EventArgs;
```

Defining the event in one line is a C# shorthand notation. The compiler creates a variable of the delegate type EventHandler<CarInfoEventArgs> and adds methods to subscribe and unsubscribe from the delegate. The long form of the shorthand notation is shown next. This is very similar to auto-properties and full properties. With events, the add and remove keywords are used to add and remove a handler to the delegate:

```csharp
private EventHandler<CarInfoEventArgs> newCarInfo;
public event EventHandler<CarInfoEventArgs> NewCarInfo
{
    add
    {
        newCarInfo += value;
    }
    remove
    {
        newCarInfo -= value;
    }
}
```

> **NOTE** The long notation to define events is useful if more needs to be done than just adding and removing the event handler, such as adding synchronization for multiple thread access. The WPF controls make use of the long notation to add bubbling and tunneling functionality with the events. You can read more about event bubbling and tunneling events in Chapter 29, “Core XAML.”

The class `CarDealer` fires the event by calling the `Invoke` method of the delegate. This invokes all the handlers that are subscribed to the event. Remember, as previously shown with multicast delegates, the order of the methods invoked is not guaranteed. To have more control over calling the handler methods you can use the `Delegate` class method `GetInvocationList` to access every item in the delegate list and invoke each on its own, as shown earlier.

```csharp
NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
```

Firing the event is just a one-liner. However, this is only with C# 6. Previous to C# 6, firing the event was more complex. Here is the same functionality implemented before C# 6. Before firing the event, you need to check whether the event is null. Because between a null check and firing the event the event could be set to null by another thread, a local variable is used, as shown in the following example:

```csharp
EventHandler<CarInfoEventArgs> newCarInfo = NewCarInfo;
if (newCarInfo != null)
{
    newCarInfo(this, new CarInfoEventArgs(car));
}
```

With C# 6, all this could be replaced by using null propagation, with a single code line as you’ve seen earlier.

Before firing the event, it is necessary to check whether the delegate `NewCarInfo` is not `null`. If no one subscribed, the delegate is `null`:

```csharp
protected virtual void RaiseNewCarInfo(string car)
{
    NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
}
```

### Event Listener

The class `Consumer` is used as the event listener. This class subscribes to the event of the `CarDealer` and defines the method `NewCarIsHere` that in turn fulfills the requirements of the `EventHandler<CarInfoEventArgs>` delegate with parameters of type `object` and `CarInfoEventArgs` (code file `EventsSample/Consumer.cs`):

```csharp
using static System.Console;

namespace Wrox.ProCSharp.Delegates
{
    public class Consumer
```

With events, the publisher and listener are directly connected. This can be a problem with garbage collection. For example, if a listener is not directly referenced any more, there’s still a reference from the publisher. The garbage collector cannot clean up memory from the listener, as the publisher still holds a reference and fires events to the listener.

This strong connection can be resolved by using the weak event pattern and using the `WeakEventManager<T>` as an intermediary between the publisher and listeners.

The preceding example with the `CarDealer` as publisher and the `Consumer` as listener is modified in this section to use the weak event pattern.

The `WeakEventManager<T>` is defined within the `System.Windows` assembly that is not part of .NET Core. This sample is done with a .NET Framework 4.6 console application and does not run on other platforms.

> **NOTE** With subscribers that are created dynamically, in order to not be in danger of having resource leaks, you need to pay special attention to events. That is, you need to either ensure that you unsubscribe events before the subscribers go out of scope (are not needed any longer), or use weak events. Events often are a reason for memory leaks in applications because subscribers have a long-lived scope, and thus the source cannot be garbage collected as well.

Using weak events, the event publisher (in the sample code the `CarDealer` class) doesn’t need to be changed. No matter—if the tightly coupled events or weak events are used, the implementation is the same. What’s different is the implementation of the consumer. The consumer needs to implement the interface `IWeakEventListener`. This interface defines the method `ReceiveWeakEvent` that is called from the weak event manager when the event arrives. The method implementation acts as a proxy and in turn invokes the method `NewCarIsHere` (code file `WeakEvents/Consumer.cs`):

```csharp
using System;
using static System.Console;
using System.Windows;

namespace Wrox.ProCSharp.Delegates
{
    public class Consumer: IWeakEventListener
    {
        private string _name;

        public Consumer(string name)
        {
            this._name = name;
        }

        public void NewCarIsHere(object sender, CarInfoEventArgs e)
```
