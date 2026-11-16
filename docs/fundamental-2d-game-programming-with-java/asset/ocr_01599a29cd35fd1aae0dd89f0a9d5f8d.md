```
remove( asteroid );
bullets.remove( bullet );
explosions.add(
    new AsteroidExplosion( bullet.getPosition() )
);
explosion[ rand.nextInt( explosion.length ) ].fire();
} }
}
```

```
private void remove( Asteroid asteroid ) {
    asteroids.remove( asteroid );
    state.updateScore( asteroid.getSize() );
    spawnBabies( asteroid );
}
```

```
private void spawnBabies( Asteroid asteroid ) {
    if ( asteroid.getSize() == Size.Large ) {
        asteroids.add(
            factory.getMediumAsteroid( asteroid.getPosition() )
        );
        asteroids.add(
            factory.getMediumAsteroid( asteroid.getPosition() )
        );
    }
    if ( asteroid.getSize() == Size.Medium ) {
        asteroids.add( factory.getSmallAsteroid( asteroid.getPosition() ) );
        asteroids.add( factory.getSmallAsteroid( asteroid.getPosition() ) );
    }
}
```

```
private boolean shouldRespawn() {
    return !ship.isAlive() && shipExplosion == null;
}
```

```
private void processRespawnShip( double delta ) {
    respawn += delta;
    if ( respawn > 1.0 ) {
        if ( state.getLives() > 0 ) {
            respawn = 0.0;
            state.setLives( state.getLives() - 1 );
            createShip( true );
        } else {
```