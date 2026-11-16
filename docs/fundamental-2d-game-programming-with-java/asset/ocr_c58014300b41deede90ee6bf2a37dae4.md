```
@Override
public void update (LineEvent event ) {
boolean wasStarted = started;
lock.lock();
try {
if ( event.getType() == Type.OPEN ) {
open = true;
} else if ( event.getType() == Type.CLOSE ) {
open = false;
} else if ( event.getType() == Type.START ) {
started = true;
} else if ( event.getType() == Type.STOP ) {
started = false;
}
cond.signalAll();
} finally {
lock.unlock();
}
if ( wasStarted && !started ) {
fireTaskFinished();
}
}
}
```

# USING THE BLOCKING CLIP CLASS

The BlockingClip class extends the AudioStream base class and provides implementations for the following abstract methods:

+   - open
+   - close
+   - start
+   - stop
+   - restart
+   - loop

Each of these methods that has to block when the Clip object performs the task has the following signature:

```
lock.lock();
try {
```