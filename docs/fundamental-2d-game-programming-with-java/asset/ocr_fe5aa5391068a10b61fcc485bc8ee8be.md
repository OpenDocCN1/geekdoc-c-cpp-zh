```
public PrototypeAsteroid createLargeAsteroid( Vector2f position ) {
PrototypeAsteroid asteroid = new PrototypeAsteroid( wrapper );
asteroid.setPosition( position );
asteroid.setPolygon( getRandomAsteroid( LARGE ) );
asteroid.setSize( Size.Large );
return asteroid;
}
```

```
public PrototypeAsteroid createMediumAsteroid( Vector2f position ) {
PrototypeAsteroid asteroid = new PrototypeAsteroid( wrapper );
asteroid.setPosition( position );
asteroid.setPolygon( getRandomAsteroid( MEDIUM ) );
asteroid.setSize( Size.Medium );
return asteroid;
}
```

```
public PrototypeAsteroid createSmallAsteroid( Vector2f position ) {
PrototypeAsteroid asteroid = new PrototypeAsteroid( wrapper );
asteroid.setPosition( position );
asteroid.setPolygon( getRandomAsteroid( SMALL ) );
asteroid.setSize( Size.Small );
return asteroid;
}
```

```
private Vector2f[] getRandomAsteroid( Vector2f[][] asteroids ) {
return mirror( asteroids[ rand.nextInt( asteroids.length ) ] );
}
```

```
private Vector2f[] mirror( Vector2f[] polygon ) {
Vector2f[] mirror = new Vector2f[ polygon.length ];
float x = rand.nextBoolean() ? 1.0f : -1.0f;
float y = rand.nextBoolean() ? 1.0f : -1.0f;
Matrix3x3f mat = Matrix3x3f.scale( x, y );
for( int i = 0; i < polygon.length; ++i ) {
mirror[i] = mat.mul( polygon[i] );
}
return mirror;
}
}
```

The RandomAsteroidExample, shown in Figure 8.10 and located in the javagames.prototype package, uses PolygonWrapper, PrototypeAsteroid, and PrototypeAsteroid Factory to generate random rocks flying around the screen.