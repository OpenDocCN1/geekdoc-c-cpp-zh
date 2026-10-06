Rectangle.h header file and replace that directive with an import instead, like so:

```
#import "XYPoint.h"
```

# Program 8.5B. Output

```
Origin at (100, 200)
Origin at (100, 200)
```

That's better. This time, changing the value of myPoint to (50, 50) inside main had no effect on the rectangle's origin because a copy of the point was created inside the Rectangle's setOrigin: method.

Incidentally, we didn't synthesize the origin methods here because the synthesized setter setOrigin: method would have behaved just like the one you originally wrote. That is, by default, the action of a synthesized setter is to copy the object pointer, not the object itself.

You can synthesize a different type of setter method that instead makes a copy of the object. However, to do that, you need to learn how to write a special copying method. We revisit this topic in Chapter 17, "Memory Management and Automatic Reference Counting."

Before leaving this section, let's think about the getter side of the Rectangle class. Suppose in your test program from Program 8.4 you inserted the following lines after you had your Rectangle's values:

```
XYPoint *theOrigin = myRect.origin;
theOrigin.x = 200;
theOrigin.y = 300;
```