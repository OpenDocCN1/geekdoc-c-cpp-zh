

```java
// Add mouse listeners
// For full screen : mouse = new RelativeMouseInput( this );
mouse = new RelativeMouseInput( canvas );
canvas.addMouseListener( mouse );
canvas.addMouseMotionListener( mouse );
canvas.addMouseWheelListener( mouse );

setVisible( true );
canvas.createBufferStrategy( 2 );
bs = canvas.getBufferStrategy();
canvas.requestFocus();

gameThread = new Thread( this );
gameThread.start();
}

public void run() {
    running = true;
    initialize();
    while( running ) {
        gameLoop();
    }
}

private void gameLoop() {
    processInput();
    renderFrame();
    sleep( 10L );
}

private void renderFrame() {
    do
    do {
        Graphics g = null;
        try {
            g = bs.getDrawGraphics();
            g.clearRect( 0, 0, getWidth(), getHeight() );
            render( g );
        } finally {
            if ( g != null ) {
                g.dispose();
            }
        }
    } while( bs.contentsRestored() );
    bs.show();
} while( bs.contentsLost() );
```

```java
private void sleep( long sleep ) {
    try {
        Thread.sleep( sleep );
    } catch( InterruptedException ex ) {
    }
}
```

```java
private void initialize() {
    frameRate = new FrameRate();
    frameRate.initialize();

    earthDelta = (float)Math.toRadians( 0.5 );
    moonDelta = (float)Math.toRadians( 2.5 );

    showStars = true;
    stars = new int[ 1000 ];
    for( int i = 0; i < stars.length - 1; i += 2 ) {
        stars[i] = rand.nextInt( SCREEN_W );
        stars[i+1] = rand.nextInt( SCREEN_H );
    }
}
```

```java
private void processInput() {
    keyboard.poll();
    mouse.poll();

    if( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
        showStars = !showStars;
    }
}
```

```java
private void render( Graphics g ) {
    g.setColor( Color.GREEN );
    frameRate.calculate();
    g.drawString( frameRate.getFrameRate(), 20, 20 );
    g.drawString( "Press [SPACE] to toggle stars", 20, 35 );

    if( showStars ) {
        g.setColor( Color.WHITE );
        for( int i = 0; i < stars.length - 1; i += 2 ) {
            g.fillRect( stars[i], stars[i+1], 1, 1 );
        }
    }

    // draw the sun...
    Matrix3x3f sunMat = Matrix3x3f.identity();
    sunMat = sunMat.mul(
        Matrix3x3f.translate( SCREEN_W / 2, SCREEN_H / 2 )
    );

    Vector2f sun = sunMat.mul( new Vector2f() );

    g.setColor( Color.YELLOW );
    g.fillOval( (int)sun.x - 50, (int)sun.y - 50, 100, 100 );

    // draw Earth's Orbit
    g.setColor( Color.WHITE );
    g.drawOval( (int)sun.x - SCREEN_W / 4, (int)sun.y - SCREEN_W / 4,
            SCREEN_W / 2, SCREEN_W / 2 );

    // draw the Earth
    Matrix3x3f earthMat = Matrix3x3f.translate( SCREEN_W / 4, 0 );
    earthMat = earthMat.mul( Matrix3x3f.rotate( earthRot ) );
    earthMat = earthMat.mul( sunMat );

    earthRot += earthDelta;

    Vector2f earth = earthMat.mul( new Vector2f() );
    g.setColor( Color.BLUE );
    g.fillOval( (int)earth.x - 10, (int)earth.y - 10, 20, 20 );

    // draw the Moon
    Matrix3x3f moonMat = Matrix3x3f.translate( 30, 0 );
    moonMat = moonMat.mul( Matrix3x3f.rotate( moonRot ) );
    moonMat = moonMat.mul( earthMat );

    moonRot += moonDelta;

    Vector2f moon = moonMat.mul( new Vector2f() );
    g.setColor( Color.LIGHT_GRAY );
    g.fillOval( (int)moon.x - 5, (int)moon.y - 5, 10, 10 );
}

protected void onWindowClosing() {
    try {
        running = false;
        gameThread.join();
    } catch( InterruptedException e ) {
        e.printStackTrace();
    }

    System.exit( 0 );
}

public static void main( String[] args ) {
    final MatrixMultiplyExample app = new MatrixMultiplyExample();
    app.addWindowListener( new WindowAdapter() {
        public void windowClosing( WindowEvent e ) {
            app.onWindowClosing();
        }
    });
}
```

```java
SwingUtilities.invokeLater(new Runnable() {
    public void run() {
        app.createAndShowGUI();
    }
});
}
}
```

## 仿射变换

Java 有一个名为 AffineTransform 的类，可用于执行矩阵变换。虽然不重写代码是件好事，但研究和学习算法以理解它们也是件好事。代码示例将继续从零开始开发库，但请随意使用内置类。

```
AffineTransform.setToIdentity()
AffineTransform.concatenate(AffineTransform)
AffineTransform.rotate(double radians)
AffineTransform.scale(double sx, double sy)
AffineTransform.translate(double tx, double ty)
AffineTransform.shear(double sx, double sy)
```

使用 AffineTransform 类，有多种方法可以将变换应用于数据点。以下代码使用了所有可用方法：

```
AffineTransform trans = new AffineTransform();
Shape srcShape = new Rectangle();
Shape destShape = null;
Point2D srcPoint = new Point2D.Float();
Point2D destPoint = new Point2D.Float();
Point2D pointSrc[] = new Point2D[] {
    new Point2D.Float(),
    new Point2D.Float(),
    new Point2D.Float(),
    new Point2D.Float()
};
Point2D pointDest[] = new Point2D[3];
double[] doubleSrc = new double[6];
double[] doubleDest = new double[6];
float[] floatSrc = new float[6];
float[] floatDest = new float[6];
int srcOff = 0;
int dstOff = 0;
int numPts = 3; // array is (x,y) pairs...
// Point -> Point
trans.transform( srcPoint, destPoint );
// Point[] -> Point[]
trans.transform( pointSrc, srcOff, pointDest, dstOff, numPts );
// double[] -> double[]
trans.transform( doubleSrc, srcOff, doubleDest, dstOff, numPts );
// float[] -> float[]
trans.transform( floatSrc, srcOff, floatDest, dstOff, numPts );
// double[] -> float[]
trans.transform( doubleSrc, srcOff, floatDest, dstOff, numPts );
// float[] -> double[]
trans.transform( floatSrc, srcOff, doubleDest, dstOff, numPts );
// Shape -> Shape
destShape = trans.createTransformedShape( srcShape );
```

此处显示的最后一个示例，将一个 Shape 转换为另一个 Shape，在为其他操作（例如物理或碰撞检测）检索转换后的坐标时会带来困难。结果数据可以通过 PathIterator 获取，但其用法有点难以理解。路径迭代可以返回各种路径数据：

- SEG_MOVETO—新路径的起始位置
- SEG_LINETO—线条的第二个点
- SEG_QUADTO—指定二次参数曲线的两个点
- SEG_CUBICTO—指定三次参数曲线的三个点

请注意，可能会返回三个 (x,y) 对。以下代码转换一个矩形并遍历结果变换：

```
AffineTransform trans = new AffineTransform();
trans.rotate( Math.PI / 3.0 );
trans.translate( 5.0, 7.0 );
Shape shape = new Rectangle( 0, 0, 100, 150 );
Shape transformed = trans.createTransformedShape( shape );
PathIterator pit = transformed.getPathIterator( null );
float[ ] seg = new float[6];
while( !pit.isDone( ) ) {
    int segType = pit.currentSegment( seg );
    String point = "( " + seg[0] + ", " + seg[1] +
        " ),(" + seg[2] + ", " + seg[3] +
        " ),(" + seg[4] + ", " + seg[5] + ")";
    switch( segType ) {
        case PathIterator.SEG_MOVETO:
            System.out.println( "SEG_MOVETO: " + point );
            break;
        case PathIterator.SEG_LINETO:
            System.out.println( "SEG_LINETO: " + point );
            break;
        case PathIterator.SEG_QUADTO:
            System.out.println( "SEG_QUADTO: " + point );
            break;
        case PathIterator.SEG_CUBICTO:
            System.out.println( "SEG_CUBICTO: " + point );
            break;
        case PathIterator.SEG_CLOSE:
            System.out.println( "SEG_CLOSE: " + point );
            break;
    }
    pit.next();
}
```

## 资源与进一步阅读

Akenine-Moller, Tomas 和 Eric Haines, 《实时渲染》. 第2版, A K Peters, 2002.

Ericson, Christer, 《实时碰撞检测》, Focal Press, 2004.

## 第4章

![](img/588a4cda8f2acae94a7e1987bf99400d_107_0.png)

## 时间与空间

当我学习游戏编程时，我想做一些涉及物理的事情，于是搜索了一些方程式并阅读了关于运动的教程。接着，我尝试编写一些涉及重力的代码，并努力做得正确，以便我的计算机程序中的重力与地球上的重力相同。当我读到重力是 9.8 m/s² 时，我停下来，盯着电脑看了一会儿，完全不知道从何入手。我没有类似米的东西，也没有秒。我束手无策。正是在这一点上，我开始意识到计算机游戏可能有多难。本章的目标是向游戏循环添加时间步长，以便进行涉及时间的计算。它还涵盖屏幕映射，以便任何任意坐标系都可以绘制到任何大小的窗口上。

## 计算时间增量

之前的所有示例都在每一帧更新移动对象。这会导致不同计算机速度的对象移动速度取决于帧率而快慢不同。参见图 4.1。

