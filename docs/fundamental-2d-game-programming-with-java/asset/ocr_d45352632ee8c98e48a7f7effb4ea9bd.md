```
public void setDamaged( boolean damaged ) {
    this.damaged = damaged;
}
```

```
public boolean isDamaged() {
    return damaged;
}
```

```
public void rotateLeft( float delta ) {
    angle += rotationDelta * delta;
}
```

```
public void rotateRight( float delta ) {
    angle -= rotationDelta * delta;
}
```

```
public void setThrusting( boolean thrusting ) {
    curAcc = thrusting ? acceleration : 0.0f;
}
```

```
public void setAngle( float angle ) {
    this.angle = angle;
}
```

```
public PrototypeBullet launchBullet() {
    Vector2f bulletPos = position.add( Vector2f.polar( angle, 0.0325f ) );
    return new PrototypeBullet( bulletPos, angle );
}
```

```
public void update( float time ) {
    updatePosition( time );
    rendererList.clear();
    Vector2f[] world = transformPolygon();
    rendererList.add( world );
    wrapper.wrapPolygon( world, renderList );
}
```

```
private Vector2f[] transformPolygon() {
    Matrix3x3f mat = Matrix3x3f.rotate( angle );
    mat = mat.mul( Matrix3x3f.translate( position ) );
    return transform( polyman, mat );
}
```

```
private void updatePosition( float time ) {
    Vector2f accel = Vector2f.polar( angle, curAcc );
    velocity = velocity.add( accel.mul( time ) );
    float maxSpeed = Math.min( maxVelocity / velocity.len(), 1.0f );
    velocity = velocity.mul( maxSpeed );
}
```