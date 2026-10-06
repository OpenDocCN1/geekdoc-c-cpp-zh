How many subclasses can a class have, and how many superclasses can it have?

+   4. Write a Rectangle method called translate: that takes an XYPoint object as its argument. Have it translate the rectangle's origin by the specified vector. Note: Translation simply means moving the point from one place to another.

+   5. Define a new class called GraphicObject, and make it a subclass of NSObject. Define instance variables in your new class as follows:

```
int    fillColor;   // 32-bit color
BOOL   filled;      // Is the object filled?
int    lineColor;   // 32-bit line color
```

Write methods to set and retrieve the variables defined previously.

Make the Rectangle class a subclass of GraphicObject.

Define new classes, Circle and Triangle, which are also subclasses of GraphicObject. Write methods to set and retrieve the various parameters for these objects and also to calculate the circle's circumference and area, and the triangle's perimeter and area.

+   6. Write a Rectangle method called containsPoint: that takes an XYPoint object as its argument:

- (BOOL) containsPoint: (XYPoint *) aPoint;

Have the method return the BOOL value YES if the rectangle encloses the specified point and NO if it does.

+   7. Write a Rectangle method called intersect: that takes a rectangle as an argument and returns a rectangle representing the overlapping area between the two rectangles. For example, given the two rectangles shown in Figure 8.10,