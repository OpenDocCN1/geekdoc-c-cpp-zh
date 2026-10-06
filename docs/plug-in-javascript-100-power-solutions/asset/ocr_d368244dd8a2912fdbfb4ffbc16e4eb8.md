call, it's necessary to ensure that the interrupting call moves at the same speed as the one specified in the call.

For example, if the call to Slide specifies an animation time of 1000 milliseconds, but it interrupts another slide and discovers that the object is now only one third of the distance from the destination (instead of the 100 percent it would have been if this was the first Slide call on the object), then the new slide should only take one-third of 1000 milliseconds to move, or 333 milliseconds.

# Using the Pythagorean Theorem

To calculate the new distance to travel, and there, determine the speed of the new slide, the plug-in uses the Pythagorean theorem, which states that on a right angled triangle, the volume of the square on the hypotenuse is equal to the sum of the squares of the other two sides.

This works because if you draw a line between any two points, on a two-dimensional surface such as a browser, you can draw a horizontal line from one point and a vertical line from the other so that they meet each other at a single coordinate to create a right angled triangle, with the longest edge connecting the two locations.

Therefore, using the Pythagorean theorem, the distance between the requested start and ends is determined by passing the results of frx and fry to the subfunction Distance().

```
var len = Distance(tox - frx, toy - fry)
```

The Distance() function looks like this:

```
function Distance(x, y) {
  x = Math.max(1, x)
  y = Math.max(1, y)
  return Math.round(Math.sqrt(Math.abs(x * x) + Math.abs(y * y)))
}
```

The variable x is the length of one short side of the triangle, while y is the length of the other side. If either value is 0, it is changed to 1, otherwise division-by-zero errors may occur.

Each value is multiplied by itself to determine the volumes of the squares, and they are converted to absolute values, since they could be negative numbers. These figures are added together to get their combined volume, which is also the volume of the square on the long side of the triangle.

Finally, to discover the length of the triangle's longest side, the square root of this new value is returned—the distance in pixels between the locations frx,fry and toy.

With the distance stored in len, the values of frx and fry are overwritten with those of the actual coordinates of the code, looking them up with the X() and Y() plug-ins using the following code: the plug-in will use this new start location, overriding the one passed to it by the calling code:

```
frx = X(id)
fry = Y(id)
```