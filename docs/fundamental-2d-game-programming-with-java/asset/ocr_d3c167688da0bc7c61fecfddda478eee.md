```
if (shouldChangeState()) {
    AttractState state = getState();
    state.setAsteroids( asteroids );
    getController().setState( state );
    return;
}

for ( Asteroid a : asteroids ) {
    a.update( delta );
}

protected boolean shouldChangeState() {
    return time > getWaitTime();
}

protected float getWaitTime() {
    return 5.0f;
}

private void setAsteroids( List<Asteroid> asteroids ) {
    this.asteroids = asteroids;
}

protected abstract AttractState getState();
public List<Asteroid> getAsteroids() {
    return asteroids;
}

@Override
public void processInput( float delta ) {
    if ( keys.keyDownOnce( KeyEvent.VK_ESCAPE ) ) {
        app.shutDownGame();
    }

    if ( keys.keyDownOnce( KeyEvent.VK_SPACE ) ) {
        GameState state = new GameState();
        state.setLevel( 1 );
        state.setLives( 2 );
        getController().setState( new LevelStarting( state ) );
    }
}

@Override
public void render( Graphics2D g, Matrix3x3f view ) {
    background.render( g, view );
    for ( Asteroid a : asteroids ) {
        a.draw( g, view );
    }
}
}
```