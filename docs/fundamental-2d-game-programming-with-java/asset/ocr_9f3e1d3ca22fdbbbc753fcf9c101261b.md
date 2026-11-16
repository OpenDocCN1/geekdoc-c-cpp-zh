```
```java
private float[] lineCircleIntersection(
    Vector2f O, Vector2f d, Vector2f C, float r ) {
    Vector2f V = O.sub( C );
    float b = d.dot( V );
    float bb = b*b;
    float rr = r*r;
    float Vv = V.dot( V );
    float c = Vv - rr;
    if ( bb < c ) {
        return null;
    }
    float root = (float)Math.sqrt( bb - c );
    return new float[]{ -b - root, -b + root };
}
```
```

```
```java
@Override
protected void render( Graphics g ) {
    super.render( g );
    g.drawString( "T0: " + t0, 20, 35 );
    g.drawString( "T1: " + t1, 20, 50 );
    drawLine( g, p0, p1 );
    drawOval( g, center, radius );
    drawIntersections( g, plane0, segment0 );
    drawIntersections( g, plane1, segment1 );
}
```
```

```
```java
private void drawLine( Graphics g, Vector2f p0, Vector2f p1 ) {
    Matrix3x3f view = getViewportTransform();
    Vector2f p0Cpy = view.mul( p0 );
    Vector2f p1Cpy = view.mul( p1 );
    g.drawLine( (int)p0Cpy.x, (int)p0Cpy.y, (int)p1Cpy.x, (int)p1Cpy.y );
}
```
```

```
```java
private void drawOval( Graphics g, Vector2f center, float radius ) {
    Matrix3x3f view = getViewportTransform();
    Vector2f topLeft =
        new Vector2f( center.x - radius, center.y + radius );
    topLeft = view.mul( topLeft );
    Vector2f bottomRight =
        new Vector2f( center.x + radius, center.y - radius );
    bottomRight = view.mul( bottomRight );
    int circleX = (int)topLeft.x;
    int circleY = (int)topLeft.y;
    int circleWidth = (int)(bottomRight.x - topLeft.x);
```
```