
![](img/588a4cda8f2acae94a7e1987bf99400d_432_0.png)

Figure 13.6 Sound Player Example. © 2014 Timothy Wright.

These three events—one-shot, loop, and restart—for both small and large data files, provide many sound needs for computer games. The SoundPlayerExample code, seen in Figure 13.6 and located in the javagames.sound package, demonstrates using the new sound classes to add sound to the game loop.

The initialize() method loads two sounds: a weapon blast and a rain sound. The readBytes() method extracts the raw sound bytes from the file. The loadWaveFile() method creates all of the event objects. For short clips, the events use a BlockingClip. For large data, a BlockingDataLine can be used. This example uses a small sound with both types of sound types for testing. The shutDownClips() method stops each sound event thread before returning.

The processInput() method handles the keypresses as always. The F1 and F2 keys load the two different sounds. The number 1 key starts the one-shot clip and the 2 key stops the one-shot clip. The 3 key starts the clip loop, and 4 stops it. The 5 key fires the restart clip. The 6, 7, 8, 9, and 0 keys do the same things with a data line stream. The render() method displays the usual instructions.

And now...making a limited appearance, it's the terminate() method (I was beginning to think this method would never be needed). This method shuts down all the event threads when the program is shut down.

```java
package javagames.sound;
import java.awt.Graphics;
import java.awt.event.KeyEvent;
import java.io.*;
import javagames.util.*;

public class SoundPlayerExample extends SimpleFramework {
    private OneShotEvent oneShotClip;
    private LoopEvent loopClip;
    private RestartEvent restartClip;
    private OneShotEvent oneShotStream;
    private LoopEvent loopStream;
    private RestartEvent restartStream;
    private byte[] weaponBytes;
    private byte[] rainBytes;
    private String loaded;

    public SoundPlayerExample() {
        appWidth = 340;
        appHeight = 340;
        appSleep = 10L;
        appTitle = "Sound Player Example";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();

        InputStream in = ResourceLoader.load(
                SoundPlayerExample.class,
                "./res/assets/sound/WEAPON_sciFi_fire_02.wav",
                "asdf"
        );
        weaponBytes = readBytes(in);

        in = ResourceLoader.load(
                SoundPlayerExample.class,
                "./res/assets/sound/WEATHER_rain_medium_5k.wav",
                "asdf"
        );
        rainBytes = readBytes(in);
        loadWaveFile(weaponBytes);
        loaded = "weapon";
    }

    private byte[] readBytes(InputStream in) {
        try {
            BufferedInputStream buf = new BufferedInputStream(in);
            ByteArrayOutputStream out = new ByteArrayOutputStream();
            int read;
            while ((read = buf.read()) != -1) {
                out.write(read);
            }
            in.close();
            return out.toByteArray();
        } catch (IOException ex) {
            ex.printStackTrace();
            return null;
        }
    }

    private void loadWaveFile(byte[] rawData) {
        shutDownClips();
        oneShotClip = new OneShotEvent(new BlockingClip(rawData));
        oneShotClip.initialize();
        loopClip = new LoopEvent(new BlockingClip(rawData));
        loopClip.initialize();
        restartClip = new RestartEvent(new BlockingClip(rawData));
        restartClip.initialize();
        oneShotStream = new OneShotEvent(new BlockingDataLine(rawData));
        oneShotStream.initialize();
        loopStream = new LoopEvent(new BlockingDataLine(rawData));
        loopStream.initialize();
        restartStream = new RestartEvent(new BlockingDataLine(rawData));
        restartStream.initialize();
    }

    private void shutDownClips() {
        if (oneShotClip != null) oneShotClip.shutDown();
        if (loopClip != null) loopClip.shutDown();
        if (restartClip != null) restartClip.shutDown();
        if (oneShotStream != null) oneShotStream.shutDown();
        if (loopStream != null) loopStream.shutDown();
        if (restartStream != null) restartStream.shutDown();
    }

    @Override
    protected void processInput(float delta) {
        super.processInput(delta);

        if (keyboard.keyDownOnce(KeyEvent.VK_F1)) {
            loadWaveFile(weaponBytes);
            loaded = "weapon";
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_F2)) {
            loadWaveFile(rainBytes);
            loaded = "rain";
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_1)) {
            oneShotClip.fire();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_2)) {
            oneShotClip.done();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_3)) {
            loopClip.fire();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_4)) {
            loopClip.done();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_5)) {
            restartClip.fire();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_6)) {
            oneShotStream.fire();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_7)) {
            oneShotStream.done();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_8)) {
            loopStream.fire();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_9)) {
            loopStream.done();
        }

        if (keyboard.keyDownOnce(KeyEvent.VK_0)) {
            restartStream.fire();
        }
    }

    @Override
    protected void updateObjects(float delta) {
        super.updateObjects(delta);
    }

    @Override
    protected void render(Graphics g) {
        super.render(g);

        textPos = Utility.drawString(g, 20, textPos,
            "",
            "(F1) Load Weapon",
            "(F2) Load Rain",
            "Loaded: " + loaded,
            "",
            "(1) Fire One Shot (clip)",
            "(2) Cancel One Shot (clip)",
            "(3) Start Loop (clip)",
            "(4) Stop Loop (clip)",
            "(5) Reusable (clip)",
            "",
            "(6) Fire One Shot (stream)",
            "(7) Cancel One Shot (stream)",
            "(8) Start Loop (stream)",
            "(9) Stop Loop (stream)",
            "(0) Reusable (stream)"
        );
    }

    @Override
    protected void terminate() {
        super.terminate();
        shutDownClips();
    }

    public static void main(String[] args) {
        launchApp(new SoundPlayerExample());
    }
}
```

## ADDING SOUND CONTROLS

You're almost done. The only thing left to add are the sound controls. The following controls are available:

- Boolean: MUTE APPLY_REVERB
- Enum: REVERB
- Float: AUX_RETURN AUX_SEND
- BALANCE
- MASTER_GAIN
- PAN
- REVERB_RETURN
- REVERB_SEND
- SAMPLE_RATE
- VOLUME

Not all lines support all controls, so it is important to check if the control is available before getting access. The following code checks for a MASTER_GAIN control and acquires the control if it is available:

```java
if (line.isControlSupported(FloatControl.Type.MASTER_GAIN)) {
    FloatControl gainControl =
        (FloatControl) line.getControl(FloatControl.Type.MASTER_GAIN);
}
```

The MASTER_GAIN control will adjust the sound volume and the PAN control will determine from which speaker the sound is heard. If the sound is not a mono sound, but a stereo sound, use the BALANCE control. The updated AudioStream code adds support for GAIN and PAN controls.

```java
package javagames.sound;

import java.util.*;
import java.util.concurrent.locks.*;
import javax.sound.sampled.*;
import javax.sound.sampled.LineEvent.*;

public abstract class AudioStream implements LineListener {
    public static final int LOOP_CONTINUOUSLY = -1;

    protected final Lock lock = new ReentrantLock();
    protected final Condition cond = lock.newCondition();

    protected volatile boolean open = false;
    protected volatile boolean started = false;

    // UPDATES
    protected FloatControl gainControl;
    protected FloatControl panControl;
    // UPDATES

    protected byte[] soundData;

    private List<BlockingAudioListener> listeners =
        Collections.synchronizedList(
            new ArrayList<BlockingAudioListener>());

    public AudioStream(byte[] soundData) {
        this.soundData = soundData;
    }

    public abstract void open();

    public abstract void close();

    public abstract void start();

    public abstract void loop(int count);

    public abstract void restart();

    public abstract void stop();

    public boolean addListener(BlockingAudioListener listener) {
        return listeners.add(listener);
    }

    protected void fireTaskFinished() {
        synchronized (listeners) {
            for (BlockingAudioListener listener : listeners) {
                listener.audioFinished();
            }
        }
    }

    @Override
    public void update(LineEvent event) {
        boolean wasStarted = started;
        lock.lock();
        try {
            if (event.getType() == Type.OPEN) {
                open = true;
            } else if (event.getType() == Type.CLOSE) {
                open = false;
            } else if (event.getType() == Type.START) {
                started = true;
            } else if (event.getType() == Type.STOP) {
                started = false;
            }
            cond.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```

