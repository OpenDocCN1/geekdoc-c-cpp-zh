![](bbox=[0.22, 0.1, 0.78, 0.38])

**Figure 10.5** 2D rectangle classes

It is best to ignore the fact that the two concrete classes are static inner classes—that is just a gimmick to avoid names such as FloatRectangle2D and DoubleRectangle2D.

When you construct a Rectangle2D.Float object, you supply the coordinates as float numbers. For a Rectangle2D.Double object, you supply them as double numbers.

```
```java
var floatRect = new Rectangle2D.Float(10.0F, 25.0F, 22.5F, 20.0F);
var doubleRect = new Rectangle2D.Double(10.0, 25.0, 22.5, 20.0);
```
```

The construction parameters denote the top left corner, width, and height of the rectangle.

The Rectangle2D methods use double parameters and return values. For example, the getWidth method returns a double value, even if the width is stored as a float in a Rectangle2D.Float object.