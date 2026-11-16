
private float tx, ty;
private float vx, vy;
private float rot, rotStep;
private float scale, scaleStep;
private float sx, sxStep;
private float sy, syStep;
private boolean doTranslate;
private boolean doScale;
private boolean doRotate;
private boolean doShear;

public VectorGraphicsExample() {
}

protected void createAndShowGUI() {
    Canvas canvas = new Canvas();
    canvas.setSize(640, 480);
    canvas.setBackground(Color.BLACK);
    canvas.setIgnoreRepaint(true);
    getContentPane().add(canvas);
    setTitle("Vector Graphics Example");
    setIgnoreRepaint(true);
    pack();

    // Add key listeners
    keyboard = new KeyboardInput();
    canvas.addKeyListener(keyboard);

    // Add mouse listeners
    // For full screen : mouse = new RelativeMouseInput( this );
    mouse = new RelativeMouseInput(canvas);
    canvas.addMouseListener(mouse);
    canvas.addMouseMotionListener(mouse);
    canvas.addMouseWheelListener(mouse);

    setVisible(true);
    canvas.createBufferStrategy(2);
    bs = canvas.getBufferStrategy();
    canvas.requestFocus();

    gameThread = new Thread(this);
    gameThread.start();
}

public void run() {
    running = true;
    initializing = true;
    while (running) {
        gameLoop();
    }
}

private void gameLoop() {
    processInput();
    processObjects();
    renderFrame();
    sleep(10L);
}

private void renderFrame() {
    do {
        do {
            Graphics g = null;
            try {
                g = bs.getDrawGraphics();
                g.clearRect(0, 0, getWidth(), getHeight());
                render(g);
            } finally {
                if (g != null) {
                    g.dispose();
                }
            }
        } while (bs.contentsRestored());
        bs.show();
    } while (bs.contentsLost());
}

private void sleep(long sleep) {
    try {
        Thread.sleep(sleep);
    } catch (InterruptedException ex) {}
}

private void initialize() {
    frameRate = new FrameRate();
    frameRate.initialize();
    polygon = new Vector2f[] {
        new Vector2f(10, 0),
        new Vector2f(-10, 8),
        new Vector2f(0, 0),
        new Vector2f(-10, -8),
    };
    world = new Vector2f[polygon.length];
    reset();
}

private void reset() {
    tx = SCREEN_W / 2;
    ty = SCREEN_H / 2;
    vx = vy = 2;
    rot = 0.0f;
    rotStep = (float)Math.toRadians(1.0);
    scale = 1.0f;
    scaleStep = 0.1f;
    sx = sy = 0.0f;
    sxStep = syStep = 0.01f;
    doRotate = doScale = doTranslate = false;
    doXShear = doYShear = false;
}

private void processInput() {
    keyboard.poll();
    mouse.poll();
    if (keyboard.keyDownOnce(KeyEvent.VK_R)) {
        doRotate = !doRotate;
    }
    if (keyboard.keyDownOnce(KeyEvent.VK_S)) {
        doScale = !doScale;
    }
    if (keyboard.keyDownOnce(KeyEvent.VK_T)) {
        doTranslate = !doTranslate;
    }
    if (keyboard.keyDownOnce(KeyEvent.VK_X)) {
        doXShear = !doXShear;
    }
    if (keyboard.keyDownOnce(KeyEvent.VK_Y)) {
        doYShear = !doYShear;
    }
    if (keyboard.keyDownOnce(KeyEvent.VK_SPACE)) {
        reset();
    }
}

private void processObjects() {
    // copy data...
    for (int i = 0; i < polygon.length; ++i) {
        world[i] = new Vector2f(polygon[i]);
    }

    if (doScale) {
        scale += scaleStep;
        if (scale < 1.0 || scale > 5.0) {
            scaleStep = -scaleStep;
        }
    }

    if (doRotate) {
        rot += rotStep;
        if (rot < 0.0f || rot > 2 * Math.PI) {
            rotStep = -rotStep;
        }
    }

    if (doTranslate) {
        tx += vx;
        if (tx < 0 || tx > SCREEN_W) {
            vx = -vx;
        }
        ty += vy;
        if (ty < 0 || ty > SCREEN_H) {
            vy = -vy;
        }
    }

    if (doXShear) {
        sx += sxStep;
        if (Math.abs(sx) > 2.0) {
            sxStep = -sxStep;
        }
    }

    if (doYShear) {
        sy += syStep;
        if (Math.abs(sy) > 2.0) {
            syStep = -syStep;
        }
    }

    for (int i = 0; i < world.length; ++i) {
        world[i].shear(sx, sy);
        world[i].scale(scale, scale);
        world[i].rotate(rot);
        world[i].translate(tx, ty);
    }
}

private void render(Graphics g) {
    g.setFont(new Font("Courier New", Font.PLAIN, 12));
    g.setColor(Color.GREEN);
    frameRate.calculate();
    g.drawString("FrameRate: " + getFrameRate(), 20, 20);
    g.drawString("Translate(T) : " + doTranslate, 20, 35);
    g.drawString("Rotate(R) : " + doRotate, 20, 50);
    g.drawString("Scale(S) : " + doScale, 20, 65);
    g.drawString("X-Shear(X) : " + doXShear, 20, 80);
    g.drawString("Y-Shear(Y) : " + doYShear, 20, 95);
    g.drawString("Press [SPACE] to reset", 20, 110);

    Vector2f S = world[world.length - 1];
    Vector2f P = null;
    for (int i = 0; i < world.length; ++i) {
        P = world[i];
        g.drawLine((int)S.x, (int)S.y, (int)P.x, (int)P.y);
        S = P;
    }
}

protected void onWindowClosing() {
    try {
        running = false;
        gameThread.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    System.exit(0);
}

public static void main(String[] args) {
    final VectorGraphicsExample app = new VectorGraphicsExample();
    app.addWindowListener(new WindowAdapter() {
        public void windowClosing(WindowEvent e) {
            app.onWindowClosing();
        }
    });
    SwingUtilities.invokeLater(new Runnable() {
        public void run() {
            app.createAndShowGUI();
        }
    });
}

## USING POLAR COORDINATES

Cartesian coordinates are represented as a pair of (x,y) values. Polar coordinates are represented as an angle and a distance. See Figure 3.3.

![](img/588a4cda8f2acae94a7e1987bf99400d_79_0.png)

Figure 3.3
Cartesian vs. Polar Coordinates.
© 2014 Timothy Wright.

Instead of an (x,y) pair, polar coordinates are in the form (r,a), where r is a distance (radius), and a is an angle. Because Java's trigonometric functions use radians, all angles are assumed to be in radians. It is easy to convert between the two representations, however:

```
Math.toRadians( double degrees )
Math.toDegrees( double radians )
```

To convert from the Cartesian coordinates to the polar coordinates, the point can be treated as a triangle, using trigonometry to solve for the desired values.

![](img/588a4cda8f2acae94a7e1987bf99400d_80_0.png)

Figure 3.4 Cartesian to Polar Conversion. © 2014 Timothy Wright.

The distance, as seen in Figure 3.4, can be seen as the hypotenuse of the triangle, and can be found using the Pythagorean theorem:

```
$r^2 = a^2 + b^2$
$r = \sqrt{a^2 + b^2}$
```

The angle can be found using the tangent function:

```
$\theta = \tan \frac{y}{x}$
```

Converting back from the polar coordinate to the (x,y) pair is also easy:

```
$x = r \cos \theta$
$y = r \sin \theta$
```

It is the previous definition that can be used to derive the rotation equation shown earlier. Rotating from the starting angle some number of radians is the same as adding the desired additional rotation angle to the starting angle. In other words, to rotate a point some number of radians, the equation can be expressed as follows:

```
$x' = r \cos(\theta + \phi)$
$y' = r \sin(\theta + \phi)$
```

### Trigonometry to the rescue:

```
sin(θ + ϕ) = sin θ cos ϕ + cos θ sin ϕ
cos(θ + ϕ) = cos θ cos ϕ - sin θ sin ϕ
```

Replacing the previous equation with this new representation gives:

```
x' = r(cos θ cos ϕ - sin θ sin ϕ)
y' = r(sin θ cos ϕ + cos θ sin ϕ)
```

Distributing the r values gives:

```
x' = r cos θ cos ϕ - r sin θ sin ϕ
y' = r sin θ cos ϕ + r cos θ sin ϕ
```

Remembering the following:

```
x = r cos θ
y = r sin θ
```

You can substitute the original x and y values, leaving the following:

```
x' = x cos ϕ - y sin ϕ
y' = y cos ϕ + x sin ϕ
```

This is the equation presented earlier for rotation of a coordinate in the Vector2f class. The PolarCoordinateExample, located in the javagames.transform package and shown in Figure 3.5, converts from a Cartesian coordinate to a polar coordinate and back again. The coord variable holds the screen position where the mouse is located, offset by the center of the screen.
