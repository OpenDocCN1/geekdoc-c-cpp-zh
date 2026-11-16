+   lockInterruptibly()—The synchronized block in the wait/notify method does not respond to thread interruption. This method blocks until the lock is acquired, but will return with an exception if the Lock object is interrupted.

In addition, the Condition object has timeout values available for the await() methods as well as this method:

+   awaitUninterruptibly()—This method will wait for notification and not respond to thread interruption.

Another feature is multiple lock types. ReentrantLock can be created with a fairness policy so the lock acquisition is granted to the thread that has been waiting the longest. There is also a ReadWriteLock that maintains two different locks so that while only one thread can write to the object at a time, many threads can read.

The BlockingHardwareListener interface, located in the javagames.threads package, is used for event notification when the hardware task is finished.

```
package javagames.threads;

public interface BlockingHardwareListener {
    public void taskFinished();
}
```

The BlockingHardware class maintains a list of listeners and notifies the listeners when the hardware task is complete. The BlockingHardware also maintains its own state variables in case the FakeHardware class state doesn't match reality.

The turnOn(), turnOff(), start(), and stop() methods all block using the Lock/Condition objects. This makes the FakeHardware class easier to use in a single threaded loop, like a game loop, and keeps the chance of race conditions and deadlock bugs to a minimum.

```
package javagames.threads;
import java.util.*;
import java.util.concurrent.locks.*;
import javagames.threads.FakeHardware.FakeHardwareEvent;
```

```
public class BlockingHardware {
    private final Lock lock = new ReentrantLock();
    private final Condition cond = lock.newCondition();
```