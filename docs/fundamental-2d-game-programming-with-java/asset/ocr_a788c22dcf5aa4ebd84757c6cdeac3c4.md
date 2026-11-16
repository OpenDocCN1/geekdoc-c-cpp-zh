![](bbox=[0.103, 0.088, 0.433, 0.203])

Figure 7.9 Circle Representation. © 2014 Timothy Wright.

You draw a circle so that it stretches with the size of the window the same way you draw the AABB.

```
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
    int circleHeight = (int)(bottomRight.y - topLeft.y);

    g.drawOval( circleX, circleY, circleWidth, circleHeight );
}
```

To check if a point is inside a circle, you compare the distance from the point in the center of the circle to the radius, as shown in Figure 7.10. If the radius is larger than the distance, the point is inside the circle.

![](bbox=[0.103, 0.74, 0.433, 0.85])

Figure 7.10 Point in Circle. © 2014 Timothy Wright.