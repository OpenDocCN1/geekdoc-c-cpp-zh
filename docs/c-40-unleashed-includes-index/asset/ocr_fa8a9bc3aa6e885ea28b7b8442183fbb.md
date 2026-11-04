Ignore the “to do” notes for the time being. The preceding code realizes the core engine of the countdown as a simple whole loop. There’s a problem, though: The Start method blocks upon calling it, sitting in the while loop for the duration specified by the timer. It would be more desirable for the Start call to be asynchronous, so let’s introduce a background thread on which the timer will tick:

```
public void Start() {
    new Thread(() => {
        uint n = _seconds;
        while (n > 0u) {
            // TODO: let the user know one second has ticked away
            Thread.Sleep(1000);
            n--;
        }
        // TODO: let the user know we've reached zero
    }).Start();
}
```

Feel free to refactor the preceding code if you don’t like the use of a lambda expression for substantial amounts of code, but that’s merely a matter of taste. What’s more important is that the Start method now returns immediately, with the timer ticking on a separate thread.

Now to the heart of our mission: how to fill in the gaps left by our “to do” notes, used to inform the user about certain events. Because we want to keep our countdown mechanism generic, we can’t hard code the actions to be taken whenever an event occurs. Instead, we’ll have the user supply callback procedures, or with more appropriate wording, event handlers, through delegates. To do so, let’s introduce two more properties of a delegate type:

```
public Action<uint> Tick { get; set; }
public Action Finished { get; set; }
```

With the preceding in place, you can use the CountDown class as follows:

```
var countDown = new CountDown(5);

// Hook up event handlers
countDown.Tick = currentSecond => Console.WriteLine(currentSecond);
countDown.Finished = () => Console.Beep();

countDown.Start();
```

The two property assignments, later to be replaced by event handler registrations, are the means for the user to specify how a Tick event and a Finished event should be dealt with.