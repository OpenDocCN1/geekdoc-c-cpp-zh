

剪切矩阵如下：

```
[ 1, sx, 0 ]   [x]
Shear [sy, 1, 0] * V[Wy]
[ 0, 0, 1 ]   [w]
```

```
Vx = 1*x + sx*y + 0*w = x + sx*y
Vy = sy*x + 1*y + 0*w = y + sy*x
Vw = 0*x + 0*y + 1*w = w
```

最后，旋转矩阵如下：

```
[cos(a), -sin(a), 0]   [x]
Rotation [sin(a), cos(a), 0] * V[Wy]
[ 0, 0, 1 ]   [w]
```

```
Vx = x*cos(a) + -y*sin(a) + 0*w = x*cos(a) - y*sin(a)
Vy = x*sin(a) + y*cos(a) + 0*w = x*sin(a) + y*cos(a)
Vw = 0*x + 0*y + 1*w = w
```

这也与先前显示的向量类中的旋转代码相匹配。

```java
package javagames.util;
```

```java
public class Matrix3x3f {

    private float[][] m = new float[3][3];

    public Matrix3x3f() {
    }

    public Matrix3x3f( float[][] m ) {
        setMatrix( m );
    }

    public Matrix3x3f add( Matrix3x3f m1 ) {
        return new Matrix3x3f( new float[][] {
            { this.m[ 0 ][ 0 ] + m1.m[ 0 ][ 0 ],
                this.m[ 0 ][ 1 ] + m1.m[ 0 ][ 1 ],
                this.m[ 0 ][ 2 ] + m1.m[ 0 ][ 2 ] },
            { this.m[ 1 ][ 0 ] + m1.m[ 1 ][ 0 ],
                this.m[ 1 ][ 1 ] + m1.m[ 1 ][ 1 ],
                this.m[ 1 ][ 2 ] + m1.m[ 1 ][ 2 ] },
            { this.m[ 2 ][ 0 ] + m1.m[ 2 ][ 0 ],
                this.m[ 2 ][ 1 ] + m1.m[ 2 ][ 1 ],
                this.m[ 2 ][ 2 ] + m1.m[ 2 ][ 2 ] } } );
    }

    public Matrix3x3f sub( Matrix3x3f f1 ) {
        return new Matrix3x3f( new float[][] {
            { this.m[ 0 ][ 0 ] - f1.m[ 0 ][ 0 ],
                this.m[ 0 ][ 1 ] - f1.m[ 0 ][ 1 ],
                this.m[ 0 ][ 2 ] - f1.m[ 0 ][ 2 ] },
            { this.m[ 1 ][ 0 ] - f1.m[ 1 ][ 0 ],
                this.m[ 1 ][ 1 ] - f1.m[ 1 ][ 1 ],
                this.m[ 1 ][ 2 ] - f1.m[ 1 ][ 2 ] },
            { this.m[ 2 ][ 0 ] - f1.m[ 2 ][ 0 ],
                this.m[ 2 ][ 1 ] - f1.m[ 2 ][ 1 ],
                this.m[ 2 ][ 2 ] - f1.m[ 2 ][ 2 ] } } );
    }

    public Matrix3x3f mul( Matrix3x3f f1 ) {
        return new Matrix3x3f( new float[][] {
            { this.m[ 0 ][ 0 ] * f1.m[ 0 ][ 0 ] + this.m[ 0 ][ 1 ] * f1.m[ 1 ][ 0 ] + this.m[ 0 ][ 2 ] * f1.m[ 2 ][ 0 ],
                this.m[ 0 ][ 0 ] * f1.m[ 0 ][ 1 ] + this.m[ 0 ][ 1 ] * f1.m[ 1 ][ 1 ] + this.m[ 0 ][ 2 ] * f1.m[ 2 ][ 1 ],
                this.m[ 0 ][ 0 ] * f1.m[ 0 ][ 2 ] + this.m[ 0 ][ 1 ] * f1.m[ 1 ][ 2 ] + this.m[ 0 ][ 2 ] * f1.m[ 2 ][ 2 ] },
            { this.m[ 1 ][ 0 ] * f1.m[ 0 ][ 0 ] + this.m[ 1 ][ 1 ] * f1.m[ 1 ][ 0 ] + this.m[ 1 ][ 2 ] * f1.m[ 2 ][ 0 ],
                this.m[ 1 ][ 0 ] * f1.m[ 0 ][ 1 ] + this.m[ 1 ][ 1 ] * f1.m[ 1 ][ 1 ] + this.m[ 1 ][ 2 ] * f1.m[ 2 ][ 1 ],
                this.m[ 1 ][ 0 ] * f1.m[ 0 ][ 2 ] + this.m[ 1 ][ 1 ] * f1.m[ 1 ][ 2 ] + this.m[ 1 ][ 2 ] * f1.m[ 2 ][ 2 ] },
            { this.m[ 2 ][ 0 ] * f1.m[ 0 ][ 0 ] + this.m[ 2 ][ 1 ] * f1.m[ 1 ][ 0 ] + this.m[ 2 ][ 2 ] * f1.m[ 2 ][ 0 ],
                this.m[ 2 ][ 0 ] * f1.m[ 0 ][ 1 ] + this.m[ 2 ][ 1 ] * f1.m[ 1 ][ 1 ] + this.m[ 2 ][ 2 ] * f1.m[ 2 ][ 1 ],
                this.m[ 2 ][ 0 ] * f1.m[ 0 ][ 2 ] + this.m[ 2 ][ 1 ] * f1.m[ 1 ][ 2 ] + this.m[ 2 ][ 2 ] * f1.m[ 2 ][ 2 ] }
        } );
    }

    public void setMatrix( float[][] m ) {
        this.m = m;
    }

    public static Matrix3x3f zero() {
        return new Matrix3x3f( new float[][] {
            { 0.0f, 0.0f, 0.0f },
            { 0.0f, 0.0f, 0.0f },
            { 0.0f, 0.0f, 0.0f }
        });
    }

    public static Matrix3x3f identity() {
        return new Matrix3x3f( new float[][] {
            { 1.0f, 0.0f, 0.0f },
            { 0.0f, 1.0f, 0.0f },
            { 0.0f, 0.0f, 1.0f }
        });
    }

    public static Matrix3x3f translate( Vector2f v ) {
        return translate( v.x, v.y );
    }

    public static Matrix3x3f translate( float x, float y ) {
        return new Matrix3x3f( new float[][] {
            { 1.0f, 0.0f, 0.0f },
            { 0.0f, 1.0f, 0.0f },
            { x, y, 1.0f }
        });
    }

    public static Matrix3x3f scale( Vector2f v ) {
        return scale( v.x, v.y );
    }

    public static Matrix3x3f scale( float x, float y ) {
        return new Matrix3x3f( new float[][] {
            { x, 0.0f, 0.0f },
            { 0.0f, y, 0.0f },
            { 0.0f, 0.0f, 1.0f }
        });
    }

    public static Matrix3x3f shear( Vector2f v ) {
        return shear( v.x, v.y );
    }

    public static Matrix3x3f shear( float x, float y ) {
        return new Matrix3x3f( new float[][] {
            { 1.0f, y, 0.0f },
            { x, 1.0f, 0.0f },
            { 0.0f, 0.0f, 1.0f }
        } );
    }

    public static Matrix3x3f rotate( float rad ) {
        return new Matrix3x3f( new float[][] {
            { (float) Math.cos( rad ), (float) -Math.sin( rad ), 0.0f },
            { (float) Math.sin( rad ), (float) Math.cos( rad ), 0.0f },
            { 0.0f, 0.0f, 1.0f }
        } );
    }

    public Vector2f mul( Vector2f vec ) {
        return new Vector2f(
            vec.x * this.m[ 0 ][ 0 ] + vec.y * this.m[ 0 ][ 1 ] + this.m[ 0 ][ 2 ],
            vec.x * this.m[ 1 ][ 0 ] + vec.y * this.m[ 1 ][ 1 ] + this.m[ 1 ][ 2 ]
        );
    }

    @Override
    public String toString() {
        StringBuilder buf = new StringBuilder();
        for ( int i = 0; i < 3; ++i ) {
            buf.append( "" );
            buf.append( m[ i ][ 0 ] );
            buf.append( ", " );
            buf.append( m[ i ][ 1 ] );
            buf.append( ", " );
            buf.append( m[ i ][ 2 ] );
            buf.append( "]\n" );
        }
        return buf.toString();
    }
}
```

![](img/588a4cda8f2acae94a7e1987bf99400d_98_0.png)

图 3.9
矩阵乘法示例。
© 2014 Timothy Wright.

位于 javagames.transform 包中并如图 3.9 所示的 MatrixMultiplicationExample 演示了如何使用矩阵对对象串联变换操作。矩阵之所以是如此强大的工具，是因为诸如变换和旋转之类的操作可以存储到单个矩阵中，然后一次性应用到对象上。虽然对于单个对象来说这并非必要，但如果需要转换数百或数千个多边形，节省的开销真的可以累积起来。

> **提示**
> 仅供娱乐，此示例还会创建一些随机星星，可以使用“空格”键打开或关闭（明白吗？）。

将单位矩阵作为起点，然后乘以一个将对象移动到屏幕中心的平移矩阵。接着将太阳向量乘以该矩阵，使太阳的中心位于屏幕中心。虽然这只是一个点，但整个多边形模型都可以乘以该矩阵来转换所有坐标。

地球轨道的路径被绘制为一个白色圆圈，然后绘制地球，使其围绕太阳旋转。请注意，使用的是同一个矩阵。将地球的旋转与先前的矩阵串联，可以让地球只需再进行一次旋转和平移就围绕太阳旋转。本示例与前一个示例的区别很重要。有关先旋转再平移与先平移再旋转的区别，请参见图 3.10 和图 3.11。

![](img/588a4cda8f2acae94a7e1987bf99400d_99_0.png)

图 3.10 平移 -> 旋转。© 2014 Timothy Wright.

![](img/588a4cda8f2acae94a7e1987bf99400d_99_1.png)

图 3.11 旋转 -> 平移。© 2014 Timothy Wright.

仍然使用同一个矩阵，另一个代表月球的圆圈围绕地球运行。这两颗行星都围绕太阳运行。使用矩阵乘法，这一切都是可能的，而且非常简单。请务必研究代码，直到结果变得合理。

```java
package javagames.transform;
import java.awt.*;
import java.awt.event.*;
import java.awt.image.*;
import java.util.Random;
import javagames.util.*;
import javax.swing.*;
import javagames.swing.*;
```

```java
public class MatrixMultiplyExample extends JFrame implements Runnable {
	private static final int SCREEN_W = 640;
	private static final int SCREEN_H = 480;

	private FrameRate frameRate;
	private BufferStrategy bs;
	private volatile boolean running;
	private Thread gameThread;
	private RelativeMouseInput mouse;
	private KeyboardInput keyboard;

	private float earthRot, earthDelta;
	private float moonRot, moonDelta;

	private boolean showStars;
	private int[] stars;
	private Random rand = new Random();
	public MatrixMultiplyExample() {
	}

	protected void createAndShowGUI() {
		Canvas canvas = new Canvas();
		canvas.setSize( SCREEN_W, SCREEN_H );
		canvas.setBackground( Color.BLACK );
		canvas.setIgnoreRepaint( true );
		getContentPane().add( canvas );
		setTitle( "Matrix Multiply Example" );
		setIgnoreRepaint( true );
		pack();

		// Add key listeners
		keyboard = new KeyboardInput();
		canvas.addKeyListener( keyboard );
```

