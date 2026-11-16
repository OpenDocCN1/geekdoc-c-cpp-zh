```
```java
public void rotateLeft( float delta ) {
    angle += rotationDelta * delta;
}
```
```

```
```java
public void rotateRight( float delta ) {
    angle -= rotationDelta * delta;
}
```
```

```
```java
public void reset() {
    setAlive( true );
    setPosition( new Vector2f() );
    setAngle( 0.0f );
    positionList.clear();
    collisionList.clear();
    velocity = new Vector2f();
    particles.clear();
}
```
```

```
```java
public void setThrusting( boolean thrusting ) {
    if ( isAlive() ) {
        curAcc = thrusting ? acceleration : 0.0f;
        if ( thrusting ) {
            while ( particles.size() < MAX_PARTICLES ) {
                particles.add( createRandomParticle() );
            }
        }
    }
}
```
```

```
```java
public void setAngle( float angle ) {
    this.angle = angle;
}
```
```

```
```java
public Bullet launchBullet() {
    Vector2f bulletPos = position.add( Vector2f.polar( angle, 0.0325f ) );
    return new Bullet( bulletPos, angle );
}
```
```

```
```java
public void update( float delta ) {
    if ( isAlive() ) {
        updatePosition( delta );
        updateInvincible( delta );
        updateParticles( delta );
        collisionList.clear();
        Vector2f[] world = transformPolygon();
        collisionList.add( world );
        wrapper.wrapPolygon( world, collisionList );
    }
}
```
```