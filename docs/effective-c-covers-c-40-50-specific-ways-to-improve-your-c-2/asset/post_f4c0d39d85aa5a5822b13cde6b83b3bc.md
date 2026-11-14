
You write a nifty Windows Presentation Foundation (WPF) application that needs to respond to mouse down events. In your form class, you can choose to override the OnMouseDown() method:

```
public partial class Window1 : Window
{
    // other code elided

    public Window1()
    {
        InitializeComponent();
    }

    protected override void OnMouseDown(
        MouseButtonEventArgs e)
    {
        DoMouseThings(e);
        base.OnMouseDown(e);
    }
}
```

Or, you could attach an event handler (which requires both C# and XAML):

```
<!-- XAML File -->
<Window x:Class="Item36_OverridesAndEvent.Window1"
    xmlns=
    "http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Window" Height="300" Width="300"
    MouseDown="OnMouseDown">
    <Grid>
    </Grid>
</Window>
```

// C Sharp file:

```
public partial class Window1 : Window
{
    // other code elided

    public Window1()
    {
        InitializeComponent();
    }

    private void OnMouseDown(object sender,
        MouseButtonEventArgs e)
    {
        DoMouseThings(e);
    }

    private void DoMouseThings(MouseButtonEventArgs e)
    {
        throw new NotImplementedException();
    }
}
```

The first solution is preferred. This may seem surprising given the emphasis on declarative code in WPF applications. Even so, if the logic must be implemented in code, you should use the virtual method. If an event handler throws an exception, no other handlers in the chain for that event are called (see Items 24 and 25). Some other ill-formed code prevents the system from calling your event handler. By overriding the protected virtual function, your handler gets called first. The base class version of the virtual function is responsible for calling any event handlers attached to the particular event. That means that if you want the event handlers called (and you almost always do), you must call the base class. In some rare cases, you will want to replace the default behavior instead of calling the base class version so that none of the event handlers gets called. You can't guarantee that all event handlers will be called because some ill-formed event handler might throw an exception, but you can guarantee that your derived class's behavior is correct.

Using the override is more efficient than attaching the event handler. You will remember from Item 25 that events are built on top of multicast delegates. That enables any event source to have multiple observers. The event-handling mechanism takes more work for the processor because it must examine the event to see if any event handlers have been attached. If so, it must iterate the entire invocation list, which may contain any number of target methods. Each method in the event invocation list must be called. Determining whether there are event handlers and iterating each at runtime takes more execution time than invoking one virtual function.

If that's not enough for you, examine the first listing in this item again. Which is clearer? Overriding a virtual function has one function to examine and modify if you need to maintain the form. The event mechanism has two points to maintain: the event handler function and the code that wires up the event. Either of these could be the point of failure. One function is simpler.

Okay, I've been giving all these reasons to use the overrides and not use the event handlers. The .NET Framework designers must have added events for a reason, right? Of course they did. Like the rest of us, they're too busy to write code nobody uses. The overrides are for derived classes. Every other class must use the event mechanism. That also means declarative actions defined in the XAML file will be accessed through the event handlers. In this example, your designer may have actions that are supposed to occur on a MouseDown event. The designer will create XAML declarations for those behaviors. Those behaviors will be accessed using events on the form. You could redefine all that behavior in your code, but that's way too much work to handle one event. It only moves the problem from the designer's hands to yours. You clearly want designers doing design work instead of you. The obvious way to handle that is to create an event and access the XAML declarations created by a design tool. So, in the end, you have created a new class to send an event to the form class. It would be simpler to just attach the form's event handler to the form in the first place. After all, that's why the .NET Framework designers put those events in the forms.

Another reason for the event mechanism is that events are wired up at runtime. You have more flexibility using events. You can wire up different event handlers, depending on the circumstances of the program. Suppose that you write a drawing program. Depending on the state of the program, a mouse down might start drawing a line, or it might select an object. When the user switches modes, you can switch event handlers. Different classes, with different event handlers, handle the event depending on the state of the application.

Finally, with events, you can hook up multiple event handlers to the same event. Imagine the same drawing program again. You might have multiple event handlers hooked up on the MouseDown event. The first would perform the particular action. The second might update the status bar or update the accessibility of different commands. Multiple actions can take place in response to the same event.

When you have one function that handles one event in a derived class, the override is the better approach. It is easier to maintain, more likely to be correct over time, and more efficient. Reserve the event handlers for other uses. Prefer overriding the base class implementation to attaching an event handler.

## Item 31: Implement Ordering Relations with IComparable<T> and IComparer<T>

Your types need ordering relationships to describe how collections should be sorted and searched. The .NET Framework defines two interfaces that describe ordering relationships in your types: IComparable<T> and IComparer<T>. IComparable defines the natural order for your types. A type implements IComparer to describe alternative orderings. You can define your own implementations of the relational operators (<, >, <=, >=) to provide type-specific comparisons, to avoid some runtime inefficiencies in the interface implementations. This item discusses how to implement ordering relations so that the core .NET Framework orders your types through the defined interfaces and so that other users get the best performance from these operations.

The IComparable interface contains one method: CompareTo(). This method follows the long-standing tradition started with the C library function strcmp: Its return value is less than 0 if the current object is less than the comparison object, 0 if they are equal, and greater than 0 if the current object is greater than the comparison object. IComparable<T> will be used by most newer APIs in the .NET landscape. However, some older APIs will use the classic IComparable interface. Therefore, when you implement IComparable<T>, you should also implement IComparable. IComparable takes parameters of type System.Object. You need to perform runtime type checking on the argument to this function. Every time comparisons are performed, you must reinterpret the type of the argument:

```
public struct Customer : IComparable<Customer>, IComparable
{
    private readonly string name;

    public Customer(string name)
    {
        this.name = name;
    }
}
```

```
#region IComparable<Customer> Members
public int CompareTo(Customer other)
{
    return name.CompareTo(other.name);
}
#endregion
```

```
#region IComparable Members
int IComparable.CompareTo(object obj)
{
    if (!(obj is Customer))
    throw new ArgumentException(
    "Argument is not a Customer", "obj");
    Customer otherCustomer = (Customer)obj;
    return this.CompareTo(otherCustomer);
}
#endregion
```

Notice that IComparable is explicitly implemented in this structure. That ensures that the only code that will call the object-typed version of CompareTo() is code that was written for the previous interface. There's just too much to dislike about the classic version of IComparable. You've got to check the runtime type of the argument. Incorrect code could legally call this method with anything as the argument to the CompareTo method. More so, proper arguments must be boxed and unboxed to provide the actual comparison. That's an extra runtime expense for each compare. Sorting a collection will make, on average n lg(n) comparisons of your objects using the IComparable.Compare method. Each of those will cause three boxing and unboxing operations. For an array with 1,000 points, that will be more than 20,000 boxing and unboxing operations, on average: n lg(n) is almost 7,000, and there are 3 box and unbox operations per comparison.

You may be wondering why you should implement the nongeneric IComparable interface at all. There are two reasons. First, there's simple backward compatibility. Your types will interact with code created before
