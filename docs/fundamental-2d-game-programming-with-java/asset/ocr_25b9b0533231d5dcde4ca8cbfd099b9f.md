```
float velocity = random.nextFloat() * 0.375f;
Vector2f bulletPos =
    position.add( Vector2f.polar( angle, -0.0325f ) );
p.setPosition( bulletPos );
p.setVector( angle + (float)Math.PI + a, velocity );
return p;
}
```

```
private void updateParticles( float delta ) {
    Iterator<Particle> part = particles.iterator();
    while( part.hasNext() ) {
        Particle p = part.next();
        Vector2f bulletPos =
            position.add( Vector2f.polar( angle, -0.0325f ) );
        p.setPosition( bulletPos );
        p.update( delta );
        if( p.hasDied() ) {
            part.remove();
        }
    }
}
```

# THE SHIPFACTORY CLASS

The ShipFactory class parses the ship model file:

```
<model bounds="0.075" sprite="Ship.png" glow="ShipGlow.png">
    <coord x="-0.0325" y="-0.0" />
    <coord x="-0.0325" y="0.0325" />
    <coord x="0.0" y="0.0" />
    <coord x="-0.0325" y="-0.0325" />
</model>
```

There are two sprites, a regular one and a green glow sprite for invincible mode. There is also a convenience method for creating new Ship objects.

```
package javagames.completegame.object;

import java.awt.Image.BufferedImage;
import java.io.InputStream;
import java.util.Vector;
import javax.imageio.ImageIO;
```