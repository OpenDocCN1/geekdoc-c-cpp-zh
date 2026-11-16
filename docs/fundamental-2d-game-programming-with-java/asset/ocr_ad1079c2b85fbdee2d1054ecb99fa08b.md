```
} finally {
    System.out.println( "Stream finished" );
    dataLine.drain();
    dataLine.stop();
}
}
}
```

# CREATING THE BLOCKINGDATALINE CLASS

Now that the AudioDataStream wraps a SourceDataLine and provides a similar class as the Clip class, a BlockingDataLine can be created that waits for the sound events before returning. This creates blocking classes for small and large sound files.

The BlockingDataLine uses the same structure as the BlockClip.

```
Lock.lock();
try {
    // use clip
    while( not finished ) {
        cond.wait();
    }
} finally {
    Lock.unlock();
}
```

The open() method creates a new AudioDataLine, adds a LineListener, opens the stream, and blocks until it is complete. The start() method starts the stream and waits until data has begun streaming before returning. The loop() method does the same.

The restart() method forwards the request to the AudioDataLine. The stop() method stops the stream and waits for the stop() event before returning. The close() method closes the stream.

```
package javagames.sound;
```

```
public class BlockingDataLine extends AudioStream {
    private AudioDataLine stream;
    public BlockingDataLine( byte[] soundData ) {
        super( soundData );
    }
```