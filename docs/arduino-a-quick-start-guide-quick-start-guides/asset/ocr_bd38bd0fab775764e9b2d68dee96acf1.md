around the x-axis. Here’s the code that gets the controller data via the serial port:

```
Download: MotionSensor/Game/Game.pde

void serialEvent(Serial port) {
    final String arduinoData = port.readStringUntil(LINE_FEED);

    if (arduinoData != null) {
        final int[] data = int(split(trim(arduinoData), ' '));
        if (data.length == 4) {
            buttonPressed = (data[3] == 1);
            if (buttonPressed) {
                paused = !paused;
                if (done) {
                    done = false;
                    initGame();
                }
            }

            if (!paused)
                xpos = int(map(data[0], X_AXIS_MIN, X_AXIS_MAX, 0, WIDTH));
        }
    }
}
```

Processing calls the serialEvent() function whenever new data is available on the serial port. The controller sends its data line by line. Each line contains the current acceleration of the x-, y-, and z-axes and the current state of the button. It separates all attributes by blanks. So, in serialEvent(), we read the new line, split it at the blank characters, and convert the resulting strings into int values. This all happens in line 5.

We check whether we actually got all four attributes, and then we see whether the player has pushed the button on the game controller. If yes, we toggle the pause state: if the game currently is in pause mode, we continue the game; otherwise, we pause it. Also, we check whether the game has been finished. If yes, we start a new game.

Finally, we read the current X acceleration in line 17 and map it to the possible x positions of our paddle. That’s really all we have to do to move the paddle using our own game controller. Also, it doesn’t matter if you use the controller to control a game or a completely different type of software. You only have to read four integer values from the serial port when you need them.

In this section, you have learned much more about game programming than about Arduino programming or hardware. But you should