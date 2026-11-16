

![](img/588a4cda8f2acae94a7e1987bf99400d_501_0.png)

图 15.28 简单碰撞问题。© 2014 Timothy Wright.

为了防止初始接触或几乎接触多边形的点卡住，必须忽略这些点。但这会引起另一个问题。如果新位置几乎接触多边形，它将在下一帧之前不会与多边形相交，但到那时，由于它非常接近，会被忽略，因此不会卡住。这会导致点如果在多边形线前方停止，会直接穿过它。

```
if end-point really close to the line
    collision has occurred
else if start-point really close to the line
    ignore it, or it will get stuck
```

这段伪代码描述了防止点粘在多边形线上或穿过多边形线所需的检查。

图 15.29 所示的方程用于查找点 P 到 SQ 线段的有符号垂直距离。请记住对法向量进行归一化。此距离值可用于检查点是否接触或几乎接触线段。

![](img/588a4cda8f2acae94a7e1987bf99400d_501_1.png)

图 15.29 垂直点距离。© 2014 Timothy Wright.

在使用碰撞后更新点位置的更准确方法时，也存在问题。如果反射发生在角上，新位置可能会跳过应引起碰撞的线。如图 15.30 所示。

![](img/588a4cda8f2acae94a7e1987bf99400d_502_0.png)

图 15.30 角错误修正。© 2014 Timothy Wright.

每次发现碰撞时，都必须检查新反射向量与整个多边形的碰撞。虽然大多数物体移动得不够快，不会成为问题，但这可能会在角落周围引起大量检查。

仅将点保留在原位的第二个问题也可能发生在角上，但涉及多次碰撞。

![](img/588a4cda8f2acae94a7e1987bf99400d_502_1.png)

图 15.31 顺时针/逆时针测试。© 2014 Timothy Wright.

如图 15.31 所示，存在两种不同的碰撞。如果按顺时针或逆时针检查多边形边，第一个碰撞点将会改变。不仅每次碰撞都会导致更多碰撞检查，所有碰撞都必须检查多次碰撞，测量到每次碰撞的距离，并且只使用最近的一个。

使用哪种方法取决于所需的准确度级别。请务必处理可能发生的奇怪情况。

![](img/588a4cda8f2acae94a7e1987bf99400d_503_0.png)

图 15.32 弹跳点示例。© 2014 Timothy Wright.

如图 15.32 所示且位于 javagames.collision 包中的 BouncingPointExample，会创建具有随机速度方向和距离的随机点，并在多边形内部让它们弹跳。EPSILON 值用于检查非常接近零的值。生成的点数可以调整。pointCount 变量保存当前点数，点和速度存储在各自的数组中。polygon 数组保存原始多边形，副本保存视口变换后的坐标。

initialize() 方法使用硬编码点创建多边形，并使用 createPoints() 方法创建初始随机点。每当重置点时，都会调用此方法。

processInput() 方法使用方向键增加或减少点数，并使用空格键重新启动点。clamp() 方法使点保持在 MIN_POINTS 和 MAX_POINTS 常数之间。

updateObjects() 方法根据每个点的速度更新其位置，如果发生碰撞，则计算新速度。此示例用于碰撞检测使用了简单方法，因此仅在没有碰撞时才更新每个点的位置。getNewVelocity() 方法在点与多边形边发生碰撞时返回该点的新速度。以下代码确保点不会穿过或粘在多边形上。

```
private boolean hitPolygon(
    Vector2f start, Vector2f end, Vector2f S, Vector2f P ) {
    if( isZero( getPointLineDistance( end, S, P ) ) ) {
        return true;
    } else if( !isZero( getPointLineDistance( start, S, P ) ) ) {
        return lineLineIntersection( start, end, S, P );
    } else {
        return false;
    }
}
```

getPointLineDistance() 方法计算给定点到线段的距离，以便可以使用到每条线段的距离来防止点粘连。lineLineIntersection() 方法只需在存在交点时返回即可。不需要实际交点位置。calculateReflection() 方法用于将每个点从多边形边弹开。最后，render() 方法显示常规说明，绘制多边形，并将每个点绘制为微小矩形。

```
package javagames.collision;

import java.awt.Graphics;
import java.awt.event.KeyEvent;
import java.util.Random;
import javagames.util.*;

public class BouncingPointExample extends SimpleFramework {
    private static final float EPSILON = 0.000001f;
    private static final int MAX_POINTS = 4096;
    private static final int MIN_POINTS = 8;
    private static final int MULTIPLE = 2;

    private int pointCount;
    private Vector2f[] points;
    private Vector2f[] velocities;
    private Vector2f[] polygon;
    private Vector2f[] polygonCpy;

    public BouncingPointExample() {
        appTitle = "Bouncing Point Example";
        appWidth = 640;
        appHeight = 640;
        appSleep = 1L;
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    protected void initialize() {
        super.initialize();

        polygon = new Vector2f[] {
            new Vector2f( 0.09233177f, -0.22378719f),
            new Vector2f(-0.21752739f, 0.16431928f),
            new Vector2f(-0.37089205f, 0.14553994f),
            new Vector2f(-0.46478873f, 0.32707357f),
            new Vector2f(-0.21439749f, 0.41784036f),
            new Vector2f(-0.05790299f, 0.31768388f),
            new Vector2f(-0.107981205f, 0.17370892f),
            new Vector2f( 0.08607197f, -0.101721406f),
            new Vector2f( 0.2832551f, -0.042253494f),
            new Vector2f( 0.12989044f, 0.29577464f),
            new Vector2f( 0.4522692f, 0.042253554f),
            new Vector2f( 0.5054773f, 0.32707357f),
            new Vector2f( 0.5899843f, -0.098591566f),
            new Vector2f( 0.85289514f, -0.08920181f),
            new Vector2f( 0.5117371f, -0.18935835f),
            new Vector2f( 0.458529f, -0.5649452f),
            new Vector2f( 0.3552426f, -0.08920181f),
            new Vector2f( 0.16744912f, -0.22378719f),
            new Vector2f( 0.33959305f, -0.342723f),
            new Vector2f( 0.26760566f, -0.5962441f),
            new Vector2f(-0.17370892f, -0.56807506f),
            new Vector2f(-0.22065729f, -0.26134586f),
        };
        polygonCpy = new Vector2f[polygon.length];
        pointCount = MIN_POINTS;
        createPoints();
    }

    private void createPoints() {
        Random rand = new Random();
        points = new Vector2f[ pointCount ];
        velocities = new Vector2f[ points.length ];
        for (int i = 0; i < points.length; ++i ) {
            points[i] = new Vector2f();
            double rad = Math.toRadians( rand.nextInt( 360 ) );
            double distancePerSecond = rand.nextFloat() + 0.5f;
            float vx = (float)(distancePerSecond * Math.cos( rad ));
            float vy = (float)(distancePerSecond * Math.sin( rad ));
            velocities[i] = new Vector2f( vx, vy );
        }
    }

    protected void processInput( float delta ) {
        super.processInput( delta );
        if ( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
            createPoints();
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_UP ) ) {
            pointCount = clamp( pointCount * MULTIPLE );
            createPoints();
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_DOWN ) ) {
            pointCount = clamp( pointCount / MULTIPLE );
            createPoints();
        }
    }

    private int clamp( int count ) {
        if ( count < MIN_POINTS ) return MIN_POINTS;
        if ( count > MAX_POINTS ) return MAX_POINTS;
        return count;
    }

    protected void updateObjects( float delta ) {
        super.updateObjects( delta );
        for ( int i = 0; i < points.length; ++i ) {
            Vector2f velocity = velocities[i];
            Vector2f start = points[i];
            Vector2f end = start.add( velocity.mul( delta ) );
            Vector2f newVelocity = getNewVelocity( start, end, velocity );
            if( newVelocity != null ) {
                velocities[i] = newVelocity;
            } else
                points[i] = end;
        }
    }

    private Vector2f getNewVelocity(
        Vector2f start, Vector2f end, Vector2f velocity ) {

