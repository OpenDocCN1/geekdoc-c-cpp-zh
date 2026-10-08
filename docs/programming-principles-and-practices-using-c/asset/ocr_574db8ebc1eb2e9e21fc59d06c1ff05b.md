with data and options without a framework to help understanding, debugging, and performance.

# 14.1.2 Operations

+   * We provide a minimum of operations as part of each class. Our ideal is the minimal interface that allows us to do what we want. Where we want greater convenience, we can always provide it in the form of added nonmember functions or yet another class.

+   * We want the interfaces of our classes to show a common style. For example, all functions performing similar operations in different classes have the same name, take arguments of the same types, and where possible require those arguments in the same order. Consider the constructors: if a shape requires a location, it takes `Point` as its first argument:

```
Line ln{Point{100,200},Point{300,400}};
Mark m{Point{100,200},'x'};  // display a single point as an 'x'
Circle c{Point{200,200},250};
```

All functions that deal with points use class `Point` to represent them. That would seem obvious, but many libraries exhibit a mixture of styles. For example, imagine a function for drawing a line. We could use one of two styles:

```
void draw_line(Point p1, Point p2);  // from p1 to p2 (our style)
void draw_line(int x1, int y1, int x2, int y2);  // from (x1,y1) to (x2,y2)
```

We could even allow both, but for consistency, improved type checking, and improved readability we use the first style exclusively. Using `Point` consistently also saves us from confusion between coordinate pairs and the other common pair of integers: width and height. For example, consider:

```
draw_rectangle(Point{100,200}, 300, 400);  // our style
draw_rectangle(100,200,300,400);  // alternative
```

The first call draws a rectangle with a point, width, and height. That's reasonably easy to guess, but how about the second call? Is that a rectangle defined by points (100,200) and (300,400)? A rectangle defined by a point (100,200), a width 300, and a height 400? Something completely different (though plausible to someone)? Using the `Point` type consistently avoids such confusion.

Incidentally, if a function requires a width and a height, they are always presented in that order (just as we always give an x coordinate before a y coordinate). Getting such little details consistent makes a surprisingly large difference to the ease of use and the avoidance of run-time errors.