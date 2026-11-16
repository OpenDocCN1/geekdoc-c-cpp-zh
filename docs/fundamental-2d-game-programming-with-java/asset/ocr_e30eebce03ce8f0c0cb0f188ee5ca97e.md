```
```java
private List<BlockingAudioListener> listeners =
    Collections.synchronizedList(
        new ArrayList<BlockingAudioListener>() );
public AudioStream( byte[] soundData ) {
    this.soundData = soundData;
}
public abstract void open();
public abstract void close();
public abstract void start();
public abstract void loop( int count );
public abstract void restart();
public abstract void stop();
public boolean addListener( BlockingAudioListener listener ) {
    return listeners.add( listener );
}
protected void fireTaskFinished() {
    synchronized( listeners ) {
    for( BlockingAudioListener listener : listeners ) {
        listener.audioFinished();
    }
    }
}
@Override
public void update( LineEvent event ) {
    boolean wasStarted = started;
    lock.lock();
    try {
    if( event.getType() == Type.OPEN ) {
        open = true;
    } else if( event.getType() == Type.CLOSE ) {
        open = false;
    } else if( event.getType() == Type.START ) {
        started = true;
    } else if( event.getType() == Type.STOP ) {
        started = false;
    }
    cond.signalAll();
    } finally {
    lock.unlock();
    }
}
```
```