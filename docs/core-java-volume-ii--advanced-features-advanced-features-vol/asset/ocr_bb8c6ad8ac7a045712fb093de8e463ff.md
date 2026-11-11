![](bbox=[0.317, 0.159, 0.77, 0.284])

**Figure 11.32** The bounding rectangle of an ellipse and an arc

Internally, all graphics classes use float coordinates because float numbers use less storage space but have sufficient precision for geometric computations. However, the Java programming language makes it a bit more tedious to manipulate float numbers. For that reason, most methods of the graphics classes use double parameters and return double values. Only when constructing a 2D object you need to choose between the constructors with float and double coordinates. For example,

```
var floatRect = new Rectangle2D.Float(5F, 10F, 7.5F, 15F);
var doubleRect = new Rectangle2D.Double(5, 10, 7.5, 15);
```

The Xxx2D.Float and Xxx2D.Double classes are subclasses of the Xxx2D classes. After object construction, essentially no benefit accrues from remembering the subclass, and you can just store the constructed object in a superclass variable as in the code example above.

As you can see from the curious names, the Xxx2D.Float and Xxx2D.Double classes are also inner classes of the Xxx2D classes. That is just a minor syntactical convenience to avoid inflation of outer class names.

Finally, the Point2D class describes a point with an x and a y coordinate. Points are used to define shapes, but they aren’t themselves shapes.

Figure 11.33 shows the relationships between the shape classes. However, the Double and Float subclasses are omitted. Legacy classes from the pre-2D library are marked with a gray fill.

# 11.3.2.2 Using the Shape Classes

You already saw how to use the Rectangle2D, Ellipse2D, and Line2D classes in Volume I, Chapter 10. In this section, you will learn how to work with the remaining 2D shapes.