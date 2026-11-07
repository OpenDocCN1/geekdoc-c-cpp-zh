However, without declaring the destructor, move semantics works for both Polygon members, name and points. Consider the following program:

_poly/polygon.cpp_

```
```cpp
#include "geoobj.hpp"
#include "polygon.hpp"

int main()
{
    Polygon p0{"Poly1", {Coord{1,1}, Coord{1,9}, Coord{9,9}, Coord{9,1}}};
    Polygon p1{p0};             // copy
    Polygon p2{std::move(p0)};   // move

    p0.draw();
    p1.draw();
    p2.draw();
}
```
```

This program has the following output:

```
polygon '' over
polygon ’Poly1’ over (1,1) (1,9) (9,9) (9,1)
polygon ’Poly1’ over (1,1) (1,9) (9,9) (9,1)
```

For both members, name and points, the values were moved from p0 to p2.
Note that if you have to implement the move constructor in class Polygon, you need special care to provide the right noexcept condition.

# 4.5  Summary

+   - Avoid objects with names.
+   - Avoid unnecessary `std::move()`. Especially do not use it when returning a local object.
+   - Constructors that initialize members from parameters, for which move operations are cheap, should take the argument by value and move it to the member.
+   - Constructors that initialize members from parameters, for which move operations take a significant amount of time, should be overloaded for move semantics for best performance.
+   - In general, creating and initializing new values from parameters, for which move operations are cheap, should take the arguments by value and move. However, do not take by value and move to update/modify existing values.
+   - Do not declare a virtual destructor in derived classes (unless you have to implement it).