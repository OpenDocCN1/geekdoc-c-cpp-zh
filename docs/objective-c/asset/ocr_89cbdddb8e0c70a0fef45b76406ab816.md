Tie these together to show some code that actually uses a struct to store and displays some points. This is shown in Listing 2.12.

# Listing 2.12

# Working with point structures

```
#import <Foundation/Foundation.h>

// declaring the point structure.
struct Point
{
    float x;
    float y;
};

int main(int argc, const char *argv[])
{
    // declaring the point variable...
    struct Point p;
    // assigning values to the struct's members...
    p.x = 20.0;
    p.y = 50.0;

    // ... then to use the point...
    moveCursorToPoint(p);

    return 0;
}
```

Objective-C and Cocoa use structures for storing things such as points, rectangles, and so on. The nice thing about using structures is that they are a very lightweight way to store groups of related variables. In Chapter 3, you see how to use objects to also group related variables and the methods that act on those variables. However, objects can have a fair amount of overhead associated with them. Structures, on the other hand, have no more overhead than the variables that make up their members. Therefore, they can sometimes be used in performance-sensitive areas where objects would be too heavy.

# Using typedefs

Naturally, typing struct Point every time you want to declare a point can quickly become tedious. Fortunately, Objective-C provides another construct that can help with this. This construct is called typedef.