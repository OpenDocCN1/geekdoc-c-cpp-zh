

![](img/588a4cda8f2acae94a7e1987bf99400d_221_0.png)

图 8.10
随机小行星示例。
© 2014 Timothy Wright.

getRandomAsteroid() 方法创建一个随机位置，然后选择一个随机大小：小、中或大。请记住，工厂的每个方法为每种大小从三种不同的多边形模型中选择一个，并为每个模型生成四个镜像版本。每个多边形有四个镜像，每种大小有三种形状，共有三种大小，因此总共有 36 个不同的模型。

还要注意，因为 PrototypeAsteroid 使用了新的 Utility.fillPolygon() 方法，所以 Graphics 对象被强制转换为 Graphics2D 对象。

```java
// RandomAsteroidExample.java
protected void render( Graphics g ) {
    super.render( g );
    g.drawString( "Press ESC to respawn", 20, 35 );
    Matrix3x3f view = getViewportTransform();
    for( PrototypeAsteroid asteroid : asteroids ) {
        asteroid.draw( (Graphics2D)g, view );
    }
}
```

RandomAsteroidExample 代码如下：

```java
package javagames.prototype;

import java.awt.*;
import java.awt.event.KeyEvent;
import java.util.*;
import javagames.prototype.PrototypeAsteroid.Size;
import javagames.util.*;

public class RandomAsteroidExample extends SimpleFramework {
	private PrototypeAsteroidFactory factory;
	private ArrayList<PrototypeAsteroid> asteroids;
	private Random rand;

	public RandomAsteroidExample() {
		appBorderScale = 0.9f;
		appWidth = 640;
		appHeight = 640;
		appMaintainRatio = true;
		appSleep = 1L;
		appTitle = "Random Asteroids";
		appBackground = Color.WHITE;
		appFPSColor = Color.BLACK;
	}

	@Override
	protected void initialize() {
		super.initialize();

		rand = new Random();
		asteroids = new ArrayList<PrototypeAsteroid>();
		PolygonWrapper wrapper =
			new PolygonWrapper( appWidth, appWorldHeight );
		factory = new PrototypeAsteroidFactory( wrapper );
		createAsteroids();
	}

	private void createAsteroids() {
		asteroids.clear();
		for ( int i = 0; i < 42; ++i ) {
			asteroids.add( getRandomAsteroid() );
		}
	}

	private PrototypeAsteroid getRandomAsteroid() {
		float x = rand.nextFloat() * 2.0f - 1.0f;
		float y = rand.nextFloat() * 2.0f - 1.0f;
		Vector2f position = new Vector2f( x, y );
		Size[] sizes = Size.values();
		Size randomSize = sizes[ rand.nextInt( sizes.length ) ];
		switch( randomSize ) {
		    case Small: return factory.createSmallAsteroid( position );
		    case Medium: return factory.createMediumAsteroid( position );
		    case Large:
		    default: return factory.createLargeAsteroid( position );
		}
	}

	@Override
	protected void processInput( float delta ) {
	    super.processInput( delta );
	    if( keyboard.keyDownOnce( KeyEvent.VK_ESCAPE ) ) {
	        createAsteroids();
	    }
	}

	@Override
	protected void updateObjects( float delta ) {
	    super.updateObjects( delta );
	    for( PrototypeAsteroid asteroid : asteroids ) {
	        asteroid.update( delta );
	    }
	}

	@Override
	protected void render( Graphics g ) {
	    super.render( g );
	    g.drawString( "Press ESC to respawn", 20, 35 );
	    Matrix3x3f view = getViewportTransform();
	    for( PrototypeAsteroid asteroid : asteroids ) {
	        asteroid.draw( (Graphics2D)g, view );
	    }
	}

	public static void main( String[] args ) {
	    launchApp( new RandomAsteroidExample() );
	}
}
```

## PROTOTYPE BULLET 类

PrototypeBullet 代码同样位于 javagames.prototype 包中，是最简单的原型游戏源代码。除了绘制圆形以便屏幕可以调整大小之外，没有什么值得讨论的。

```java
package javagames.prototype;

import java.awt.*;
import javagames.util.*;

public class PrototypeBullet {
    private Vector2f velocity;
    private Vector2f position;
    private Color color;
    private float radius;

    public PrototypeBullet( Vector2f position, float angle ) {
        this.position = position;
        velocity = Vector2f.polar( angle, 1.0f );
        radius = 0.006f;
        color = Color.GREEN;
    }

    public Vector2f getPosition() {
        return position;
    }

    public void draw( Graphics2D g, Matrix3x3f view ) {
        g.setColor( color );
        Vector2f topLeft = new Vector2f(
                position.x - radius, position.y + radius );
        topLeft = view.mul( topLeft );
        Vector2f bottomRight = new Vector2f(
                position.x + radius, position.y - radius );
        bottomRight = view.mul( bottomRight );

        int circleX = (int)topLeft.x;
        int circleY = (int)topLeft.y;
        int circleWidth = (int)(bottomRight.x - topLeft.x);
        int circleHeight = (int)(bottomRight.y - topLeft.y);
        g.fillOval(
                circleX, circleY, circleWidth, circleHeight
        );
    }

    public void update( float time ) {
        position = position.add( velocity.mul( time ) );
    }
}
```

## PROTOTYPE SHIP 类

PrototypeShip 代码位于 javagames.prototype 包中，大部分不言自明。构造函数设置了一些用于移动飞船的常量，并对模型点进行了硬编码。有用于损坏状态、角度、推进的 set*() 和 get*() 方法，以及用于向左或向右旋转飞船的方法。

launchBullet() 方法返回一个新的 PrototypeBullet 对象，并将其移动到飞船的机头处。

```java
// PrototypeShip.java
public PrototypeBullet launchBullet() {
    Vector2f bulletPos = position.add( Vector2f.polar( angle, 0.0325f ) );
    return new PrototypeBullet( bulletPos, angle );
}
```

isTouching() 方法检查与给定小行星对象的渲染列表中每艘飞船的碰撞。精彩的部分是 updatePosition() 方法，它驱动飞船飞行。首先，更新速度：

$V_1 = V_0 + at$

加速度在 setThrusting() 方法中设置。如果飞船没有向前移动，则加速度为 0，速度保持不变。请注意，新的加速度向量使用当前角度，这会慢慢改变飞船行驶的方向。

```java
Vector2f accel = Vector2f.polar(angle, curAcc);
```

接下来，将新速度保持在最大值以下。如果不执行此操作，飞船将继续加速，最终速度会超过子弹。请注意，使用的是最小值，因此当最大速度不小于实际速度时，最大速度为 1.0，没有任何变化。只有当最大速度小于实际值时，速度才会受到限制。

```java
float maxSpeed = Math.min( maxVelocity / velocity.len(), 1.0f );
velocity = velocity.mul( maxSpeed );
```

接下来，应用摩擦力。尽管太空中没有摩擦力，但我想为飞船添加摩擦力，以便它最终会减速。如果飞船没有加速，摩擦力会持续减速。

```java
float slowDown = 1.0f - friction * time;
velocity = velocity.mul( slowDown );
```

最后，更新位置并将其包装。

```java
position = position.add( velocity.mul( time ) );
position = wrapper.wrapPosition( position );
```

PrototypeShip 代码如下：

```java
package javagames.prototype;

import java.awt.*;
import java.util.ArrayList;
import javagames.util.*;

public class PrototypeShip {
	private float angle;
	private float acceleration;
	private float friction;
	private float maxVelocity;
	private float rotationDelta;
	private float curAcc;

	private Vector2f position;
	private Vector2f velocity;

	private PolygonWrapper wrapper;

	private boolean damaged;

	private Vector2f[] polygon;
	private ArrayList<Vector2f[]> renderlist;

	public PrototypeShip( PolygonWrapper wrapper ) {
		this.wrapper = wrapper;

		friction = 0.25f;
		rotationDelta = (float)Math.toRadians( 180.0 );
		acceleration = 1.0f;
		maxVelocity = 0.5f;
		velocity = new Vector2f();

		position = new Vector2f();
		polygon = new Vector2f[] {
			new Vector2f( 0.032f, 0.0f ),
			new Vector2f( -0.032f, -0.032f ),
			new Vector2f( 0.0f, 0.0f ),
			new Vector2f( -0.032f, 0.032f ),
		};

		renderList = new ArrayList<Vector2f[]>();
	}
}
```

