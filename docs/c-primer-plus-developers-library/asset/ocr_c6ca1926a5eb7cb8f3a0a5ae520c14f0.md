Notice that the formal variable is type polar. When you pass a polar structure to this function, the structure contents are copied into the dapos structure, and the function then uses that copy in its work. Because dapos is a structure, the function uses the membership (dot) operator (see Chapter 4) to identify structure members.

Next, let’s try something more ambitious and write a function that converts rectangular coordinates to polar coordinates. We’ll have the function accept a rect structure as its argument and return a polar structure to the calling function. This involves using functions from the math library, so the program has to include the cmath header file (math.h on older systems). Also on some systems you have to tell the compiler to load the math library (see Chapter 1, “Getting Started with C++”). You can use the Pythagorean theorem to get the distance from the horizontal and vertical components:

`distance = sqrt( x * x + y * y )`

The `atan2()` function from the math library calculates the angle from the x and y values:

`angle = atan2(y, x)`

(There’s also an `atan()` function, but it doesn’t distinguish between angles 180 degrees apart. That uncertainty is no more desirable in a math function than it is in a wilderness guide.)

Given these formulas, you can write the function as follows:

```
```cpp
// convert rectangular to polar coordinates
polar rect_to_polar(rect xypos)   // type polar
{
    polar answer;

    answer.distance =
        sqrt( xypos.x * xypos.x + xypos.y * xypos.y);
    answer.angle = atan2(xypos.y, xypos.x);
    return answer;      // returns a polar structure
}
```
```

Now that the functions are ready, writing the rest of the program is straightforward. Listing 7.12 presents the result.

# Listing 7.12  structfun.cpp

```
```cpp
// structfun.cpp -- functions with a structure argument
#include <iostream>
#include <cmath>

// structure declarations
struct polar
{
    double distance;    // distance from origin
    double angle;       // direction from origin
};
struct rect
```
```