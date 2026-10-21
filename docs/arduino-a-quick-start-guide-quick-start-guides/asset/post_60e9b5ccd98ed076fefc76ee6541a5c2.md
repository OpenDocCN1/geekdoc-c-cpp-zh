
![](img/dcfd13a1bf99c4d3f9996627012a6526_139_0.png)

Figure 6.4: Game controller with accelerometer and pushbutton

That's the whole trick. To see its effect, leave the sensor untouched on your desk, and run the program with different buffer sizes. If you do not touch the sensor, you would not expect the program's output to change. But if you set BUFFER_SIZE to 1, you will quickly see small changes. They will disappear as soon as the buffer is big enough.

The acceleration data we measure now is sufficiently accurate, and we can finally build a game controller that will not annoy users because of unexpected movements.

## 6.5 Building Your Own Game Controller

To build a full-blown game controller, we only need to add a button to our breadboard. In Figure 6.4, you can see how to do it (please, double-check the pin labels on your breakout board!).

![](img/dcfd13a1bf99c4d3f9996627012a6526_140_0.png)

# Figure 6.5: An Arduino prototyping shield

That’s how it looks inside a typical modern game controller. We will not build a fancy housing for the controller, but we still should think about ergonomics for a moment. Our current breadboard solution is rather fragile, and you cannot really wave around the board when it’s connected to the Arduino. Sooner or later you will disconnect some wires, and the controller will stop working.

To solve this problem, you could try to attach the breadboard to the Arduino using some rubber bands. That works, but it does not look very pretty, and it’s still hard to handle.

A much better solution is to use an Arduino Prototyping shield (see Figure 6.5). It is a pluggable breadboard that lets you quickly build circuit prototypes. The breadboard is surrounded by the Arduino’s pins, so you no longer need long wires. Shields are a great way to enhance an Arduino’s capabilities, and you can get shields for many different purposes such as adding Ethernet, sound, displays, and so on.²

Using the Proto Shield our game controller looks as in Figure 6.6, on the next page. Neat, eh?

> 2. At http://shieldlist.org/, you find a comprehensive list of Arduino shields.

![](img/dcfd13a1bf99c4d3f9996627012a6526_141_0.png)

# Figure 6.6: The complete game controller on a Proto shield

Now that the hardware is complete, we need a final version of the game controller software. It supports the button we have added, and it performs the anti-jittering we have created in Section 6.4, Finding and Polishing Edge Values, on page 137:

Download MotionSensor/Controller/Controller.pde

```
#include <Bounce.h>

const unsigned int BUTTON_PIN = 7;
const unsigned int X_AXIS_PIN = 2;
const unsigned int Y_AXIS_PIN = 1;
const unsigned int Z_AXIS_PIN = 0;
const unsigned int NUM_AXES = 3;
const unsigned int PINS[NUM_AXES] = {
  X_AXIS_PIN, Y_AXIS_PIN, Z_AXIS_PIN
};
const unsigned int BUFFER_SIZE = 16;
const unsigned int BAUD_RATE = 19200;

int buffer[NUM_AXES][BUFFER_SIZE];
int buffer_pos[NUM_AXES] = { 0 };

Bounce button(BUTTON_PIN, 20);

void setup() {
  Serial.begin(BAUD_RATE);
  pinMode(BUTTON_PIN, INPUT);
}
```

```
int get_axis(const int axis) {
    delay(1);
    buffer[axis][buffer_pos[axis]] = analogRead(PINS[axis]);
    buffer_pos[axis] = (buffer_pos[axis] + 1) % BUFFER_SIZE;

    long sum = 0;
    for (int i = 0; i < BUFFER_SIZE; i++)
        sum += buffer[axis][i];
    return round(sum / BUFFER_SIZE);
}

int get_x() { return get_axis(0); }
int get_y() { return get_axis(1); }
int get_z() { return get_axis(2); }

void loop() {
    Serial.print(get_x());
    Serial.print(" ");
    Serial.print(get_y());
    Serial.print(" ");
    Serial.print(get_z());
    Serial.print(" ");
    if (button.update())
        Serial.println(button.read() == HIGH ? "1" : "0");
    else
        Serial.println("0");
}
```

As in Section 3.7, Building a Dice Game, on page 80, we use the Bounce class to debounce the button. The rest of the code is pretty much standard, and the only thing worth mentioning is that we use a 19200 baud rate to transfer the controller data sufficiently fast.

Compile and upload the code, open the serial terminal, and play around with the controller. Move it, press the button sometimes, and it should output something like the following:

```
324 365 396 0
325 364 397 0
325 364 397 1
325 364 397 0
325 365 397 0
325 365 397 1
326 364 397 0
```

A homemade game controller is nice, but wouldn’t it be even nicer if we also had a game that supports it? That’s what we will build in the next section.

## 6.6 Writing Your Own Game

To test our game controller, we will program a simple Breakout³ clone in Processing. The game’s goal is to destroy all bricks in the upper half of the screen with a ball. You can control the ball with the paddle at the bottom of the screen, and you can tilt the controller around the x-axis to move the paddle horizontally. It’ll look something like this:

![](img/dcfd13a1bf99c4d3f9996627012a6526_143_0.png)

Although this is not a book about game programming, it will not hurt to take a look at the game’s innards, especially because game programming with Processing is really pure fun! Download the code from the book’s website⁴ and play the game before you dive into the code.

Because we will connect our game controller to the serial port, we have to initialize it:

```
import processing.serial.*;
Serial arduinoPort;
```

3. http://en.wikipedia.org/wiki/Breakout_%28arcade_game%29
4. http://www.pragprog.com/titles/msard

Then we define some constants that will help us to customize the game easily:

```
final int COLUMNS = 7;
final int ROWS = 4;
final int BALL_RADIUS = 8;
final int BALL_DIAMETER = BALL_RADIUS * 2;
final int MAX_VELOCITY = 8;
final int PADDLE_WIDTH = 60;
final int PADDLE_HEIGHT = 15;
final int BRICK_WIDTH = 40;
final int BRICK_HEIGHT = 20;
final int MARGIN = 10;
final int WIDTH = COLUMNS * BRICK_WIDTH + 2 * MARGIN;
final int HEIGHT = 300;
final int X_AXIS_MIN = 252;
final int X_AXIS_MAX = 443;
final int LINE_FEED = 10;
final int BAUD_RATE = 19200;
```

Most of these values should be self-explanatory—they define the size of the objects that appear on the screen. For example, PADDLE_WIDTH is width of the paddle measured in pixels, and COLUMNS and ROWS set the layout of the bricks. You should replace X_AXIS_MIN and X_AXIS_MAX the minimum and maximum values you measured for your sensor in Section 6.4, Finding and Polishing Edge Values, on page 137.

Next we choose how to represent the game's objects:

```
int px, py;
int vx, vy;
int xpos = WIDTH / 2;
int[][] bricks = new int[COLUMNS][ROWS];
```

We store the balls' current x and y coordinates in px and py. For its current x and y velocity, we use vx and vy. We store the paddle's x position in xpos.

bricks is a two-dimensional array and contains the current state of the bricks on the screen. If an array element is set to 1, the corresponding brick is still on the screen. 0 means that it has been destroyed already.

Finally, we need to store the possible states of the game:

```
boolean buttonPressed = false;
boolean paused = true;
boolean done = true;
```

Unsurprisingly, we set buttonPressed to true when the button on the controller is pressed. Otherwise, it is false. paused tells you whether the game is currently paused, and done is true when the current level is done, that is, when all bricks have been destroyed.

Every Processing program needs a setup() function, and here is ours:

```
Download MotionSensor/Game/Game.pde

void setup() {
  size(WIDTH, HEIGHT);
  noCursor();
  textFont(loadFont("Verdana-Bold-36.vlw"));
  initGame();
  println(Serial.list());
  arduinoPort = new Serial(this, Serial.list()[0], BAUD_RATE);
  arduinoPort.bufferUntil(LINE_FEED);
}

void initGame() {
  initBricks();
  initBall();
}

void initBricks() {
  for (int x = 0; x < COLUMNS; x++)
    for (int y = 0; y < ROWS; y++)
      bricks[x][y] = 1;
}

void initBall() {
  px = width / 2;
  py = height / 2;
  vx = int(random(-MAX_VELOCITY, MAX_VELOCITY));
  vy = -2;
}
```

The setup() function initializes the screen, hides the mouse pointer with noCursor(), and sets the font that we will use to output messages (create the font using Processing's Tools > Create Font menu). Then we call initGame() to initialize the bricks array and the ball's current position and velocity. To make things more interesting, the velocity in x direction is set to a random value. We set the velocity for the y direction to -2, which makes the ball fall at a reasonable speed.

Now that everything is initialized, we can implement the game's main loop. Processing's draw() method is a perfect place:⁵

5. http://processing.org/reference/ has excellent documentation for all Processing classes.
