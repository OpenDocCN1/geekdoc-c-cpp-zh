```
```java
public BlockingClip( byte[] soundData ) {
    super( soundData );
}

/**
 * This guy could throw a bunch of exceptions.
 * We're going to wrap them all in a custom exception
 * handler that is a RuntimeException so we don't
 * have to catch and throw all these exceptions.
 */
@Override
public void open() {
    lock.lock();
    try {
        ByteArrayInputStream in = new ByteArrayInputStream( soundData );
        AudioInputStream ais = AudioSystem.getAudioInputStream( in );
        clip = AudioSystem.getClip();
        clip.addLineListener( this );
        clip.open( ais );
        while ( !open ) {
            cond.await();
        }
    } catch ( UnsupportedAudioFileException ex ) {
        throw new SoundException( ex.getMessage(), ex );
    } catch ( LineUnavailableException ex ) {
        throw new SoundException( ex.getMessage(), ex );
    } catch ( IOException ex ) {
        throw new SoundException( ex.getMessage(), ex );
    } catch ( InterruptedException ex ) {
        ex.printStackTrace();
    } finally {
        lock.unlock();
    }
}

@Override
public void start() {
    lock.lock();
    try {
        clip.flush();
        clip.setFramePosition( 0 );
        clip.start();
```
```