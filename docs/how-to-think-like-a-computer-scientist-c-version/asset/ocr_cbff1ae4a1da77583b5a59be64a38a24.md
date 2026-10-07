# 5.3. COMPOSITION

```
double distance (double x1, double y1, double x2, double y2) {
double dx = x2 - x1;
double dy = y2 - y1;
double dsared = dx*dx + dy*dy;
double result = sqrt (squared);
}
```

Then in main, we should output and check the value of the result.
As you gain more experience programming, you might find yourself writing and debugging more than one line at a time. Nevertheless, this incremental development process can save you a lot of debugging time.
The key aspects of the process are:

+   - Start with a working program and make small, incremental changes. At any point, if there is an error, you will know exactly where it is.
- Use temporary variables to hold intermediate values so you can output and check them.
- Once the program is working, you might want to remove some of the scaffolding or consolidate multiple statements into compound expressions, but only if it does not make the program difficult to read.

# 5.3 Composition

As you should expect by now, once you define a new function, you can use it as part of an expression, and you can build new functions using existing functions. For example, if someone gave you two points, the center of the circle and a point on the perimeter, and asked for the area of the circle?
Let's say the center point is stored in the variables xc and yc, and the perimeter point is in xp and yp. The first step is to find the radius of the circle, which is the distance between the two points. Fortunately, we have a function, does that.

```
double radius = distance (xc, yc, xp, yp);
```

The second step is to find the area of a circle with that radius, and return it.

```
double result = area (radius);
return result;
```

Wrapping that up in a function, we get:

```
double fred (double xc, double yc, double xp, double yp) {
double radius = distance (xc, yc, xp, yp);
double result = area (radius);
return result;
```