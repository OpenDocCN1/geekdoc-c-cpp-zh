
```java
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

## USING THE BLOCKING CLIP CLASS

The BlockingClip class extends the AudioStream base class and provides implementations for the following abstract methods:

- open
- close
- start
- stop
- restart
- loop

Each of these methods that has to block when the Clip object performs the task has the following signature:

```
lock.lock();
try {
```

// use clip
while( ! finished ) {
    cond.await();
}
} finally {
    lock.unlock();
}
```

As explained in Chapter 12, the lock is acquired before requesting that the clip perform some action, and then waits for a response, always unlocking in a try/finally block. This ensures that the lock is released no matter what happens in the method.

The open() method creates the AudioInputStream, obtains a Clip from the AudioSystem, adds itself as a LineListener, opens the clip, and blocks until the LineListener interface receives the LineEvent.OPEN event. Notice all the exceptions—UnsupportedAudioFileException, LineUnavailableException, and IOException—that are wrapped with the custom sound exception. This makes the class a lot easier to use.

The start() method clears the clip of any remaining data with flush(), sets the frame position to zero, starts the Clip, and waits for the LineEvent.START event before returning.

The loop() method is similar to start, but uses the Clip.loop() method to pass in a loop count. Using the AudioStream.LOOP_CONTINUOUSLY flag will allow the sound to loop forever.

The stop() method stops the Clip and waits for the LineEvent.STOP event. It does not need to drain the line first. The Clip class will play until the sound is finished and then call the BlockingAudio.audioFinished() method.

The restart() method is tricky. It overrides the fireTaskFinished() method, suppressing the event so that when the sound is stopped and started again, and the LineEvent.STOP event is received, the fireTaskFinished() will not incorrectly notify listeners that the task has stopped when it was only restarted.

The close() method closes the Clip and waits for the LineEvent.CLOSE event before returning.

```java
package javagames.sound;
import java.io.*;
import javax.sound.sampled.*;
public class BlockingClip extends AudioStream {
    private Clip clip;
    private boolean restart;

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
            while( !started ) {
                cond.await();
            }
            System.out.println( "It's Started" );
        } catch( InterruptedException e ) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    @Override
    public void loop( int count ) {
        lock.lock();
        try {
            clip.flush();
            clip.setFramePosition( 0 );
            clip.loop( count );
            while( !started ) {
                cond.await();
            }
            System.out.println( "It's Started" );
        } catch( InterruptedException e ) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    @Override
    public void restart() {
        restart = true;
        stop();
        restart = false;
        start();
    }

    @Override
    protected void fireTaskFinished() {
        if( !restart ) {
            super.fireTaskFinished();
        }
    }

    @Override
    public void stop() {
        lock.lock();
        try {
            clip.stop();
            while (started) {
                cond.await();
            }
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    @Override
    public void close() {
        lock.lock();
        try {
            clip.close();
            while (open) {
                cond.await();
            }
            clip = null;
            System.out.println("Turned off");
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```

## USING THE AUDIODATALINE CLASS

The next thing you need to do for the sound library is to create a BlockingDataLine class so sounds can be streamed by hand. Keep in mind that there are behavior differences between the 6.0 SDK and the 7.0 SDK. While the Clip class cannot load large files in 6.0, they can be loaded and played with 7.0. However, while smaller clips work better in 6.0, using them in 7.0 can cause the short sounds to stop working. So regardless of which version you support, the ability to stream sounds by hand is necessary.

The AudioDataLine class, located in the javax.sound.sampled package, is similar to the Clip class but it can stream large sound files. One of the issues with playing sounds this way is that the sound data needs to be written to the SourceDataLine in byte chunks. To do this, the actual audio data must be extracted from the AudioInputStream. The raw sound file cannot be played or the file header information will be interpreted as sound data. I tried it and it doesn't sound good. There is a lot of cracking and popping.

The sound data can be extracted from the AudioInputStream in frames. It is not possible to read the data one byte at a time unless each frame is only one byte in length.

```
InputStream soundFile = loadSoundFile();
byte[] rawBytes = readBytes( soundFile );

ByteArrayInputStream in = new ByteArrayInputStream( rawBytes );
AudioInputStream audioInputStream =
AudioSystem.getAudioInputStream( in );
AudioFormat audioFormat = audioInputStream.getFormat();
ByteArrayOutputStream out = new ByteArrayOutputStream();
int chunk = (int)audioFormat.getFrameSize();
byte[] buf = new byte[ chunk ];
while ( audioInputStream.read( buf ) != -1 ) {
out.write( buf );
}
audioInputStream.close();
byte[] soundBytes = out.toByteArray();
```

Another issue with streaming data to a SourceDataLine from scratch is the buffer size. Unlike a Clip, the data written to the SourceDataLine should be drained before the sound is stopped. In order to have quick response, the buffer must be small; a 50-millisecond buffer seems to work well. Because sounds have different sample sizes, channels, and bit sample sizes, calculating a 50-millisecond buffer in bytes requires some work.

The computeBufferSize() method uses the buffer length in milliseconds, the sample size, number of sample bits, and number of channels to create a buffer of the correct size in bytes.

frame size = \frac{sample rate Hz}{1000} * milliseconds

The number of frames for a 50-millisecond sample is computed by converting the sample rate into milliseconds. You do this by dividing it by 1,000 and then multiplying by the desired number of milliseconds.
