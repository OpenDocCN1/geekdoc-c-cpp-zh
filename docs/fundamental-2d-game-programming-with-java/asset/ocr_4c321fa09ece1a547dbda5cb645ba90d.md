and the sprite position. The Ship also adds particles for the rocket blasts when the ship is flying.

```
package javagames.completegame.object;
import java.awt.*;
import java.util.*;
import javagames.util.*;

public class Ship {
	private static final int MAX_PARTICLES = 300;
	private float angle;
	private float acceleration;
	private float friction;
	private float maxVelocity;
	private float maxVelocityDelta;
	private float curAcc;
	private Vector2f position;
	private Vector2f velocity;
	private ArrayList<Particle> particles;
	private Random random;
	private PolygonWrapper wrapper;
	private boolean alive;
	private boolean invincible;
	private float invincibleDelta;
	private Sprite ship;
	private Sprite glow;
	private Vector2f[] polygon;
	private ArrayList<Vector2f[]> collisionList;
	private ArrayList<Vector2f> positionList;
	public Ship( PolygonWrapper wrapper ) {
		this.wrapper = wrapper;
		friction = 0.25f;
		rotationDelta = (float)Math.toRadians( 180.0 );
		acceleration = 1.0f;
		maxVelocity = 0.5f;
		velocity = new Vector2f();
		position = new Vector2f();
		particles = new ArrayList<Particle>();
	}
```