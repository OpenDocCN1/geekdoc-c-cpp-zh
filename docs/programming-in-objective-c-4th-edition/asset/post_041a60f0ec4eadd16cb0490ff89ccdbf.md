
```objc
[b initVar];    // use overriding ClassB
method
  [b printVar];    // reveal value of x;
  }
  return 0;
}
```

You'll get this warning message when you build this program:

warning: 'ClassA' may not respond to '-printVar'

What happened here? We talked about this in an earlier section.
Take a look at the declaration for ClassA:

```objc
// ClassA declaration and definition

@interface ClassA: NSObject
{
  int x;
}
```

```objc
-(void) initVar;
@end
```

Note that no printVar method is declared. That method is declared and defined in ClassB. Therefore, even though ClassB objects and their descendants can use this method through inheritance, ClassA objects cannot because the method is defined farther down in the hierarchy.

# Note

You can coerce the use of this method in some ways, but we don't go into that here—besides, it's not good programming practice.

Returning to our example, let's add a printVar method to ClassA so you can display the value of its instance variable:

```objc
// ClassA declaration and definition

@interface ClassA: NSObject
{
    int x; // Will be inherited by subclasses
}

-(void) initVar;
-(void) printVar;
@end

@implementation ClassA
-(void) initVar {
    x = 100;
}

-(void) printVar {
    NSLog("@x = %i", x);
}
@end
```

ClassB's declaration and definition remain unchanged. Let's try compiling and running this program again.

# Program 8.7. Output

```objc
x = 100
x = 200
```

Now we can talk about the actual example. First, a and b are defined to be ClassA and ClassB objects, respectively. After allocation and initialization, a message is sent to asking it to apply the initVar method. This method is defined in the definition of ClassA, so this method is selected. The method simply sets the value of the instance variable x to 100 and returns. The printVar method, which you just added to ClassA, is invoked next to display the value of x.

As with the ClassA object, the ClassB object b is allocated and initialized, its instance variable x is set to 200, and finally its value displayed.

Be sure that you understand how the proper method is chosen for a and b based on which class they belong to. This is a fundamental concept of object-oriented programming in Objective-C.

As an exercise, consider removing the printVar method from ClassB. Would this work? Why or why not?

When defining a subclass, not only can you add new methods to effectively extend the definition of a class, but you can also add new instance variables. In both cases, the effect is cumulative. You can never subtract methods or instance variables through inheritance; you can only add—or, in the case of methods, add or override.

So, in review, why would you want to create a subclass? Here are three reasons:

- 1. You want to extend the functionality of a class, perhaps by adding new methods and/or instance variables.
- 2. You want to make a specialized version of a class (e.g., a particular type of graphic object).
- 3. You need to change the default behavior of a class by overriding one or more of its methods.

# Abstract Classes

What better way to conclude this chapter than with a bit of terminology? We introduce it here because it's directly related to the notion of inheritance.

Sometimes classes are created just to make it easier for someone to create a subclass. For that reason, these classes are called abstract classes or, equivalently, abstract superclasses. Methods and instance variables are defined in the class, but no one is expected to actually create an instance from that class. For example, consider the root object NSObject. Can you think of any use for defining an object from that class?

The Foundation framework, covered in Part II, "The Foundation Framework," has several of its so-called abstract classes. As an example, the Foundation's NSNumber class is an abstract class that was created for working with numbers as objects. Integers and floating-point numbers typically have different storage requirements. Separate subclasses of NSNumber exist for each numeric type. Because these subclasses, unlike their abstract superclasses, actually exist, they are known as concrete subclasses. Each concrete subclass falls under the NSNumber class and is collectively referred as a cluster. When you send a message to the NSNumber class to create a new integer object, the appropriate subclass is used to allocate the necessary storage for an integer object and to set its value appropriately. These subclasses are actually private. You don't access them directly yourself; they are accessed indirectly through the abstract superclass. The abstract superclass gives a common interface for working with all types of number objects and relieves you of the burden of having to know which type of number you have stored in your number object and how to set and retrieve its value.

Admittedly, this discussion might seem a little “abstract” (sorry!); don't worry—just a basic grasp of the concept is sufficient here.

# Exercises

- 1. Add a new class called ClassC, which is a subclass of ClassB, to Program 8.1. Make an initVar method that sets the value of its instance variable x to 300. Write a test routine that declares ClassA, ClassB, and ClassC objects and invokes their corresponding initVar methods.
- 2. When dealing with higher-resolution devices, you might need to use a coordinate system that enables you to specify points as floating-point values instead of simple integers (iOS uses a structure called CGRect for working with rectangles. All coordinates and sizes are expressed as floating point numbers when working with such rectangles). Modify the XYPoint and Rectangle classes from this chapter to deal with floating-point numbers. The rectangle’s width, area, and perimeter should all work with floating-point numbers as well.
- 3. Program 8.1 to add a new class called ClassB2 that, like ClassB, is a subclass of ClassA. What can you say about the relationship between ClassB and ClassB2?

Identify the hierarchical relationship between the NSObject class, ClassA, ClassB, and ClassB2.

What is the superclass of ClassB?

What is the superclass of ClassB2?

How many subclasses can a class have, and how many superclasses can it have?
- 4. Write a Rectangle method called translate: that takes an XYPoint object as its argument. Have it translate the rectangle's origin by the specified vector. Note: Translation simply means moving the point from one place to another.
- 5. Define a new class called GraphicObject, and make it a subclass of NSObject. Define instance variables in your new class as follows:

```objc
int    fillColor;   // 32-bit color
BOOL   filled;      // Is the object filled?
int    lineColor;   // 32-bit line color
```

Write methods to set and retrieve the variables defined previously.

Make the Rectangle class a subclass of GraphicObject.

Define new classes, Circle and Triangle, which are also subclasses of GraphicObject. Write methods to set and retrieve the various parameters for these objects and also to calculate the circle's circumference and area, and the triangle's perimeter and area.
- 6. Write a Rectangle method called containsPoint: that takes an XYPoint object as its argument:

```objc
-(BOOL) containsPoint: (XYPoint *) aPoint;
```

Have the method return the BOOL value YES if the rectangle encloses the specified point and NO if it does.
- 7. Write a Rectangle method called intersect: that takes a rectangle as an argument and returns a rectangle representing the overlapping area between the two rectangles. For example, given the two rectangles shown in Figure 8.10, the method should return a rectangle whose origin is at (400, 420), whose width is 50, and whose height is 60.

# Figure 8.10. Intersecting rectangles

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_280_0.png)

If the rectangles do not intersect, return one whose width and height are zero and whose origin is at (0,0).
- 8. Write a method for the Rectangle class called draw draws a rectangle using dashes and vertical bar characters. The following code sequence

```objc
Rectangle *myRect = [[Rectangle alloc] init];
myRect setWidth: 10 andHeight: 3;
myRect draw;
```

would produce the following output:

```
|   |
|   |
|   |
|   |
|   |
------
```
