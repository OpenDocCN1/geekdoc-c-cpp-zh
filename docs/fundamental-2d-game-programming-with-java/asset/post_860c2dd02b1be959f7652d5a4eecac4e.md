
```java
@Override
public void open() {
    lock.lock();
    try {
        stream = new AudioDataLine( soundData );
        stream.initialize();
        stream.addLineListener( this );
        stream.open();
        while ( !open ) {
            cond.await();
        }
        System.out.println( "open" );
    } catch( InterruptedException ex ) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}

@Override
public void start() {
    lock.lock();
    try {
        stream.start();
        while ( !started ) {
            cond.await();
        }
        System.out.println( "started" );
    } catch( InterruptedException ex ) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}

@Override
public void loop( int count ) {
    lock.lock();
    try {
        stream.loop( count );
        while ( !started ) {
            cond.await();
        }
        System.out.println( "started" );
    } catch( InterruptedException ex ) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}

@Override
public void restart() {
    stream.reset();
}

@Override
public void stop() {
    lock.lock();
    try {
        stream.stop();
        while(started) {
            cond.await();
        }
        System.out.println("stopped");
    } catch(InterruptedException ex) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}

@Override
public void close() {
    lock.lock();
    try {
        stream.close();
        while(open) {
            cond.await();
        }
        System.out.println("closed");
    } catch( InterruptedException ex ) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}
```

## CREATING A SOUNDEVENT CLASS

Luckily, perhaps by design, this issue was also covered in Chapter 12. By using the blocking queue method, you can create a SoundEvent class that runs in another thread off the game loop and processes sound events in a single threaded queue. Refer to the BlockingQueueExample in Chapter 12 for a detailed explanation of using the blocking queue to communicate between threads.

```java
package javagames.sound;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

public class SoundEvent implements Runnable {
    public static final String SHUT_DOWN = "shutdown";
    protected AudioStream audio;
    protected BlockingQueue<String> queue;
    private Thread consumer;
    public SoundEvent( AudioStream audio ) {
        this.audio = audio;
    }
    public void initialize() {
        audio.addListener( getListener() );
        queue = new LinkedBlockingQueue<String>();
        consumer = new Thread( this );
        consumer.start();
    }
    public void put( String event ) {
        try {
            queue.put( event );
        } catch( InterruptedException e ) { }
    }
    public void shutDown() {
        Thread temp = consumer;
        consumer = null;
        try {
            // send event to wake up consumer
            // and/or stop.
            queue.put( SHUT_DOWN );
            temp.join( 1000L );
            System.out.println( "Event shutdown!!!" );
        } catch( InterruptedException ex ) { }
    }

    @Override
    public void run() {
        while (Thread.currentThread() == consumer) {
            try {
                processEvent( queue.take() );
            } catch( InterruptedException e ) {
            }
        }
    }

    protected void processEvent( String event )
    throws InterruptedException { }

    protected void onAudioFinished() { }

    private BlockingAudioListener getListener() {
        return new BlockingAudioListener() {
            @Override
            public void audioFinished() {
                onAudioFinished();
            }
        };
    }
}
```

## USING THE ONESHOTEVENT CLASS

The OneShotEvent, as shown in Figure 13.3 and located in the javax.sound package, has two states—WAITING and RUNNING—and two events—FIRE and DONE.

![](img/588a4cda8f2acae94a7e1987bf99400d_427_0.png)

Figure 13.3 One Shot Event. © 2014 Timothy Wright.

If the OneShotEvent is waiting, the fire event starts playing the sound. The fire event does nothing while the sound is playing. The DONE event will stop the sound, or the sound will stop when it is finished playing. This state machine concept is explored in detail in Chapter 12.

```java
package javagames.sound;

public class OneShotEvent extends SoundEvent {
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";
    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";

    private String currentState;

    public OneShotEvent( AudioStream audio ) {
        super( audio );
        currentState = STATE_WAITING;
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    public void done() {
        put( EVENT_DONE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        System.out.println( "Got " + event + " event" );
        if ( currentState == STATE_WAITING ) {
            if ( event == EVENT_FIRE ) {
                audio.open();
                audio.start();
                currentState = STATE_RUNNING;
            }
        } else if ( currentState == STATE_RUNNING ) {
            if ( event == EVENT_DONE ) {
                audio.stop();
                audio.close();
                currentState = STATE_WAITING;
            }
        }
    }

    @Override
    protected void onAudioFinished() {
        put( EVENT_DONE );
    }
}
```

## USING THE LOOPEVENT CLASS

The LoopEvent, as shown in Figure 13.4 and located in the same package, is very similar to the OneShotEvent.

![](img/588a4cda8f2acae94a7e1987bf99400d_429_0.png)

Figure 13.4 Loop Event. © 2014 Timothy Wright.

The only difference is that the sound keeps repeating until the DONE method is called. This event does not stop by itself.

```java
package javagames.sound;

public class LoopEvent extends SoundEvent {
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";
    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";

    private String currentState;

    public LoopEvent( AudioStream audio ) {
        super( audio );
        currentState = STATE_WAITING;
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    public void done() {
        put( EVENT_DONE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        System.out.println( "Got " + event + " event" );
        if ( currentState == STATE_WAITING ) {
            if( event == EVENT_FIRE ) {
                audio.open();
                audio.loop( AudioStream.LOOP_CONTINUOUSLY );
                currentState = STATE_RUNNING;
            }
        } else if( currentState == STATE_RUNNING ) {
            if( event == EVENT_DONE ) {
                audio.stop();
                audio.close();
                currentState = STATE_WAITING;
            }
        }
    }
}
```

## USING THE RESTARTEVENT CLASS

The RestartEvent, as shown in Figure 13.5, plays the sound only once, but another fire event issued while the sound is playing will restart the sound.

![](img/588a4cda8f2acae94a7e1987bf99400d_430_0.png)

Figure 13.5 Restart Event. © 2014 Timothy Wright.

```java
package javagames.sound;

public class RestartEvent extends SoundEvent {
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";
    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";
    private String currentState;

    public RestartEvent( AudioStream stream ) {
        super( stream );
        currentState = STATE_WAITING;
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        System.out.println( "Got " + event + " event" );
        if ( currentState == STATE_WAITING ) {
            if( event == EVENT_FIRE ) {
                currentState = STATE_RUNNING;
                audio.open();
                audio.start();
            }
        } else if ( currentState == STATE_RUNNING ) {
            if( event == EVENT_FIRE ) {
                audio.restart();
            }

            if( event == EVENT_DONE ) {
                currentState = STATE_WAITING;
                audio.close();
            }
        }
    }

    @Override
    protected void onAudioFinished() {
        put( EVENT_DONE );
    }
}
```
