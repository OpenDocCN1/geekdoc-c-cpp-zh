![](bbox=[0.35, 0.11, 0.63, 0.25])

Fig. 15.25 | Creating JFrame to display arcs. (Part 2 of 2.)

# 15.7 Drawing Polygons and Polylines

Polygons are closed multisided shapes composed of straight-line segments. Polylines are sequences of connected points. Figure 15.26 discusses methods for drawing polygons and polylines. Some methods require a Polygon object (package java.awt). Class Polygon’s constructors are also described in Fig. 15.26. The application of Figs. 15.27–15.28 draws polygons and polylines.

| Method | Description |
|---|---|
| Graphics methods for drawing polygons | |
| public void drawPolygon( int[] xPoints, int[] yPoints, int points ) | Draws a polygon. The x-coordinate of each point is specified in the xPoints array and the y-coordinate of each point in the yPoints array. The last argument specifies the number of points. This method draws a closed polygon. If the last point is different from the first, the polygon is closed by a line that connects the last point to the first. |
| public void drawPolyline( int[] xPoints, int[] yPoints, int points ) | Draws a sequence of connected lines. The x-coordinate of each point is specified in the xPoints array and the y-coordinate of each point in the yPoints array. The last argument specifies the number of points. If the last point is different from the first, the polyline is not closed. |
| public void drawPolygon( Polygon p ) | Draws the specified polygon. |
| public void fillPolygon( int[] xPoints, int[] yPoints, int points ) | Draws a filled polygon. The x-coordinate of each point is specified in the xPoints array and the y-coordinate of each point in the yPoints array. The last argument specifies the number of points. This method draws a closed polygon. If the last point is different from the first, the polygon is closed by a line that connects the last point to the first. |
| public void fillPolygon( Polygon p ) | Draws the specified filled polygon. The polygon is closed. |

Fig. 15.26 | Graphics methods for polygons and class Polygon methods. (Part 1 of 2.)