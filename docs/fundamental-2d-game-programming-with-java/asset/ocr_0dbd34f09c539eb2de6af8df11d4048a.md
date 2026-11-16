```
public void fire() {
    put( EVENT_FIRE );
}

public void done() {
    put( EVENT_DONE );
}

protected void processEvent( String event ) throws InterruptedException {
    while( queue.peek() == EVENT_DONE || queue.peek() == EVENT_FIRE ) {
        event = queue.take();
    }

    if( currentState == STATE_CLOSED ) {
        if( event == EVENT_OPEN ) {
            audio.open();
            currentState = STATE_WAITING;
        }
    } else if( currentState == STATE_WAITING ) {
        if( event == EVENT_CLOSE ) {
            audio.close();
            currentState = STATE_CLOSED;
        }

        if( event == EVENT_FIRE ) {
            audio.loop( AudioStream.LOOP_CONTINUOUSLY );
            currentState = STATE_RUNNING;
        }
    } else if( currentState == STATE_RUNNING ) {
        if( event == EVENT_CLOSE ) {
            audio.stop();
            audio.close();
            currentState = STATE_CLOSED;
        }

        if( event == EVENT_DONE ) {
            audio.stop();
            currentState = STATE_WAITING;
        }
    }
}
```