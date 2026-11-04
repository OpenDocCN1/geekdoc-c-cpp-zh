Assuming both the egg timer and the chronometer are implemented using the same countdown mechanism on the inside, both the interactive parts and reactive parts are surfaced quite differently. For example, starting the timer involves releasing the egg timer's rotating top half; the chronometer needs a button press. Those actions are “interactive.” We're in the driver's seat and give a signal to start the countdown mechanism.

On the reactive side, things are also different. When the countdown reaches zero, the egg timer reacts by ringing a bell. The chronometer, on the other hand, isn't really interested in this event because it doesn't provide a special notification about reaching zero to the user. Because no further time-elapsed events would be raised by the inner countdown mechanism, the little arrow will keep pointing upward to the 60 (which equals 0 in clock arithmetic, of course) indicator.

Our task is to provide a general-purpose countdown mechanism that can be embedded in both an egg timer and a chronometer. (You're invited to think about other uses.) And guess what? To realize the reactive parts, we'll use events. For now, we start by using simple delegates and refine the solution toward the use of C# events later.

# Using Delegates

To realize our countdown mechanism in code, let's build a CountDown class that gets initialized with the number of seconds to countdown. This part leads to the following obvious skeleton code:

```
```csharp
class CountDown {
    private uint _seconds;

    public CountDown(uint seconds) {
        _seconds = seconds;
    }
}
```
```

Next, we need to separate two concerns: the parts dealing with interactive user actions versus the ones that have a reactive nature. We already know how to realize interactive concepts by means of regular methods. In fact, we did so for the timer's initialization by the definition of a constructor (the method to be called to create a countdown). Besides this, we need a method to start the countdown:

```
```csharp
public void Start() {
    uint n = _seconds;
    while (n > 0u) {
        // TODO: let the user know one second has ticked away
        Thread.Sleep(1000);
    }
    // TODO: let the user know we've reached zero
}
```
```