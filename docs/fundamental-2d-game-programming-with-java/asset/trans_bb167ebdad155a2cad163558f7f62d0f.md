

![](img/588a4cda8f2acae94a7e1987bf99400d_487_0.png)

图 15.17
线-线相交。
© 2014 Timothy Wright。

要查找交点，使用点积的一个属性。

$A * B^{\perp} = 0$

回想一下，两个垂直向量的点积始终为零。此方程用作起点。将参数线方程代入此方程，从而可以找到 t 值。参见图 15.18。

![](img/588a4cda8f2acae94a7e1987bf99400d_487_1.png)

图 15.18
线-线分量。
© 2014 Timothy Wright。

```
n1 * (X - C) = 0
n1 * [A + t(B - A) - C] = 0
n1 * [t(B - A) + (A - C)] = 0
n1 * t(B - A) + n1(A - C) = 0
n1 * t(B - A) = -n1 * (A - C)
```

```
t * [n_1 * (B - A)] = n_1 * (C - A)
t_1 = \frac{n_1 * (C - A)}{n_1 * (B - A)} = \frac{(D - C)^\perp * (C - A)}{(D - C)^\perp * (B - A)}
```

如果之前示例中的直线互换位置，则另一个 t 值为：

```
t_2 = \frac{n_2 * (A - C)}{n_2 * (D - C)} = \frac{(B - A)^\perp * (A - C)}{(B - A)^\perp * (D - C)}
```

如果分母值中的任何一个为零，则直线平行且不存在交点：

```
n * (B - A) = 0
n * (D - C) = 0
```

此外，需要检查每个 t 值是否介于零和一之间。由于两者都介于零和一之间，因此存在交点：

```
0 \le t_1 \le 1
0 \le t_2 \le 1
```

可以通过找到公共分母值来简化算法。

![](img/588a4cda8f2acae94a7e1987bf99400d_488_0.png)

图 15.19 垂直向量。© 2014 Timothy Wright。

观察图 15.19 中的关系，很明显：

$A^+ * B = -A * B^\perp$

可以使用此关系重写 t 值方程，使它们共享相同的分母。

$t_1 = \frac{(D - C)^\perp * (C - A)}{(D - C)^\perp * (B - A)} = \frac{-[(D - C)^\perp * (A - C)]}{-[(D - C)^\perp * (A - B)]} = \frac{(D - C)^\perp * (A - C)}{(D - C)^\perp * (A - B)}$

$t_2 = \frac{(B - A)^\perp * (A - C)}{(B - A)^\perp * (D - C)} = \frac{-[(B - A)^\perp * (A - C)]}{-[(B - A)^\perp * (D - C)]} = \frac{(B - A)^\perp * (A - C)}{(D - C)^\perp * (A - B)}$

现在可以使用以下内容来计算交点值：

let d = (D - C)^\perp * (A - C)
e = (B - A)^\perp * (A - C)
f = (D - C)^\perp * (A - B)
t_1 = d/f
t_2 = e/f

由于除法是一项开销较大的操作，因此可以在执行除法之前验证范围是否介于零和一之间。

```
if f < 0
if d < 0 or d > f : no intersection
else
if d > 0 or d < f : no intersection
```

可以对 e 值执行相同的检查。如果这些检查均不为真，则两个交点值都将介于零和一之间且存在交点。完整算法如下：

```
private float[] LineLineIntersection(
Vector2f A, Vector2f B, Vector2f C, Vector2f D ) {
Vector2f DsubC = D.sub( C );
Vector2f DsubCperp = DsubC.perp();
Vector2f AsubB = A.sub( B );
float f = DsubCperp.dot( AsubB );
if( Math.abs( f ) < EPSILON ) {
return null; // zero denom
}
Vector2f AsubC = A.sub( C );
float d = DsubCperp.dot( AsubC );
if ( f > 0 ) {
    if( d < 0 || d > f ) return null;
} else {
    if( d > 0 || d < f ) return null;
}
Vector2f BsubA = B.sub( A );
Vector2f BsubAperp = BsubA.perp();
float e = BsubAperp.dot( AsubC );
if ( f > 0 ) {
    if( e < 0 || e > f ) return null;
} else {
    if( e > 0 || e < f ) return null;
}
return new float[]{
    d / f, e / f
};
}
```

图 15.20 线-线相交示例。© 2014 Timothy Wright。

![](img/588a4cda8f2acae94a7e1987bf99400d_490_0.png)

如图 15.20 所示且位于 javagames.collision 包中的 LineLineIntersectionExample，使用先前描述的算法查找两条线段之间的交点。EPSILON 值用于查看行列式是否为零，这发生在两条直线平行时。向量 A 和 B 构成第一条线段，向量 C 和 D 构成第二条线段。intersect 向量保存使用第一个 t 值找到的交点。如果不存在交点，则交点值为 null。

processInput() 方法将 D 向量设置为鼠标位置。左键单击设置其他三条线点中的每一个。单击右键清除所有点。updateObjects() 方法查找两条直线的交点，然后使用第一个返回值来计算交点。LineLineIntersection() 方法采用四个向量（每条线段两个），并以包含两个值的数组形式返回交点值，如果未找到交点则返回 null。

render() 方法绘制两条线段以及交点位置的准星。drawLine() 方法和 drawCrossHairs() 方法负责在屏幕上绘制符号。LineLineIntersectionExample 代码如下：

```
package javagames.collision;

import java.awt.*;
import java.awt.event.MouseEvent;
import javagames.util.*;

public class LineLineIntersectionExample extends SimpleFramework {
    private static final float EPSILON = 0.00001f;

    private Vector2f A, B, C, D;
    private Vector2f intersect;

    public LineLineIntersectionExample() {
        appTitle = "Line Line Intersection";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );

        D = getWorldMousePosition();

        if( mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
            if( A == null ) A = D;
            else if( B == null ) B = D;
            else C = D;
        }

        if (mouse.buttonDownOnce(MouseEvent.BUTTON3)) {
            A = B = C = D = null;
            intersect = null;
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );

        if ( A != null && B != null && C != null && D != null ) {
            float[] t = lineLineIntersection( A, B, C, D );
            if ( t == null ) {
                intersect = null;
            } else {
                intersect = A.add( B.sub( A ).mul( t[ 0 ] ) );
            }
        }
    }

    private float[] lineLineIntersection(
        Vector2f A, Vector2f B, Vector2f C, Vector2f D ) {
        Vector2f DsubC = D.sub( C );
        Vector2f DsubCperp = DsubC.perp( );
        Vector2f AsubB = A.sub( B );
        float f = DsubCperp.dot( AsubB );
        if ( Math.abs( f ) < EPSILON ) {
            return null; // zero denom
        }

        Vector2f AsubC = A.sub( C );
        float d = DsubCperp.dot( AsubC );
        if ( f > 0 ) {
            if ( d < 0 || d > f ) return null;
        } else {
            if ( d > 0 || d < f ) return null;
        }

        Vector2f BsubA = B.sub( A );
        Vector2f BsubAperp = BsubA.perp( );
        float e = BsubAperp.dot( AsubC );
        if ( f > 0 ) {
            if ( e < 0 || e > f ) return null;
        } else {
            if ( e > 0 || e < f ) return null;
        }
        return new float[]{
            d / f, e / f
        };
    }

    @Override
    protected void render( Graphics g ) {
        super.render( g );
        g.drawString( "Left Mouse to place points", 20, 35 );
        g.drawString( "Right Mouse to clear points", 20, 50 );
        g.setColor( intersect == null ? Color.RED : Color.GREEN );
        drawLine( g, A, B );
        drawLine( g, C, D );
        drawCrossHairs( g );
    }

    private void drawLine( Graphics g, Vector2f v0, Vector2f v1 ) {
        if( v0 != null ) {
            Matrix3x3f view = getViewportTransform();
            Vector2f va = view.mul( v0 );
            if( v1 == null ) {
                g.fillRect( (int)va.x, (int)va.y, 1, 1 );
            } else {
                Vector2f vb = view.mul( v1 );
                g.drawLine( (int)va.x, (int)va.y, (int)vb.x, (int)vb.y );
            }
        }
    }

    private void drawCrossHairs( Graphics g ) {
        if( intersect != null ) {
            Matrix3x3f view = getViewportTransform();
            Vector2f intView = view.mul( intersect );
            g.setColor( Color.BLACK );
            int x = (int)intView.x;
            int y = (int)intView.y;
            g.drawLine( x, y - 20, x, y + 20 );
            g.drawLine( x - 20, y, x + 20, y );
        }
    }

    public static void main( String[] args ) {
        launchApp( new LineLineIntersectionExample() );
    }
}
```

