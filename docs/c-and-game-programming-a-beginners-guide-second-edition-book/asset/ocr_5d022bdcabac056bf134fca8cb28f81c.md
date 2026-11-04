# GameTimer.cs

The GameTimer Class serves as a gauge for the game's events; for example, an event can be added, timed, or removed—addEvent, TimedEvent, and removeEvent. The game relies on the timed events to allow for actions not controlled by the player (see Example 5.74 and GameTimer.cs on the CD-ROM).

# Example 5.74. GameTimer.cs

```
```csharp
using System;
using System.Windows.Forms;
using System.Collections;

namespace GameClasses {
    public class GameTimer {
        // Member fields
        Timer gameTimer;  // main timer object
        int baseInterval; // base interval in ms
        Hashtable events; // list of TimedEvent objects

        // Default constructor
        public GameTimer(int interval) {
            events = new Hashtable();
            gameTimer = new Timer();
            gameTimer.Interval = interval;
            gameTimer.Tick += new EventHandler(Tick);
            baseInterval = interval;
        }

        // Simple start and stop functionality.
        public void Start() {gameTimer.Start();}
        public void Stop() {gameTimer.Stop();}

        // Add an event to our game timer. Use stepFactor to control the
        // frequency the given TimedEvent's Tick() will be called.
        // Use the given "key" for future reference to this TimedEvent.
        public void addEvent(TimedEvent timedEvent, int stepFactor,
            string key) {
            TimedEventNode node = new TimedEventNode();
            node.data = timedEvent;
            node.timeStep = stepFactor;
```
```