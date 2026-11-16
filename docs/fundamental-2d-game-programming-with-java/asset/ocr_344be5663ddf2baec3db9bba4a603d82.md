```
Matrix3x3f view = getViewportTransform();
topLeft = view.mul( topLeft );
bottomRight = view.mul( bottomRight );

int width = (int)Math.abs( topLeft.x - bottomRight.x );
int height = (int)Math.abs( topLeft.y - bottomRight.y );

if( scaled == null || scaled.getWidth() != width
|| scaled.getHeight() != height )
scaled = Utility.scaleImage( sprite, width, height );

g.drawImage( scaled, (int)topLeft.x, (int)topLeft.y, null );
}
```

```
private void drawAxisLines( Graphics g ) {
g.setColor( Color.WHITE );
Vector2f left = new Vector2f( appWorldWidth / 2.0f, 0.0f );
Vector2f right = new Vector2f( -left.x, 0.0f );
drawLine( g, getViewportTransform(), left, right );

Vector2f top = new Vector2f( 0.0f, appWorldHeight / 2.0f );
Vector2f bottom = new Vector2f( 0.0f, -top.y );
drawLine( g, getViewportTransform(), top, bottom );
}
```

```
private void drawPolygon( Graphics g, Matrix3x3f view ) {
g.setColor( Color.GREEN );

if( polygon.size() == 1 ) {
drawPoint( g, view, polygon.get( 0 ) );
}

for( int i = 0; i < polygon.size() - 1; ++i ) {
drawLine( g, view, polygon.get( i ), polygon.get( i + 1 ) );
}

if( closed && polygon.size() > 1 ) {
Vector2f P = polygon.get( polygon.size() - 1 );
Vector2f S = polygon.get( 0 );
drawLine( g, view, S, P );
}

if( ! polygon.isEmpty() || closed ) {
Vector2f P = polygon.get( polygon.size() - 1 );
Vector2f S = mousePos;
drawLine( g, view, S, P );
}
}
```