```
Polygon ()
    Constructor: Creates an empty polygon.

Polygon (int[] xpoints, int[] ypoints, int npoints)
    Constructor: Creates a polygon using the (x, y) coordinate pairs
    in corresponding entries of xpoints and ypoints.

void addPoint (int x, int y)
    Appends the specified point to this polygon.

boolean contains (int x, int y)
    Returns true if the specified point is contained in this polygon.

boolean contains (Point p)
    Returns true if the specified point is contained in this polygon.

Rectangle getBounds ()
    Gets the bounding rectangle for this polygon.

void translate (int deltaX, int deltaY)
    Translates the vertices of this polygon by deltaX along the x axis
    and deltaY along the y axis.
```

# FIGURE 8.6 Some methods of the Polygon class

A Polygon object encapsulates the coordinates of the polygon sides. The constructors of the Polygon class allow the creation of an initially empty polygon or one defined by arrays of integers representing the point coordinates. The Polygon class contains methods to add points to the polygon and to determine whether a given point is contained within the polygon shape. It also contains methods to get a representation of a bounding rectangle for the polygon, as well as a method to translate all of the points in the polygon to another position. Figure 8.6 lists these methods.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 8.25 What is a polyline? How do we specify its shape?
+   SR 8.26 What is the difference between a polygon and a polyline?
+   SR 8.27 What is the result of separately making each of the following changes to the RocketPanel class? You may make the change, compile and run