The calculate() method should be called once for every rendered frame. To calculate the frame rate, the current time is subtracted from the last time and stored in the delta variable. The frame count is incremented each frame, and when the delta time is over one second, the new FPS are generated. Since the delta variable is rarely exactly one second, 1,000 milliseconds are subtracted from the delta variable to save the extra milliseconds. Once the new frame rate is saved, the frame count is reset and the process begins again.

```
package javagames.util;

public class FrameRate {
    private String frameRate;
    private long lastTime;
    private long delta;
    private int frameCount;

    public void initialize() {
        lastTime = System.currentTimeMillis();
        frameRate = "FPS 0";
    }

    public void calculate() {
        long current = System.currentTimeMillis();
        delta += current - lastTime;
        lastTime = current;
        frameCount++;

        if (delta > 1000) {
            delta -= 1000;
            frameRate = String.format("FPS %s", frameCount);
            frameCount = 0;
        }
    }

    public String getFrameRate() {
        return frameRate;
    }
}
```

# CREATING THE HELLO WORLD APPLICATION

The Hello World application seen in Figure 1.1 is the first game window example. The HelloWorldApp is located in the javagames.render package. Other than clearing and redrawing the background, nothing else is rendered in the window. The HelloWorldApp extends the JFrame class, which is a top level window component from Java's Swing library. This application contains a FrameRate object, which is used to measure the frame rate of the application.