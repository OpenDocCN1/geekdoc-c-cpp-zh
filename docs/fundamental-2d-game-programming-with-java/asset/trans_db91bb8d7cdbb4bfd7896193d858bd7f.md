

## 计算反射向量

一旦找到交点，就可以计算反射向量。该向量是物体沿线段反弹的方向。参见图 15.21。

![](img/588a4cda8f2acae94a7e1987bf99400d_494_0.png)

图 15.21 反射向量。© 2014 Timothy Wright.

可以通过线段相交测试找到交点。计算反射向量只需要原始向量和反射段的垂直向量。反射向量的计算方法如下：

如图 15.22 所示，向量 V 是原始方向向量。它沿线段 AB 反射。法线是垂直于 AB 线段的单位向量。

![](img/588a4cda8f2acae94a7e1987bf99400d_494_1.png)

图 15.22 反射向量证明。© 2014 Timothy Wright.

反射向量的计算方法如下：

$$V_n = \hat{n}(V * \hat{n})$$
$$V_p = V - V_n$$
$$V' = V_p - V_n$$

要将方向沿线段反射，交点用于创建原始反射向量，以及反射的起点。参见图 15.23。

![](img/588a4cda8f2acae94a7e1987bf99400d_495_0.png)

图 15.23 反射向量分量。© 2014 Timothy Wright.

$$S_V = S_1 - S_0$$
$$n = S_V^{\perp}$$

l 是 Q 和 P 的交点。Q = P1-l，Q' 是反射。

![](img/588a4cda8f2acae94a7e1987bf99400d_496_0.png)

图 15.24 反射向量示例。© 2014 Timothy Wright.

如图 15.24 所示且位于 javagames.collision 包中的 ReflectionVectorExample 计算沿线段的反射。EPSILON 值用于检查平行线。变量 s0、s1、p0 和 p1 保存两条线段。交点向量保存两条直线的交点，反射向量保存从两条线段计算出的反射。s0 和 s1 线段保持原位，p0 点在单击左键时放置，p1 点跟随鼠标。

updateObjects() 方法使用前面描述的直线-直线相交算法计算交点。如果找到交点，则计算反射向量。如果没有交点，则将反射向量设置为 null。

getIntersection() 方法计算交点，返回单个交点而不是两个参数化直线值。getReflectionVector() 方法根据初始方向向量和垂直于反射表面的单位向量计算反射。

render() 方法绘制通常的帧率和使用信息。drawLine() 方法转换并绘制线段。ReflectionVectorExample 如下：

```
package javagames.collision;

import java.awt.*;

import java.awt.event.MouseEvent;

import javagames.util.*;

public class ReflectionVectorExample extends SimpleFramework {

    private static final float EPSILON = 0.00001f;

    private Vector2f s0, s1, p0, p1;
    private Vector2f intersection;
    private Vector2f reflection;

    public ReflectionVectorExample() {
        appTitle = "Reflection Vector Example";
        appBackground = Color.WHITE;
        appFPSCColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();

        s0 = new Vector2f( -0.75f, -0.3f );
        s1 = new Vector2f( 0.75f, -0.1f );
        p0 = new Vector2f();
        p1 = new Vector2f();
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );

        p1 = getWorldMousePosition();
        if( mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
            p0 = new Vector2f( p1 );
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );

        intersection = getIntersection( p0, p1, s0, s1 );
        if( intersection != null ) {
            Vector2f Sv = s1.sub( s0 );
            Vector2f n = Sv.perp().norm();
            Vector2f V = p1.sub( intersection );
            Vector2f reflect = getReflectionVector( V, n );
            reflection = intersection.add( reflect );
        } else {
            reflection = null;
        }
    }
}
private Vector2f getIntersection(
    Vector2f A, Vector2f B, Vector2f C, Vector2f D ) {
    Vector2f DsuB = D.sub( C ) ;
    Vector2f DsuBperp = DsuB.perp() ;
    Vector2f AsuB = A.sub( B ) ;
    float f = DsuBperp.dot( DsuB ) ;
    if ( Math.abs( f ) < EPSILON ) {
        return null ; // zero denom
    }
    Vector2f AsuC = A.sub( C ) ;
    float d = DsuBperp.dot( AsuC ) ;
    if ( f > 0 ) {
        if ( d < 0 || d > f ) return null ;
    } else {
        if ( d > 0 || d < f ) return null ;
    }
    Vector2f BsuA = B.sub( A ) ;
    Vector2f BsuAperp = BsuA.perp() ;
    float e = BsuAperp.dot( AsuC ) ;
    if ( f > 0 ) {
        if ( e < 0 || e > f ) return null ;
    } else {
        if ( e > 0 || e < f ) return null ;
    }
    return A.add( BsuA.mul( d / f ) ) ;
}

private Vector2f getReflectionVector( Vector2f V, Vector2f n ) {
    Vector2f Vn = n.mul( V.dot( n ) ) ;
    Vector2f Vp = V.sub( Vn ) ;
    return Vp.sub( Vn ) ;
}

@Override
protected void render( Graphics g ) {
    super.render( g ) ;
    g.drawString( "Left Click to move line", 20, 35 ) ;
    drawLine( g, s0, s1 ) ;
    drawLine( g, p0, p1 ) ;
    if ( reflection != null ) {
        g.setColor( Color.BLUE ) ;
        drawLine( g, intersection, reflection ) ;
    }
}

private void drawLine( Graphics g, Vector2f v0, Vector2f v1 ) {
    Matrix3x3f view = getViewportTransform();
    Vector2f v0Cpy = view.mul( v0 );
    Vector2f v1Cpy = view.mul( v1 );
    g.drawLine( (int)v0Cpy.x, (int)v0Cpy.y, (int)v1Cpy.x, (int)v1Cpy.y );
}

public static void main( String[] args ) {
    launchApp( new ReflectionVectorExample() );
}
}
```

## 在多边形内弹跳点

尝试将对象弹离多边形边缘时，有多种方法来处理碰撞响应。一种方法是只计算反射向量并调整点的速度，如图 15.25 所示。这种方法简单，但不能准确建模碰撞。

![](img/588a4cda8f2acae94a7e1987bf99400d_499_0.png)

图 15.25 简单反射。© 2014 Timothy Wright.

这种简单方法根据速度计算新的点位置，如果由起点和终点形成的线段与多边形相交，则点保留在起始位置并更新速度。

处理碰撞的另一种方法是计算交点、反射向量并更新对象的位置。如图 15.26 所示。

![](img/588a4cda8f2acae94a7e1987bf99400d_500_0.png)

图 15.26. 正确反射。© 2014 Timothy Wright.

不幸的是，两种方法都有问题。正确方法必须准确调整点，然后递归继续检查碰撞，直到没有更多碰撞或弹跳距离太小。此时，正确方法将遭受与简单方法相同的一些问题。为了尽可能保持简单，将使用简单方法。

简单方法也有许多问题。首先，只有在发生碰撞时才更新点的位置，如果点每帧移动的距离足够远，它将总是撞到某物，点将永远不会移动。参见图 15.27。

![](img/588a4cda8f2acae94a7e1987bf99400d_500_1.png)

图 15.27 点将永远不会移动。© 2014 Timothy Wright.

仅将点保留在原位的第二个问题是，当点非常靠近直线时会发生这种情况。如果点开始时接触或几乎接触多边形直线，则它将始终注册碰撞，并会粘在直线上。参见图 15.28。

