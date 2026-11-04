In similar fashion, the delegate strDel is created and assigned a reference to Reflect():

```
SomeOp<string> strDel = Reflect;
```

Because Reflect() takes a string argument and returns a string result, it is compatible with the string version of SomeOp.

Because of the type safety inherent in generics, you cannot assign incompatible methods to delegates. For example, assuming the preceding program, the following statement would be in error:

```
SomeOp<int> intDel = Reflect; // Error!
```

Because Reflect() takes a string argument and returns a string result, it cannot be assigned to an int version of SomeOp.

As explained in Chapter 15, one of the major uses of delegates occurs when handling events. Although events, themselves, cannot be generic, the delegate that supports an event can. The following program reworks an example from Chapter 15 (the .NET-compatible event demonstration) so that it uses a generic delegate:

```
// Convert event example from Chapter 15 to use generic delegate.

using System;

// Derive a class from EventArgs.
class MyEventArgs : EventArgs {
  public int EventNum;
}

// Declare a generic delegate for an event.
delegate void MyEventHandler<T, V>(T source, V args);

// Declare an event class.
class MyEvent {
  static int count = 0;

  public event MyEventHandler<MyEvent, MyEventArgs> SomeEvent;

  // This fires SomeEvent.
  public void OnSomeEvent() {
    MyEventArgs arg = new MyEventArgs();

    if(SomeEvent != null) {
      arg.EventNum = count++;
      SomeEvent(this, arg);
    }
  }
}

class X {
  public void Handler<T, V>(T source, V arg) where V : MyEventArgs {
    Console.WriteLine("Event " + arg.EventNum +
      " received by an X object.");
  }
```