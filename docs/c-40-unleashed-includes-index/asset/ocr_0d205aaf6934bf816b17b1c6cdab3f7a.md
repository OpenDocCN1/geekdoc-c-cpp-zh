as far as stating that this allows a denial-of-service attack because one client can overwrite all event handlers hooked up by other clients;

```
// Malicious chronometer overwriting the Tick delegate altogether
countDown.Tick = currentSecond => MoveHand(currentSecond);
```

This is not the only problem, though. Raising an event should really be a privileged operation that can be performed only by the event source. But by giving users a way to retrieve, through the property getter, the multicast delegate containing the hooked event handlers, everyone who can get a hold on it can raise the event:

```
// Egg timer listening to the countdown
countDown.Tick += currentSecond => TurnSpindle(6 /* degrees */);
countDown.Finished += () => Ring();

// Evil jealous chronometer that wants to take revenge on our nice egg timer
uint n = 0;
while (true) {
    countDown.Tick(n); // Chronometer raises the event from the outside!
    n = (n + 1) % 60;
}
```

In the preceding code fragment, an evil chronometer gets a hold of the Tick delegate to which the egg timer has attached a handler. Evil as it is, it starts raising the Tick event by invoking the delegate in a tight infinite loop. A little calculation shows that at a rate of one Tick invocation every 20 nanoseconds (not unrealistic at all), our poor egg timer will start rotating at a daunting speed of 833,333 rotations per second. You don't want to be in the same room as the egg timer under attack!

Both problems outlined here are at the level of trust between two parties: the event source versus its consumers. One ill-behaved consumer can make life pretty bad for its peer consumers as well as the event source. On the technical field, we can attribute this problem to the fact we're allowing unrestricted access to the multicast delegate used for the event. In other words, our use of a property is not quite ideal.

All those reasons were among the key motivations why events were introduced as a first-class concept in .NET in general and in the C# language specifically. Let's take a look at how the CountDown code would look if we use events instead.

# Using .NET Events

Events are just delegates in disguise but provide additional levels of protection against the attacks we've seen previously. Syntactically, very little has to change:

```
class CountDown {
    private uint _seconds;
```