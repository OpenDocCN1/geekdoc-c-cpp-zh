

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

## 使用极坐标

笛卡尔坐标表示为一对 (x,y) 值。极坐标表示为一个角度和一个距离。参见图 3.3。

![](img/588a4cda8f2acae94a7e1987bf99400d_79_0.png)

图 3.3
笛卡尔坐标与极坐标对比。
© 2014 Timothy Wright.

与 (x,y) 对不同，极坐标的形式为 (r,a)，其中 r 是距离（半径），a 是角度。由于 Java 的三角函数使用弧度，所有角度均假设为弧度。不过，在两种表示之间转换很容易：

```
Math.toRadians( double degrees )
Math.toDegrees( double radians )
```

要将笛卡尔坐标转换为极坐标，可以将点视为一个三角形，利用三角函数求解所需的值。

![](img/588a4cda8f2acae94a7e1987bf99400d_80_0.png)

图 3.4 从笛卡尔坐标到极坐标的转换。© 2014 Timothy Wright.

如图 3.4 所示，距离可视为三角形的斜边，可使用勾股定理求得：

```
$r^2 = a^2 + b^2$
$r = \sqrt{a^2 + b^2}$
```

角度可使用正切函数求得：

```
$\theta = \tan \frac{y}{x}$
```

将极坐标转换回 (x,y) 对同样很容易：

```
$x = r \cos \theta$
$y = r \sin \theta$
```

正是上述定义可用于推导前面所示的旋转方程。从起始角度旋转若干弧度，等同于在起始角度上加上所需的额外旋转角度。换句话说，要将一点旋转若干弧度，方程可表示如下：

```
$x' = r \cos(\theta + \phi)$
$y' = r \sin(\theta + \phi)$
```

### 三角函数来解救：

```
sin(θ + ϕ) = sin θ cos ϕ + cos θ sin ϕ
cos(θ + ϕ) = cos θ cos ϕ - sin θ sin ϕ
```

将前面的方程替换为这种新表示，得到：

```
x' = r(cos θ cos ϕ - sin θ sin ϕ)
y' = r(sin θ cos ϕ + cos θ sin ϕ)
```

分配 r 值后得到：

```
x' = r cos θ cos ϕ - r sin θ sin ϕ
y' = r sin θ cos ϕ + r cos θ sin ϕ
```

请记住以下内容：

```
x = r cos θ
y = r sin θ
```

你可以代入原始 x 和 y 值，得到以下结果：

```
x' = x cos ϕ - y sin ϕ
y' = y cos ϕ + x sin ϕ
```

这就是前面为 Vector2f 类中坐标旋转所提出的方程。PolarCoordinateExample 位于 javagames.transform 包中，如图 3.5 所示，它在笛卡尔坐标和极坐标之间进行转换。coord 变量保存鼠标所在的屏幕位置，以屏幕中心为偏移量。

