```
queue.put( Event.DONE );
} catch ( InterruptedException e ) {
} };
} }
}
```

# THE MULTI-THREAD EVENT EXAMPLE

The MultiThreadEventExample, as shown in Figure 12.8 and located in the javagames.threads package, is a simple game loop that uses the three different state classes.

![](bbox=[0.1, 0.34, 0.55, 0.54])

Figure 12.8
Multi-Thread Event Example.
© 2014 Timothy Wright.

Each state machine is running in its own thread, using the blocking queue to communicate events from the game thread. Each event contains a BlockingHardware class that wraps the FakeHardware class and waits for those tasks that run in even more threads. While the game loop code is simple, there is a lot going on here. Time spent understanding the tools in this example is well spent.

```
package javagames.threads;
import java.awt.Graphics;
import java.awt.event.KeyEvent;
import javagames.util.SimpleFramework;
import javagames.util.Utility;
public class MultiThreadEventExample extends SimpleFramework {
```