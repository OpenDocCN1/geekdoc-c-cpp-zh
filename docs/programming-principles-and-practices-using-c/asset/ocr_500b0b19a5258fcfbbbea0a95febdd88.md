```
Function(Fct f, double r1, double r2, Point orig,
int count = 100, double xscale = 25, double yscale = 25);
};
```

Function is a Shape with a constructor that generates a lot of line segments and stores them in its Shape part. Those line segments approximate the values of function f. The values of f are calculated count times for values equally spaced in the [r1:r2] range:

```
Function::Function(Fct f, double r1, double r2, Point xy,
int count, double xscale, double yscale)
// graph f(x) for x in [r1:r2] using count line segments with (0,0) displayed at xy
// x coordinates are scaled by xscale and y coordinates scaled by yscale
{
if (r2–r1<=0) error("bad graphing range");
if (count <=0) error("non-positive graphing count");
double dist = (r2–r1)/count;
double r = r1;
for (int i = 0; i<count; ++i) {
add(Point{xy.x+int(r*xscale),xy.y-int(f(r)*yscale)});
r += dist;
}
}
```

The xscale and yscale values are used to scale the x coordinates and the y coordinates, respectively. We typically need to scale our values to make them fit appropriately into a drawing area of a window.

Note that a Function object doesn’t store the values given to its constructor, so we can’t later ask a function where its origin is, redraw it with different scaling, etc. All it does is to store points (in its Shape) and draw itself on the screen. If we wanted the flexibility to change a Function after construction, we would have to store the values we wanted to change (see exercise 2).

What is the type Fct that we used to represent a function argument? It is a variant of a standard library type called std::function that can “remember” a function to be called later. Fct requires its argument to be a double and its return type to be a double.

# 15.3.1 Default Arguments

Note the way the Function constructor arguments xscale and yscale were given initializers in the declaration. Such initializers are called default arguments and their values are used if a caller doesn’t supply values. For example:

```
Function s {one, r_min, r_max,orig, n_points, x_scale, y_scale};
Function s2 {slope, r_min, r_max, orig, n_points, x_scale}; // no yscale
```