# THE QUICKRESTART CLASS

The QuickRestart class is similar to the last sound event update, allowing the sound to be opened and closed only once, instead of every time the sound is played. This class does not need the extra while loop to pull out events because the sound is restarted, which doesn't cause any queue issues.

```
package javagames.completegame.admin;

import javagames.sound.AudioStream;
import javagames.sound.SoundEvent;

public class QuickRestart extends SoundEvent {
    public static final String STATE_CLOSED = "closed";
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";

    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";
    public static final String EVENT_OPEN = "open";
    public static final String EVENT_CLOSE = "close";

    private String currentState;

    public QuickRestart( AudioStream stream ) {
        super( stream );
        currentState = STATE_CLOSED;
    }

    public void open() {
        put( EVENT_OPEN );
    }

    public void close() {
        put( EVENT_CLOSE );
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        System.out.println( "Quick Restart Got: " + event );
        System.out.println( "Current State: " + currentState );
        if( currentState == STATE_CLOSED ) {
            if( event == EVENT_OPEN ) {
                audio.open();
                currentState = STATE_WAITING;
            }
        }
    }
}
```