“Threads.” The example code implements the LineListener interface so that when the events are received, the state is stored in the open and started variables and waiting threads are notified to wake.

The readBytes() method reads the raw sound file bytes into an array for easy reuse. The runTestWithoutWaiting() method (which can lock up) demonstrates the wrong way to use the sound API. Because it doesn’t wait for the LineListener events before continuing, it can lock up, draining a sound that will never play. The runWithWaiting() demonstrates using the wait/notify mechanism to wait for LineListener events before proceeding.

Finally, the main() method runs both tests. Even if you are able to run both tests without a lockup, someone may have a machine that is too fast or too slow (like me), and no one likes it when the sound stops playing.

```
```java
package javagames.sound;

import java.io.*;
import javagames.util.ResourceLoader;
import javax.sound.sampled.*;

public class PlayingClipsExample implements LineListener {
    private volatile boolean open = false;
    private volatile boolean started = false;
    public byte[] readBytes( InputStream in ) {
        try {
            BufferedInputStream buf = new BufferedInputStream( in );
            ByteArrayOutputStream out = new ByteArrayOutputStream();
            int read;
            while( (read = buf.read()) != -1 ) {
                out.write( read );
            }
            in.close();
            return out.toByteArray();
        } catch( IOException ex ) {
            ex.printStackTrace();
            return null;
        }
    }
}
```
```