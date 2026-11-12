Functions are defined in an implementation file (filename ending in .m). It starts with the function signature. This defines the function’s name, the return value, and the function’s arguments. Arguments will appear as a comma-separated list surrounded by parentheses. Inside the list, each argument declares a data type and a name.

A pair of curly brackets follows the function signature. We can place any number of expressions inside these brackets. When the function is called, these expressions are executed in the order in which they appear.

```
CGFloat calculateDistance(CGPoint p1, CGPoint p2) {

    CGFloat xDist = p1.x - p2.x;
    CGFloat yDist = p1.y - p2.y;

    // Calculate the distance using the Pythagorean theorem.
    return sqrt(xDist * xDist + yDist * yDist);
}
```

In the above example, reading left to right, CGFloat is the return value, calculateDistance is the function name, and CGPoint p1 and CGPoint p2 are the function’s two arguments.

Inside the function, we first create two local variables. These variables are stored on the stack and will be automatically deleted when the method returns. We assign the difference between our point’s x- and y-coordinates to these variables.

The next line is blank. Whitespace is ignored by the compiler and should be used to organize your code, making it easier to follow and understand. Then we have a comment. The compiler will ignore anything after // until the end of the line. It will also ignore anything between /* and */, allowing us to create comments spanning several lines.

Finally, we reach the return keyword. This evaluates the expression to its right and then exits the function, returning the expression’s value (if any) to the caller. The calculateDistance() function calculates the distance between two points using the Pythagorean theorem. Here we square the x and y distances using the multiply operator. We add them together. Then we pass that value to the C math library’s sqrt() function and return the result.