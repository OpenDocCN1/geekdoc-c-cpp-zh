Because the event itself has already been declared as public on the base class, it doesn’t make sense to try marking it as protected (which would imply no visibility from the outside) in an attempt to make the underlying field protected. So what’s the solution?

You should realize that the capability to raise an event is something that should be a highly privileged operation. When defining events in terms of delegate-typed events, you saw how improper exposure of the underlying delegate allows for spoofing attacks: anyone on the outside of the object can raise the event. In the face of subtyping, care should be taken, too. For this reason, you should explicitly design the type such that it allows an event to be raised from outside the bounds of the class itself (for example, on a subtype).

This calls for another pattern, namely the protected virtual On* method pattern. Let’s take a look at how the subtype would use it to raise an event first:

```
public void EmergencyStop() {
    // Cause a stop somehow; requires more extensibility
    // provided by the base class.

    OnFinished(EventArgs.Empty);
}
```

To enable a subtype to raise an event, we’ve drilled a little hole in the form of a protected method that contains the logic to raise the event. By making the method protected, only derived types (and not complete external strangers) can cause the event to be raised.

Besides this, we can also make the On* methods virtual so that subtypes can override them to provide additional steps to be taken when an event is raised (for example, to do some logging). To make this useful, we need to keep ourselves honest in the base class as well. (That is, we shouldn’t raise the event without making use of the On* methods.)

Adhering to those rules, our new CountDown class looks like this:

```
class CountDown {
    private uint _seconds;

    public CountDown(uint seconds) {
        _seconds = seconds;
    }

    public event EventHandler<TickEventArgs> Tick;
    public event EventHandler Finished;

    public void Start() {
        new Thread(() => {
            uint n = _seconds;
            while (n > 0u) {
                OnTick(new TickEventArgs(n));
                Thread.Sleep(1000);
```