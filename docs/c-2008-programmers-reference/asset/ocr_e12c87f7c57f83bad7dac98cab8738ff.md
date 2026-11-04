Declare a Timer variable and define the AlarmTime property to allow users of this class to set a date and time:

```
class AlarmClock
{
    Timer t;
    public DateTime AlarmTime { get; set; }
}
```

Next, define the Start() method so that users can start the monitoring by turning on the Timer object:

```
class AlarmClock
{
    //...
    public void Start()
    {
        t.Start();
    }
}
```

Next, define a public event member in the AlarmClock class:

```
public event EventHandler TimesUp;
```

The EventHandler is a predefined delegate, and this statement defines TimesUp as an event for your class.

Define a protected virtual method in the AlarmClock class that will be used internally by your class to raise the TimesUp event:

```
protected virtual void onTimesUp(EventArgs e)
{
    if (TimesUp != null)
        TimesUp(this, e);
}
```

The EventArgs class is the base class for classes that contain event data. This class does not pass any data back to an event handler.

*The next section explains how you can create another class that derives from this EventArgs base class to pass back information to an event handler.*

Define the constructor for the AlarmClock class so that the Timer object (t) will fire its Elapsed event every 100 milliseconds. In addition, wire the Elapsed event with an event handler. The event