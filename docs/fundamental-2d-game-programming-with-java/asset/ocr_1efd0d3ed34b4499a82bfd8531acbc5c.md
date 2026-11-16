```
@Override
protected void initialize() {
super.initialize();
polygon = new ArrayList<Vector2f>();
}

@Override
protected void processInput( float delta ) {
super.processInput( delta );
mousePos = getWorldMousePosition();
if (mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
polygon.add( mousePos );
}
if (mouse.buttonDownOnce( MouseEvent.BUTTON2 ) ) {
closed = !closed;
}
if (mouse.buttonDownOnce( MouseEvent.BUTTON3 ) ) {
if ( !polygon.isEmpty() ) {
polygon.remove( polygon.size() - 1 );
}
}
}

@Override
protected void render( Graphics g ) {
super.render( g );
((Graphics2D)g).setRenderingHint( RenderingHints.KEY_ANTIALIASING,
RenderingHints.VALUE_ANTIALIAS_ON );
((Graphics2D)g).setRenderingHint( RenderingHints.KEY_INTERPOLATION,
RenderingHints.VALUE_INTERPOLATION_BILINEAR
textPos = Utility.drawString( g, 20, textPos, "Left Mouse: Add point",
"Right Mouse: Remove point", "Center Mouse: Toggle Close" );
drawSprite( g );
drawAxesLines( g );
drawPolygon( g, getViewportTransform() );
drawBoundingBox( g );
}

private void drawSprite( Graphics g ) {
if ( sprite == null ) {
return;
}
Vector2f topLeft = new Vector2f( -bounds / 2.0f, bounds / 2.0f );
Vector2f bottomRight = new Vector2f( bounds / 2.0f, -bounds / 2.0f );
```