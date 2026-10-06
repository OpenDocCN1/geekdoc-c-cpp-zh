method takes, what their types are, and what the method's return
type is.

So sure you understand the use of the @class directive.
It is simply telling the compiler that XYPoint is the name of a class.
In that way, when it sees this line:

```
XYPoint *origin;
```

it knows that origin is an object from a class called XYPoint.
That's all the compiler needs to know at that point.

Let's fill in the blanks for your new XYPoint class and Rectangle
methods so you can test everything in a program. First, Program 8.4
shows the implementation file for your XYPoint class.

First, Program 8.4 shows the new methods for the Rectangle
class.

# Program 8.4. Rectangle.m Added Methods

```
#import "XYPoint.h"

-(void) setOrigin: (XYPoint *) pt
{
  origin = pt;
}

-(XYPoint *) origin
{
  return origin;
}
@end
```