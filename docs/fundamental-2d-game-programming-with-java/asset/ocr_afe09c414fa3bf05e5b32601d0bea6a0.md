```
if (wait > 1.0f && threadPool.isShutdown()) {
    LoopEvent loop = (LoopEvent)controller.getAttribute( "ambience" );
    loop.fire();
    getController().setState( new PressSpaceToPlay() );
}
```

```
@Override
public void render( Graphics2D g, Matrix3x3f view ) {
    super.render( g, view );
    g.setRenderingHint( RenderingHints.KEY_TEXT_ANTIALIASING,
            RenderingHints.VALUE_TEXT_ANTIALIAS_ON );
    g.setFont( new Font( "Arial", Font.PLAIN, 20 ) );
    g.setColor( Color.GREEN );
    String message = "SPACE ROCKS";
    Utility.drawCenteredString( g, app.getScreenWidth(),
            app.getScreenHeight() / 3, message );
    int vw = (int)( app.getScreenWidth() * .9f );
    int vh = (int)( app.getScreenWidth() * .05f );
    int vx = ( app.getScreenWidth() - vw ) / 2;
    int vy = ( app.getScreenHeight() - vh ) / 2;
    // fill in progress
    g.setColor( Color.GRAY );
    int width = (int)( vw * percent );
    g.fillRect( vx, vy, width, vh );
    // draw border
    g.setStroke( Color.GREEN );
    g.drawRect( vx, vy, vw, vh );
}
```

# THE ATTRACTSTATE CLASS

The AttractState class is any state that the game is in while waiting for the user to start a new game or exit the application. The enter() method pulls all the necessary objects from the StateController and creates some random rocks to fly around. There is an abstract method, getState(), that subclasses supply, returning the transition game state. The getWaitTime() returns the number of seconds to stay in the current state before transitioning.

The processInput() overrides the timed transition, exiting the game on an Esc key, or starting the game on a spacebar event. The render() method draws the stars, planet background, and floating rocks.