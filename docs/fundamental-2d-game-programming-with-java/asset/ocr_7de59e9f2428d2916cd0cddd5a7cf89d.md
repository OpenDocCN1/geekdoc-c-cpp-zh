```
GradientPaint gp =
new GradientPaint( x1, y1, Color.BLACK, x2, y2, Color.WHITE );
g2d.setPaint( gp );
g2d.fillOval(
sprite.getWidth() / 4, sprite.getHeight() / 4,
sprite.getWidth() / 2, sprite.getHeight() / 2
);
g2d.setFont( new Font( "Arial", Font.BOLD, 42 ) );
g2d.setRenderingHint(
RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON
);
g2d.setColor( Color.LIGHT_GRAY );
g2d.drawString(
"Pg.1", sprite.getWidth()/2-40, sprite.getHeight()/2-20 );
g2d.setColor( Color.DARK_GRAY );
g2d.drawString(
"Pg.2", sprite.getWidth()/2-40, sprite.getHeight()/2+40 );
g2d.dispose();
}
@Override
protected void processInput( float delta ) {
super.processInput( delta );
}
@Override
protected void updateObjects( float delta ) {
super.updateObjects( delta );
}
@Override
protected void render( Graphics g ) {
super.render( g );
// Test Image
g.drawImage(
sprite, (canvas.getWidth() - sprite.getWidth())/2, 50, null );
int sw = averaged.getWidth( null );
int sh = averaged.getHeight( null );
int pos = canvas.getHeight() - sh - 50;
int textPos = pos + sh;
// Averaged Image
int imgPos = (sw + 50) * 0 + 50;
g.drawImage( averaged, imgPos, pos, null );
```