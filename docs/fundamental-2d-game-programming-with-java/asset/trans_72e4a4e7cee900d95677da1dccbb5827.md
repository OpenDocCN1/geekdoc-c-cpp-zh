

```java
Vector2f screen = view.mul( position );
AffineTransform transform =
AffineTransform.getTranslateInstance( screen.x, screen.y );
transform.rotate( -angle );
transform.translate(
-scaled.getWidth() / 2, -scaled.getHeight() / 2 );
g.drawImage( scaled, transform, null );
}

public void scaleImage( Matrix3x3f view ) {
Vector2f screenTopLeft = view.mul( topLeft );
Vector2f screenBottomRight = view.mul( bottomRight );
int scaledWidth = (int)Math.abs( screenBottomRight.x - screenTopLeft.x );
int scaledHeight =
(int)Math.abs( screenBottomRight.y - screenTopLeft.y );
scaled = Utility.scaleImage( image, scaledWidth, scaledHeight );
}
```

![](img/588a4cda8f2acae94a7e1987bf99400d_544_0.png)

**图 16.2**
精灵示例。
© 2014 提摩西·赖特。

SpriteExample 如图 16.2 所示，位于 javagames.tools 包中，是一个使用精灵类将图像绘制到世界空间矩形的快速测试。initialize() 方法加载岩石精灵并创建精灵类。updateObjects() 方法执行简单的屏幕碰撞检测。最后，render() 方法创建旋转精灵。

```java
package javagames.tools;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.InputStream;
import javagames.util.*;
import javax.imageio.ImageIO;

public class SpriteExample extends WindowFramework {
    private Sprite sprite;
    private Vector2f pos;
    private Vector2f vel;
    private float rot;
    private float rotDelta;

    public SpriteExample() {
        appTitle = "Sprite Example";
        pos = new Vector2f();
        vel = new Vector2f( 0.25f, -0.3f );
        rotDelta = (float)Math.toRadians( 90.0 );
    }

    @Override
    protected void initialize() {
        super.initialize();
        InputStream in = ResourceLoader.load( SpriteExample.class,
            "res/assets/images/large0.png",
            "images/large0.png" );
        try {
            BufferedImage image = ImageIO.read( in );
            Vector2f topLeft = new Vector2f( -0.25f, 0.25f );
            Vector2f bottomRight = new Vector2f( 0.25f, -0.25f );
            sprite = new Sprite( image, topLeft, bottomRight );
        } catch ( Exception e ) {
            e.printStackTrace();
        }
    }
}
```

```java
@Override
protected void updateObjects( float delta ) {
    super.updateObjects( delta );

    pos = pos.add( vel.mul( delta ) );
    if( pos.x < -appWorldWidth / 2.0f ) {
        pos.x = appWorldWidth / 2.0f;
        vel.x = -vel.x;
    } else if( pos.x > appWorldWidth / 2.0f ) {
        pos.x = appWorldWidth / 2.0f;
        vel.x = -vel.x;
    }

    if( pos.y < -appWorldHeight / 2.0f ) {
        pos.y = appWorldHeight / 2.0f;
        vel.y = -vel.y;
    } else if( pos.y > appWorldHeight / 2.0f ) {
        pos.y = appWorldHeight / 2.0f;
        vel.y = -vel.y;
    }

    rot += rotDelta * delta;
}

@Override
protected void render( Graphics g ) {
    super.render( g );

    g.setColor( Color.GREEN );
    g.drawRect( 0, 0, getScreenWidth() - 1, getScreenHeight() - 1 );
    sprite.render( (Graphics2D)g, getViewportTransform(), pos, rot );
}

public static void main( String[] args ) {
    launchApp( new SpriteExample() );
}
}
```

## 创建简单粒子引擎

粒子系统只是一种花哨的方式，用于跟踪爆炸中的每个粒子，包括火焰、烟雾效果、液滴或任何可以建模为微小元素集合的东西。系统中的每个粒子都维护自己的物理变量，并且每个粒子每帧都会更新。如你所想象，这些系统可能变得相当复杂。就本文而言，创建了一个非常简单的粒子系统，只是让你了解可能性。

TestParticle 类位于 javagames.tools 包中，是一个表示粒子的简单类。半径是渲染圆的大小，颜色填充圆。向量具有角度和方向，以及以秒为单位的生命周期。update() 方法更新粒子存活的时间并更新其当前位置。render() 方法将绘制缩放到屏幕的小圆（可能非常小），hasDied() 方法检查生命周期是否已过期。

```java
package javagames.tools;

import java.awt.Color;
import java.awt.Graphics2D;

import javagames.util.Matrix3x3f;
import javagames.util.Vector2f;

public class TestParticle {
	private Vector2f pos;
	private Vector2f curPos;
	private Vector2f vel;
	private Vector2f curVel;
	private Color color;
	private float lifeSpan;
	private float time;
	private float radius;

	public TestParticle() {
	}

	public void setPosition( Vector2f pos ) {
		this.pos = pos;
	}

	public void setRadius( float radius ) {
		this.radius = radius;
	}

	public void setVector( float angle, float r ) {
		vel = Vector2f.polar( angle, r );
	}

	public void setColor( Color color ) {
		this.color = color;
	}

	public void setLifeSpan( float lifeSpan ) {
		this.lifeSpan = lifeSpan;
	}
}
```

```java
public void update( float delta ) {
    time += delta;
    curVel = vel.mul( time );
    curPos = pos.add( curVel );
}

public void draw( Graphics2D g, Matrix3x3f view ) {
    g.setColor( color );
    Vector2f topLeft =
        new Vector2f( curPos.x - radius, curPos.y + radius );
    topLeft = view.mul( topLeft );
    Vector2f bottomRight =
        new Vector2f( curPos.x + radius, curPos.y - radius );
    bottomRight = view.mul( bottomRight );
    int circleX = (int)topLeft.x;
    int circleY = (int)topLeft.y;
    int circleWidth = (int)(bottomRight.x - topLeft.x);
    int circleHeight = (int)(bottomRight.y - topLeft.y);
    g.fillOval( circleX, circleY, circleWidth, circleHeight );
}

public boolean hasDied() {
    return time > lifeSpan;
}
}
```

![](img/588a4cda8f2acae94a7e1987bf99400d_548_0.png)

图 16.3
粒子示例。
© 2014 提摩西·赖特。

ParticleExample 如图 16.3 所示，位于 javagames.tools 包中，演示了创建粒子并将其渲染为爆炸。这些效果虽然简单，但通过模拟爆炸和火箭喷射，为最终游戏增色不少。

initialize() 方法为圆形爆炸创建随机颜色列表，以及粒子颜色列表。getRandomPosition() 方法为粒子事件生成随机位置。createParticleRings() 方法创建带有速度和生命周期的五个环。这些爆炸用于完整游戏中的玩家飞船。createRandomParticle() 方法向各个方向创建爆发，是用于太空岩石的爆炸。updateObjects() 方法生成随机粒子事件，绘制每个粒子，并且如果粒子已死亡，则将其从列表中移除。最后，render() 方法遍历粒子列表并绘制每个单独的粒子。

```java
package javagames.tools;

import java.awt.*;
import java.util.*;

import javagames.util.Vector2f;
import javagames.util.WindowFramework;

public class ParticleExample extends WindowFramework {
    private float elapsedRing;
    private float ringTime;
    private float elapsedBurst;
    private float burstTime;
    private Random random;
    private Vector<Color> colors;
    private Vector<TestParticle> particles;

    public ParticleExample() {
        appWidth = 640;
        appHeight = 480;
        appSleep = 1L;
        appTitle = "Particle Example";
    }

    @Override
    protected void initialize() {
        super.initialize();
        random = new Random();
        particles = new Vector<TestParticle>();
    }
```

```java
colors = new Vector<Color>();
colors.add( Color.WHITE );
colors.add( Color.RED );
colors.add( Color.YELLOW );
colors.add( Color.ORANGE );
colors.add( Color.PINK );

}

private Vector2f getRandomPosition() {
    float x = -0.5f + random.nextFloat();
    float y = -0.5f + random.nextFloat();
    return new Vector2f( x, y );
}

private void createParticleRings() {
    for( int ring = 0; ring < 5; ++ring ) {
        float velocity = 0.25f + random.nextFloat() * 1.0f;
        float lifeSpan = 1.0f + random.nextFloat() * 1.0f;
        float radius = 0.003f + random.nextFloat() * 0.003f;

        for( int i = 0; i < 100; ++i ) {
            TestParticle p = new TestParticle();
            p.setPosition( new Vector2f() );
            p.setRadius( radius );
            p.setLifeSpan( lifeSpan );
            p.setColor( colors.get( random.nextInt( colors.size() ) ) );
            float angle = (float)Math.toRadians( random.nextInt( 360 ) );
            p.setVector( angle, velocity );
            particles.add( p );
        }
    }
}

private TestParticle createRandomParticle( Vector2f pos ) {
    TestParticle p = new TestParticle();
    p.setPosition( pos );
    p.setRadius( 0.002f + random.nextFloat() * 0.004f );
    p.setLifeSpan( random.nextFloat() * 1.0f );
    switch( random.nextInt( 4 ) ) {
        case 0: p.setColor( Color.WHITE ); break;
        case 1: p.setColor( Color.GRAY ); break;
        case 2: p.setColor( Color.LIGHT_GRAY ); break;
        case 3: p.setColor( Color.DARK_GRAY ); break;
    }

    float angle = (float)Math.toRadians( random.nextInt( 360 ) );
    float velocity = random.nextFloat() * 2.0f;
```

