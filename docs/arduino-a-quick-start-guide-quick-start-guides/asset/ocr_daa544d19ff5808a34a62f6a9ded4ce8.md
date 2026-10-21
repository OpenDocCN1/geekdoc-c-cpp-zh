```
final int WIDTH = 500;
final int HEIGHT = 500;
final int BAUD_RATE = 19200;
final int X_AXIS_MIN = 300;
final int X_AXIS_MAX = 700;
final int Y_AXIS_MIN = 300;
final int Y_AXIS_MAX = 700;
final int Z_AXIS_MIN = 300;
final int Z_AXIS_MAX = 700;
final int MIN_SCALE = 5;
final int MAX_SCALE = 128;
final float MX = 2.0 / (X_AXIS_MAX - X_AXIS_MIN);
final float MY = 2.0 / (Y_AXIS_MAX - Y_AXIS_MIN);
final float MZ = 2.0 / (Z_AXIS_MAX - Z_AXIS_MIN);
final float BX = 1.0 - MX * X_AXIS_MAX;
final float BY = 1.0 - MY * Y_AXIS_MAX;
final float BZ = 1.0 - MZ * Z_AXIS_MAX;
```

X_AXIS_MIN and X_AXIS_MAX define the minimum and maximum acceleration values returned by the Nunchuk for the x-axis. The same is true for Y_AXIS_MIN, and so on. We'll need the remaining constants (MX, BX, and so on) to turn acceleration values into angles later, so don't worry too much about them.

Next we need some variables to store the cube's current state: its position, the rotation angle for the different axes, and its current scaling:

```
int xpos = WIDTH / 2;
int ypos = HEIGHT / 2;
int scale = 90;

float xrotate = 0.0;
float yrotate = 0.0;
float zrotate = 0.0;
```

In the setup() method, we initialize the screen and the serial port:

```
void setup() {
  size(WIDTH, HEIGHT, P3D);
  noStroke();
  colorMode(RGB, 1);
  background(0);
  println(Serial.list());
  arduinoPort = new Serial(this, Serial.list()[0], BAUD_RATE);
  arduinoPort.bufferUntil(LINE_FEED);
}
```