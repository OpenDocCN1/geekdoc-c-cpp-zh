```
if (size == Size.Large ) {
    large.add( asteroid );
} else if ( size == Size.Medium ) {
    medium.add( asteroid );
} else if ( size == Size.Small ) {
    small.add( asteroid );
} }

public Asteroid getLargeAsteroid() {
    return getLargeAsteroid( getAsteroidStartPosition() );
}

public Asteroid getLargeAsteroid( Vector2f position ) {
    return copy( getRandomAsteroid( large ), position );
}

public Asteroid getMediumAsteroid() {
    return getMediumAsteroid( getAsteroidStartPosition() );
}

public Asteroid getMediumAsteroid( Vector2f position ) {
    return copy( getRandomAsteroid( medium ), position );
}

public Asteroid getSmallAsteroid() {
    return getSmallAsteroid( getAsteroidStartPosition() );
}

public Asteroid getSmallAsteroid( Vector2f position ) {
    return copy( getRandomAsteroid( small ), position );
}

public Asteroid copy( Asteroid template, Vector2f position ) {
    Asteroid asteroid = new Asteroid( wrapper );
    asteroid.setPosition( position );
    asteroid.setSprite( template.getSprite() );
    asteroid.setSize( template.getSize() );
    asteroid.setPolygon( template.getPolygon() );
    return asteroid;
}

private Vector2f getAsteroidStartPosition() {
    float angle = (float)Math.toRadians( rand.nextInt( 360 ) );
    float minimum = worldWidth / 4.0f;
    float extra = rand.nextFloat() * minimum;
    float radius = minimum + extra;
    return Vector2f.polar( angle, radius );
}
```