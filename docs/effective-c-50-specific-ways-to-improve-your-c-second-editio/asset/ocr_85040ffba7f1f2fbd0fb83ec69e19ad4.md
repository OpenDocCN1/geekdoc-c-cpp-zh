```
```csharp
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
```
```

The first solution is preferred. This may seem surprising given the emphasis on declarative code in WPF applications. Even so, if the logic must be implemented in code, you should use the virtual method. If an event handler throws an exception, no other handlers in the chain for that event are called (see Items 24 and 25). Some other ill-formed code prevents the system from calling your event handler. By overriding the protected virtual function, your handler gets called first. The base class version of the virtual function is responsible for calling any event handlers attached to the particular event. That means that if you want the event handlers called (and you almost always do), you must call the base class. In some rare cases, you will want to replace the default behavior instead of calling the base class version so that none of the event handlers gets called. You can’t guarantee that all the event handlers will be called because some ill-formed event handler might throw an exception, but you can guarantee that your derived class’s behavior is correct.

Using the override is more efficient than attaching the event handler. You will remember from Item 25 that events are built on top of multicast delegates. That enables any event source to have multiple observers. The event-handling mechanism takes more work for the processor because it must examine the event to see if any event handlers have been attached. If so, it must iterate the entire invocation list, which may contain any number of target methods. Each method in the event invocation list must be