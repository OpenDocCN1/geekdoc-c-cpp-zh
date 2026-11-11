```
```java
public ShapeMaker(int pointCount)
{
    this.pointCount = pointCount;
}

/**
 * Gets the number of points needed to define this shape.
 * @return the point count
 */
public int getPointCount()
{
    return pointCount;
}

/**
 * Makes a shape out of the given point set.
 * @param p the points that define the shape
 * @return the shape defined by the points
 */
public abstract Shape makeShape(Point2D[] p);

public String toString()
{
    return getClass().getName();
}
}

/**
 * Makes a line that joins two given points.
 */
class LineMaker extends ShapeMaker
{
    public LineMaker()
    {
        super(2);
    }

    public Shape makeShape(Point2D[] p)
    {
        return new Line2D.Double(p[0], p[1]);
    }
}

/**
 * Makes a rectangle that joins two given corner points.
 */
class RectangleMaker extends ShapeMaker
{
```
```