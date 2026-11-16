```
```java
private boolean intersectCircleAABB(
Vector2f c, float r, Vector2f min, Vector2f max ) {
float d = 0.0f;
if ( c.x < min.x ) d += ( c.x - min.x )*( c.x - min.x );
if ( c.x > max.x ) d += ( c.x - max.x )*( c.x - max.x );
if ( c.y < min.y ) d += ( c.y - min.y )*( c.y - min.y );
if ( c.y > max.y ) d += ( c.y - max.y )*( c.y - max.y );
return d < r*r;
}

@Override
protected void render( Graphics g ) {
super.render( g );
// render instructions
g.drawString( "Dragging: * + dragging, 20, 35 );
g.drawString( "Click and hold to drag shapes", 20, 50 );
g.drawString( "Press [SPACE] to reset", 20, 65 );
// render objects
g.setColor( rectCollision ? Color.BLACK : Color.BLUE );
drawAABB( g, min0Cpy, max0Cpy );
g.setColor( rect1Collision ? Color.BLACK : Color.BLUE );
drawAABB( g, min1Cpy, max1Cpy );
g.setColor( circle0Collision ? Color.BLACK : Color.BLUE );
drawOval( g, c0, r0 );
g.setColor( circle1Collision ? Color.BLACK : Color.BLUE );
drawOval( g, c1, r1 );
}

// draw the AABB
private void drawAABB( Graphics g, Vector2f min, Vector2f max ) {
Matrix3x3f view = getViewportTransform();
Vector2f topLeft = new Vector2f( min.x, max.y );
topLeft = view.mul( topLeft );
Vector2f bottomRight = new Vector2f( max.x, min.y );
bottomRight = view.mul( bottomRight );
int rectX = (int)topLeft.x;
int rectY = (int)topLeft.y;
int rectWidth = (int)( bottomRight.x - topLeft.x );
int rectHeight = (int)( bottomRight.y - topLeft.y );
g.drawRect( rectX, rectY, rectWidth, rectHeight );
}
```
```