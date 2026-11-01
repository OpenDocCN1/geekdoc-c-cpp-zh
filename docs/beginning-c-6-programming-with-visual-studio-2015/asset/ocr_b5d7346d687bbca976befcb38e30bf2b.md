```
myTimer.Start();
System.Threading.Thread.Sleep(200);
ReadKey();
}
static void WriteChar(object source, ElapsedEventArgs e)
{
    Write(displayString[counter++ % displayString.Length]);
}
}
}
```

3. Run the application (once it is running, pressing a key will terminate the application). The result, after a short period, is shown in Figure 13-5.

![](bbox=[0.1, 0.43, 0.78, 0.62])

FIGURE 13-5

# How It Works

The object you are using to raise events is an instance of the System.Timers.Timer class. This object is initialized with a time period (in milliseconds). When the Timer object is started using its Start() method, a stream of events is raised, spaced out in time according to the specified time period. Main() initializes a Timer object with a timer period of 100 milliseconds, so it will raise events 10 times a second when started:

```
static void Main(string[] args)
{
    Timer myTimer = new Timer(100);
}
```

The Timer object possesses an event called Elapsed, and the event handler required by this event must match the return type and parameters of the System.Timers.ElapsedEventHandler delegate type, which is one of the standard delegates defined in the .NET Framework. This delegate specifies the following return type and parameters:

void <MethodName>(object source, ElapsedEventArgs e);

The Timer object sends a reference to itself in the first parameter and an instance of an ElapsedEventArgs object in its second parameter. It is safe to ignore these parameters for now; you'll take a look at them a little later.