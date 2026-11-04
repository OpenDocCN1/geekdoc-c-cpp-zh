# TimedEvent.cs

TimedEvent.cs is a class representing a timer; it is used to monitor events based on a set number of processing cycles. It can monitor that an event happens a set number of times, etc. Deriving from this class and overriding the Tick() method can allow for custom behavior (see Example 5.75).

# Example 5.75. TimedEvent.cs

```
```csharp
using System;

namespace GameClasses {
    public delegate void TickHandler(TimedEvent e, Object payload);

    public class TimedEvent {
        // Member fields
        public int ticks;
        public int tickCounter;
        public bool isCountdown;
        public bool isActive;
        public TickHandler remoteHandler;
        public object payload;

        public TimedEvent() {
            ticks = 0;
            isCountdown = false;
            SetTickHandler(new TickHandler(DoNothing));
        }

        public TimedEvent(TickHandler handler) {
            SetTickHandler(handler);
        }

        public TimedEvent(int numTicks, TickHandler handler) {
            SetCountdown(numTicks);
            SetTickHandler(handler);
        }

        public void SetTickHandler(TickHandler handler) {
            remoteHandler = handler;
        }
    }
```
```