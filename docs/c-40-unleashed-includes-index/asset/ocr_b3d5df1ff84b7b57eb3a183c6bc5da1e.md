use the static read-only EventArgs.Empty field. All in all, the changes made to the Start method with its embedded background thread procedure are fairly small:

```
public void Start() {
    new Thread(() => {
        uint n = _seconds;
        while (n > 0u) {
            var tick = Tick;
            if (tick != null) {
                tick(this, new TickEventArgs(n));
            }
            Thread.Sleep(1000);
            n--;
        }

        var finished = Finished;
        if (finished != null) {
            finished(this, EventArgs.Empty);
        }
    }).Start();
}
```

![](bbox=[0.1, 0.55, 0.75, 0.78])

FIGURE 18.19 Using EventHandler<T>.

As you should expect by now, for static events a null value for the sender argument is to be used.

Obviously, the use site needs to change, as well, to use the right signatures for the event handler methods. In the Tick event handler, we use the event arguments to obtain the number of elapsed seconds:

```
static void TickHandler(object sender, TickEventArgs e) {
    Console.WriteLine(e.Seconds);
}
```