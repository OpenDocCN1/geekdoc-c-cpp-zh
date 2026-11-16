```
appBorderScale = GameConstants.BORDER_SCALE;
appDisableCursor = GameConstants.DISABLE_CURSOR;
appMaintainRatio = GameConstants.MAINTAIN_RATIO;
}

@Override
protected void initialize() {
    super.initialize();

    controller = new StateController();
    controller.setAttribute( "app", this );
    controller.setAttribute( "keys", keyboard );
    controller.setAttribute( "ACME", new Acme( this ) );
    controller.setAttribute( "wrapper", new PolygonWrapper( appWorldWidth,
        appWorldHeight ) );
    controller.setAttribute( "viewport", getViewportTransform() );

    controller.setState( new GameLoading() );
}

public void shutDownGame() {
    shutDown();
}

@Override
protected void processInput( float delta ) {
    super.processInput( delta );
    controller.processInput( delta );
}

@Override
protected void updateObjects( float delta ) {
    controller.updateObjects( delta );
}

@Override
protected void render( Graphics g ) {
    controller.render( Graphics2D)g, getViewportTransform() );
    super.render( g );
}

@Override
protected void terminate() {
    super.terminate();
}
```